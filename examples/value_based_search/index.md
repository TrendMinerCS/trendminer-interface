# Value-based search[¶](#value-based-search)

A *value-based search* finds the intervals in time where one or more tags meet a condition — for example, every period where a flow rate stays above a threshold. This notebook builds one up in three steps:

1. a basic search,
1. the same search enriched with **calculations**, and
1. a second search run **within the results** of the first.

Each step returns a `PagedDataFrame`; we call `.collect()` to materialise it into a pandas `DataFrame` whose `IntervalIndex` holds the found events.

## Setup[¶](#setup)

We start by [authenticating a client](https://trendminercs.github.io/trendminer-interface/creating-a-client/index.md) and retrieving the tags we need for our example.

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

level = client.tag.from_name("TM6-BP2-LEVEL.1")
temp = client.tag.from_name("TM6-BP2-TEMP.1")
product = client.tag.from_name("TM6-BP2-PRODUCT.1")
```

import os import pandas as pd from dotenv import find_dotenv, load_dotenv from trendminer_interface import client_from_credentials

# Credentials and server details are securely stored in .env.docs for our example code.

# find_dotenv walks up from the working directory to locate it, so this works

# regardless of the directory the notebook is run from.

load_dotenv(find_dotenv(".env.docs", usecwd=True)) client = client_from_credentials( url=os.environ["TM_URL"], client_id=os.environ["TM_CLIENT_ID"], client_secret=os.environ["TM_CLIENT_SECRET"], ) level = client.tag.from_name("TM6-BP2-LEVEL.1") temp = client.tag.from_name("TM6-BP2-TEMP.1") product = client.tag.from_name("TM6-BP2-PRODUCT.1")

## A basic search[¶](#a-basic-search)

A value-based search is built from one or more `(tag, operator, value)` queries and a minimum `duration`, then run over a time window with `get_results`. The result is a `PagedDataFrame` whose `IntervalIndex` holds the events where the condition held — here, every period of at least 15 minutes where the level stays above 10. The `open` column tells us whether a result is still ongoing at the end of the search window.

In \[2\]:

Copied!

```
# Time window to search in
search_window = pd.Interval(
    pd.Timestamp("2025-01-01", tz="UTC"),
    pd.Timestamp("2026-01-01", tz="UTC"),
)

high_level = client.search.value.define(
    queries=[
        (level, ">", 10),
    ],
    duration=pd.Timedelta(minutes=15),
)

df_high_level = high_level.get_results(target=search_window).collect()
df_high_level
```

# Time window to search in

search_window = pd.Interval( pd.Timestamp("2025-01-01", tz="UTC"), pd.Timestamp("2026-01-01", tz="UTC"), ) high_level = client.search.value.define( queries=[ (level, ">", 10), ], duration=pd.Timedelta(minutes=15), ) df_high_level = high_level.get_results(target=search_window).collect() df_high_level

## Adding calculations[¶](#adding-calculations)

By default a search returns only the event intervals. Passing `calculations` attaches computed columns to each event — each is a `(tag, method, unit)` tuple, keyed by the resulting column name. Here we record the product grade at the start of each event and the mean level during it.

In \[3\]:

Copied!

```
high_level = client.search.value.define(
    queries=[
        (level, ">", 10),
    ],
    duration=pd.Timedelta(minutes=15),
    calculations={
        "product": (product, "start", ""),
        "mean_level": (level, "mean", "m"),
    },
)

df_high_level = high_level.get_results(target=search_window).collect()
df_high_level
```

high_level = client.search.value.define( queries=[ (level, ">", 10), ], duration=pd.Timedelta(minutes=15), calculations={ "product": (product, "start", ""), "mean_level": (level, "mean", "m"), }, ) df_high_level = high_level.get_results(target=search_window).collect() df_high_level

## Searching within results[¶](#searching-within-results)

We can search directly within other events (a DataFrame with IntervalIndex). The existing columns (calculations) of the target will be kept, showing for each new search result the values of the original interval in which the new result sits.

In \[4\]:

Copied!

```
high_temp = client.search.value.define(
    queries=[
        (temp, ">", 20),
    ],
    duration=pd.Timedelta(minutes=2),
    calculations={
        "max_temp": (temp, "max", "degC"),
    }
)

df_high_temp = high_temp.get_results(target=df_high_level).collect()
df_high_temp
```

high_temp = client.search.value.define( queries=[ (temp, ">", 20), ], duration=pd.Timedelta(minutes=2), calculations={ "max_temp": (temp, "max", "degC"), } ) df_high_temp = high_temp.get_results(target=df_high_level).collect() df_high_temp
