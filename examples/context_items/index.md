# Context items[¶](#context-items)

*Context items* are the annotations that live in TrendMiner's ContextHub: each one marks a period of time on a specific [`Tag`](https://trendminercs.github.io/trendminer-interface/reference/types/objects/Tag/index.md), [`Asset`](https://trendminercs.github.io/trendminer-interface/reference/types/objects/Asset/index.md) or [`Attribute`](https://trendminercs.github.io/trendminer-interface/reference/types/objects/Attribute/index.md), carries a [`ContextType`](https://trendminercs.github.io/trendminer-interface/reference/types/objects/ContextType/index.md), and can hold a description, keywords and typed fields.

The SDK represents a set of context items as **events** — a [`pandas.DataFrame`](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.html) whose [`IntervalIndex`](https://pandas.pydata.org/docs/reference/api/pandas.IntervalIndex.html) holds each item's start and end, alongside columns for its type, component and other metadata (see [Interval utilities](https://trendminercs.github.io/trendminer-interface/interval-utilities/index.md) for this shared *events* vocabulary). Every operation in this notebook is really just building or reshaping such a DataFrame and handing it to the [`client.context`](https://trendminercs.github.io/trendminer-interface/reference/interfaces/context/index.md) facade.

This example shows how to create, retrieve, update and delete context items, and then how to populate them at scale — from a [value-based search](https://trendminercs.github.io/trendminer-interface/examples/value_based_search/index.md), from a monitor, and from a scheduled update service.

## Setup[¶](#setup)

We start by [authenticating a client](https://trendminercs.github.io/trendminer-interface/creating-a-client/index.md).

In \[1\]:

Copied!

```
import os

import pandas as pd
from dotenv import find_dotenv, load_dotenv

from trendminer_interface import client_from_credentials

# Credentials and server details are securely stored in .env.docs for our example code.
# find_dotenv walks up from the working directory to locate it, so this works
# regardless of the directory the notebook is run from.
load_dotenv(find_dotenv(".env.docs", usecwd=True))

client = client_from_credentials(
    url=os.environ["TM_URL"],
    client_id=os.environ["TM_CLIENT_ID"],
    client_secret=os.environ["TM_CLIENT_SECRET"],
)
```

import os import pandas as pd from dotenv import find_dotenv, load_dotenv from trendminer_interface import client_from_credentials

# Credentials and server details are securely stored in .env.docs for our example code.

# find_dotenv walks up from the working directory to locate it, so this works

# regardless of the directory the notebook is run from.

load_dotenv(find_dotenv(".env.docs", usecwd=True)) client = client_from_credentials( url=os.environ["TM_URL"], client_id=os.environ["TM_CLIENT_ID"], client_secret=os.environ["TM_CLIENT_SECRET"], )

## Creating context items[¶](#creating-context-items)

Creating context items comes down to assembling a DataFrame with the right structure and passing it to [`client.context.item.create`](https://trendminercs.github.io/trendminer-interface/reference/interfaces/context.item/index.md). We build that DataFrame up one column at a time.

The index must be an [`IntervalIndex`](https://pandas.pydata.org/docs/reference/api/pandas.IntervalIndex.html) of timezone-aware timestamps — each interval becomes one context item's start and end. Here we use [`pandas.interval_range`](https://pandas.pydata.org/docs/reference/api/pandas.interval_range.html) to make one month-long item for each of the last six months, anchored to the client's timezone (`client.tz`).

In \[2\]:

Copied!

```
# 1 item per month for the last 6 months
df = pd.DataFrame(
    index=pd.interval_range(
        end=pd.Timestamp.now(tz=client.tz).normalize(), 
        freq="MS", 
        periods=6,
    ),
)
```

# 1 item per month for the last 6 months

df = pd.DataFrame( index=pd.interval_range( end=pd.Timestamp.now(tz=client.tz).normalize(), freq="MS", periods=6, ), )

The `type` column holds each item's [`ContextType`](https://trendminercs.github.io/trendminer-interface/reference/types/objects/ContextType/index.md), which we look up by name through the [`client.context.type`](https://trendminercs.github.io/trendminer-interface/reference/interfaces/context.type/index.md) interface. We assign a single type to every row here, but the column may mix types freely.

In \[3\]:

Copied!

```
context_type = client.context.type.from_name("Month Example")
df["type"] = context_type
```

context_type = client.context.type.from_name("Month Example") df["type"] = context_type

Every item is anchored to a *component* — a [`Tag`](https://trendminercs.github.io/trendminer-interface/reference/types/objects/Tag/index.md), [`Asset`](https://trendminercs.github.io/trendminer-interface/reference/types/objects/Asset/index.md) or [`Attribute`](https://trendminercs.github.io/trendminer-interface/reference/types/objects/Attribute/index.md) — supplied in the `component` column. We look our tag up by name with [`client.tag.from_name`](https://trendminercs.github.io/trendminer-interface/reference/interfaces/tag/index.md); see [Asset Framework navigation](https://trendminercs.github.io/trendminer-interface/examples/asset_framework_navigation/index.md) for retrieving assets and attributes instead.

In \[4\]:

Copied!

```
month_tag = client.tag.from_name("TM_Month_UTC")
df["component"] = month_tag
```

month_tag = client.tag.from_name("TM_Month_UTC") df["component"] = month_tag

Two further columns are recognised as first-class item metadata: `description` (a string) and `keywords` (a list of strings per row). Both are optional.

In \[5\]:

Copied!

```
description = "Monthly overview"
df["description"] = description

keywords = ["sdk"]
df["keywords"] = [keywords] * len(df)
```

description = "Monthly overview" df["description"] = description keywords = ["sdk"] df["keywords"] = [keywords] * len(df)

Any remaining columns are stored as **fields** on the item. When a column name matches the [`key`](https://trendminercs.github.io/trendminer-interface/reference/types/objects/ContextField/index.md) of one of the type's [`fields`](https://trendminercs.github.io/trendminer-interface/reference/types/objects/ContextType/index.md) (`ContextType.fields`), its value is shown and formatted in that field in TrendMiner; a column that matches no field key appears instead as an *Other Property*.

In \[6\]:

Copied!

```
df["month"] = df.index.left.month_name()
```

df["month"] = df.index.left.month_name()

The completed DataFrame looks like this:

In \[7\]:

Copied!

```
df
```

df

With the DataFrame complete, a single call creates every item on the server:

In \[8\]:

Copied!

```
client.context.item.create(items=df)
```

client.context.item.create(items=df)

## Retrieving, updating and deleting context items[¶](#retrieving-updating-and-deleting-context-items)

Items are retrieved by describing *which* items you want with a set of **filters**. Each filter is built from the [`client.context.filter`](https://trendminercs.github.io/trendminer-interface/reference/interfaces/context.filter/index.md) interface; combined, they narrow the result down to the items created above. Filtering on [`created_by`](https://trendminercs.github.io/trendminer-interface/reference/types/objects/ContextCreatedByFilter/index.md) is the only way to fully control what comes back — other users may have created items that match the rest of your filters.

The filters are bundled into a [`ContextHubViewDefinition`](https://trendminercs.github.io/trendminer-interface/reference/types/definitions/ContextHubViewDefinition/index.md) via [`client.context.view.define`](https://trendminercs.github.io/trendminer-interface/reference/interfaces/context.view/index.md), whose `get_items` returns a lazy [`PagedDataFrame`](https://trendminercs.github.io/trendminer-interface/reference/types/containers/PagedDataFrame/index.md); calling `collect` materialises it into an events DataFrame. Notice that creating the items added a lot of metadata (keys, identifiers, timestamps), while the data we supplied came back intact.

In \[9\]:

Copied!

```
context_filters = [
    client.context.filter.created_by.new(users=[client.user.self]),
    client.context.filter.period.new(period=pd.Timedelta(days=200)),
    client.context.filter.context_types.new(types=[context_type]),
    client.context.filter.keyword.new(keywords=["sdk"]),
    client.context.filter.components.new(queries=[(month_tag, "self")])
]

chv_def = client.context.view.define(
    filters=context_filters,
)

df = chv_def.get_items().collect()
df
```

context_filters = \[ client.context.filter.created_by.new(users=[client.user.self]), client.context.filter.period.new(period=pd.Timedelta(days=200)), client.context.filter.context_types.new(types=[context_type]), client.context.filter.keyword.new(keywords=["sdk"]), client.context.filter.components.new(queries=[(month_tag, "self")]) \] chv_def = client.context.view.define( filters=context_filters, ) df = chv_def.get_items().collect() df

To update items, modify the DataFrame and pass it to [`client.context.item.update`](https://trendminercs.github.io/trendminer-interface/reference/interfaces/context.item/index.md). Rows are matched to existing items through the `identifier` column that `get_items` returned, so keep that column intact.

In \[10\]:

Copied!

```
df["description"] = "Updated item"

client.context.item.update(df)
```

df["description"] = "Updated item" client.context.item.update(df)

The most efficient way to delete items is [`ContextHubViewDefinition.delete_items`](https://trendminercs.github.io/trendminer-interface/reference/types/definitions/ContextHubViewDefinition/index.md), which removes every item matching the definition's filters. This is powerful and easy to misuse: with loose filters you can delete far more than you intended. As a safeguard, always include at least a [`ContextCreatedByFilter`](https://trendminercs.github.io/trendminer-interface/reference/types/objects/ContextCreatedByFilter/index.md) scoped to specific users (usually yourself), so you never remove other users' items.

In \[11\]:

Copied!

```
chv_def.delete_items()
```

chv_def.delete_items()

## Populating items from a search[¶](#populating-items-from-a-search)

A common pattern is to run a [value-based search](https://trendminercs.github.io/trendminer-interface/examples/value_based_search/index.md) and turn each result into a context item — often writing the search's calculations straight into context fields. The call below reuses the search from that example and adds the `component` and `type` columns that make its result a valid input for [`create`](https://trendminercs.github.io/trendminer-interface/reference/interfaces/context.item/index.md).

Watch out for **open** results (rows where the `open` column is `True`): these create *open* context items that will never be closed, because there is no link back to the originating search. To avoid items that stay open indefinitely, either drop the open rows (creating no item for them) or clear/adjust the `open` column so a closed item is written up to the current time.

In \[12\]:

Copied!

```
now = pd.Timestamp.now(tz=client.tz)
search_interval=pd.Interval(
    now - pd.Timedelta(days=180),
    now,
)

vbs_def = client.search.value.define(
    queries=[(month_tag, "constant")],
    calculations={
        "month": (month_tag, "start", ""),
    }
)

df = vbs_def.get_results(search_interval).collect()

df = df[~df["open"]]  # drop open results

df["component"] = month_tag
df["type"] = context_type
df["keywords"] = [keywords] * len(df)
df["description"] = description

df
```

now = pd.Timestamp.now(tz=client.tz) search_interval=pd.Interval( now - pd.Timedelta(days=180), now, ) vbs_def = client.search.value.define( queries=[(month_tag, "constant")], calculations={ "month": (month_tag, "start", ""), } ) df = vbs_def.get_results(search_interval).collect() df = df\[~df["open"]\] # drop open results df["component"] = month_tag df["type"] = context_type df["keywords"] = [keywords] * len(df) df["description"] = description df

## Creating items automatically with a monitor[¶](#creating-items-automatically-with-a-monitor)

Rather than writing historic items by hand, we can attach a **monitor** to a saved search so that every new result automatically becomes a context item. We persist the search with [`client.search.value.create`](https://trendminercs.github.io/trendminer-interface/reference/interfaces/search.value/index.md), take its monitor with `get_monitor`, and configure the monitor's [context settings](https://trendminercs.github.io/trendminer-interface/reference/types/objects/ContextItemMonitorNotification/index.md) — the type, component, description and keywords each new item should get. The same technique is used as part of the [Cross-asset rollout](https://trendminercs.github.io/trendminer-interface/examples/cross_asset_rollout/index.md) example.

In \[13\]:

Copied!

```
vbs = client.search.value.create(
    name="SDK Example - Months",
    definition=vbs_def,
)

monitor = vbs.get_monitor()

monitor.context.context_type = context_type
monitor.context.component = month_tag
monitor.context.description = description
monitor.context.keywords = keywords
monitor.context.enabled = True

monitor.update()
monitor.enable()
```

vbs = client.search.value.create( name="SDK Example - Months", definition=vbs_def, ) monitor = vbs.get_monitor() monitor.context.context_type = context_type monitor.context.component = month_tag monitor.context.description = description monitor.context.keywords = keywords monitor.context.enabled = True monitor.update() monitor.enable()

## Backfilling without creating duplicates[¶](#backfilling-without-creating-duplicates)

Typically we want a monitor for new events *and* a one-off backfill of the historic events that predate it. The catch: naively re-running the backfill creates duplicate items every time. Rather than relying on running it exactly once, the robust approach is to cross-reference the items that already exist and create only the ones that are missing — the same upsert idea used in [Managing work items](https://trendminercs.github.io/trendminer-interface/examples/managing_work_items/index.md).

In \[14\]:

Copied!

```
# `df` still holds the items initialised from the search above.

# Retrieve every item that already exists (all pages).
df_existing = chv_def.get_items().collect(max_pages=None)

# Keep only the intervals that are not present yet, and create those.
df_new = df[~df.index.isin(df_existing.index)]
client.context.item.create(df_new)
```

# `df` still holds the items initialised from the search above.

# Retrieve every item that already exists (all pages).

df_existing = chv_def.get_items().collect(max_pages=None)

# Keep only the intervals that are not present yet, and create those.

df_new = df[~df.index.isin(df_existing.index)] client.context.item.create(df_new)

## Keeping fields up to date with an update service[¶](#keeping-fields-up-to-date-with-an-update-service)

Items created by a monitor cannot carry dynamic calculations. To enrich them with calculations that are only correct once the event has finished, run a small update script on a schedule.

Two practical points make that script both safe and cheap:

- Filter on the target field being **empty** (a [`ContextStringFieldFilter`](https://trendminercs.github.io/trendminer-interface/reference/types/objects/ContextStringFieldFilter/index.md) in `"empty"` mode) so you only touch items that have not been updated yet.
- Filter on the item being **closed** (a [`ContextStateFilter`](https://trendminercs.github.io/trendminer-interface/reference/types/objects/ContextStateFilter/index.md)), since a still-open result gives premature calculation results — an integral or average would only cover the event up to *now*.

It is also good practice to update the index of the tags your calculations need at the start of the script; see [Indexing tags](https://trendminercs.github.io/trendminer-interface/examples/indexing_tags/index.md).

In \[15\]:

Copied!

```
month_tag.index()

context_field = client.context.field.from_name("month")

field_filter = client.context.filter.string_field.new(
    field=context_field, 
    mode="empty",
)

state_filter = client.context.filter.state.new(
    mode="closed",
)

# Keep the previous filters, add empty field filter
context_filters_update = context_filters + [field_filter]

chv_def_update = client.context.view.define(
    filters=context_filters_update,
)

# Get items, update the `month` field
df = chv_def_update.get_items().collect()
df = month_tag.add_aggregation(events=df, method="start", name="month")
client.context.item.update(df)
```

month_tag.index() context_field = client.context.field.from_name("month") field_filter = client.context.filter.string_field.new( field=context_field, mode="empty", ) state_filter = client.context.filter.state.new( mode="closed", )

# Keep the previous filters, add empty field filter

context_filters_update = context_filters + [field_filter] chv_def_update = client.context.view.define( filters=context_filters_update, )

# Get items, update the `month` field

df = chv_def_update.get_items().collect() df = month_tag.add_aggregation(events=df, method="start", name="month") client.context.item.update(df)
