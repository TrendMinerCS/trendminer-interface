# Managing Work Items[¶](#managing-work-items)

The SDK allows us to create and update items in the work organizer of the authenticated user. This example uses value-based searches throughout, but the same retrieve, search, create, update and delete patterns apply to every saved item type.

For the object model behind these items — the interface facades, the objects they return, and the `*Definition` builders used to create them — see [Objects & Types](https://trendminercs.github.io/trendminer-interface/objects-and-types/index.md) and the [Interface tree](https://trendminercs.github.io/trendminer-interface/reference/interface-tree/index.md).

## Setup[¶](#setup)

We start by [authenticating our user](https://trendminercs.github.io/trendminer-interface/creating-a-client/index.md).

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
    username=os.environ["TM_USERNAME"],
    password=os.environ["TM_PASSWORD"],
    tz="Europe/Brussels",
)
```

import os import pandas as pd from dotenv import find_dotenv, load_dotenv from trendminer_interface import client_from_credentials

# Credentials and server details are securely stored in .env.docs for our example code.

# find_dotenv walks up from the working directory to locate it, so this works

# regardless of the directory the notebook is run from.

load_dotenv(find_dotenv(".env.docs", usecwd=True)) client = client_from_credentials( url=os.environ["TM_URL"], client_id=os.environ["TM_CLIENT_ID"], client_secret=os.environ["TM_CLIENT_SECRET"], username=os.environ["TM_USERNAME"], password=os.environ["TM_PASSWORD"], tz="Europe/Brussels", )

## Retrieving specific items[¶](#retrieving-specific-items)

To get an item from a specific location in our work organizer, we first retrieve the folder the item is in:

In \[3\]:

Copied!

```
folder = client.work.folder.from_path(names=["SDK work example"])
folder
```

folder = client.work.folder.from_path(names=["SDK work example"]) folder

We can then get an item with a specific name and of a specific type directly from this folder:

In \[4\]:

Copied!

```
from trendminer_interface import ValueBasedSearch

folder.get_item(
    name="SDK example search 1",
    content_type=ValueBasedSearch,
)
```

from trendminer_interface import ValueBasedSearch folder.get_item( name="SDK example search 1", content_type=ValueBasedSearch, )

If the item to retrieve sits directly in your home folder, you can do the following instead:

In \[5\]:

Copied!

```
client.work.my_work.get_item(
    name="SDK example search 2",
    content_type=ValueBasedSearch,
)
```

client.work.my_work.get_item( name="SDK example search 2", content_type=ValueBasedSearch, )

We can also retrieve items directly by their name from anywhere in our saved work by calling `from_name` on the appropriate interface:

In \[6\]:

Copied!

```
client.search.value.from_name("SDK example search 1")
```

client.search.value.from_name("SDK example search 1")

Note that when two or more items exist with the same name within the scope (a specific folder or the whole work organizer), an `AmbiguousResource` error will be raised.

## Searching for items[¶](#searching-for-items)

We can retrieve multiple items at once via a search in the work organizer. We filter on specific content types, or retrieve items of any content type by not passing a parameter.

From within a folder:

In \[7\]:

Copied!

```
folder.search_contents().collect()
```

folder.search_contents().collect()

From the home folder:

In \[8\]:

Copied!

```
client.work.my_work.search_contents(content_type=ValueBasedSearch).collect()
```

client.work.my_work.search_contents(content_type=ValueBasedSearch).collect()

Searching the full work organizer from a content-type-specific interface allows us to filter on a name/description `query` parameter:

In \[9\]:

Copied!

```
client.search.value.search(query="SDK *").collect()
```

client.search.value.search(query="SDK \*").collect()

## Creating, updating and deleting items[¶](#creating-updating-and-deleting-items)

The SDK allows the creation of work items of most types. Creating a new item first requires us to create a definition instance containing the desired configuration. This configuration is of course highly specific to the type of work item we are creating — see [Objects & Types](https://trendminercs.github.io/trendminer-interface/objects-and-types/index.md) for the available `*Definition` builders.

In \[10\]:

Copied!

```
hour_tag = client.tag.from_name("TM_Hour_UTC")

vbs_def = client.search.value.define(
    queries=[(hour_tag, ">", 12)],
)

vbs_def
```

hour_tag = client.tag.from_name("TM_Hour_UTC") vbs_def = client.search.value.define( queries=[(hour_tag, ">", 12)], ) vbs_def

Note that these definitions can be actionable in themselves. For example, we do not need to actually save a value-based search item in the work organizer in order to get search results (see the [Value-based search](https://trendminercs.github.io/trendminer-interface/examples/value_based_search/index.md) example for more on running searches).

In \[11\]:

Copied!

```
import pandas as pd

search_interval = pd.Interval(
    pd.Timestamp("2026-01-01", tz=client.tz),
    pd.Timestamp("2026-02-01", tz=client.tz),
)

vbs_def.get_results(target=search_interval)
```

import pandas as pd search_interval = pd.Interval( pd.Timestamp("2026-01-01", tz=client.tz), pd.Timestamp("2026-02-01", tz=client.tz), ) vbs_def.get_results(target=search_interval)

When actually saving the work item, we need to provide a name, and optionally a description and save location (folder) as well. The action of creating the item returns the newly created item.

In \[12\]:

Copied!

```
vbs = client.search.value.create(
    name="My New Search",
    description="An example search",
    folder=folder,
    definition=vbs_def,
)

vbs
```

vbs = client.search.value.create( name="My New Search", description="An example search", folder=folder, definition=vbs_def, ) vbs

Folders do not carry a definition, and can be created directly:

In \[13\]:

Copied!

```
new_folder = client.work.folder.create(
    name="New Folder",
    folder=None, # place in home folder
)
new_folder
```

new_folder = client.work.folder.create( name="New Folder", folder=None, # place in home folder ) new_folder

We can update definition and the metadata properties of our saved items.

In \[14\]:

Copied!

```
vbs.definition.duration = pd.Timedelta(hours=1)
vbs.name = "My Updated Search"

vbs = vbs.update()
vbs
```

vbs.definition.duration = pd.Timedelta(hours=1) vbs.name = "My Updated Search" vbs = vbs.update() vbs

All work items will also have a (non-reversible) delete method:

In \[15\]:

Copied!

```
vbs.delete()
```

vbs.delete()

Deleting a folder deletes all items in it.

In \[16\]:

Copied!

```
new_folder.delete()
```

new_folder.delete()

## Caveat on deleting Tag Builder items[¶](#caveat-on-deleting-tag-builder-items)

As Tag Builder work items (`Formula`, `Aggregation`, ...) lead to the creation of a new tag, their names need to be unique over the whole TrendMiner instance. However, deleting a Tag Builder item does not free up the name for re-use. The result is that **you can never re-use the name of a deleted Tag Builder tag**.

To avoid names becoming unavailable, best practice is to rename Tag Builder items before deleting them:

In \[17\]:

Copied!

```
def safe_delete(item):
    # Add the current time to the name and update
    item.name = item.name + pd.Timestamp.now().isoformat()
    item.update()

    # We can safely delete now
    item.delete()
    print(f"Deleted as '{item.name}'")


agg_def = client.tag_builder.aggregation.define(
    target=hour_tag,
    method="mean",
    position="center",
    window=pd.Timedelta(hours=3),
)

agg = client.tag_builder.aggregation.create(
    name="ReusableTag",
    definition=agg_def,
)

safe_delete(agg)
```

def safe_delete(item):

# Add the current time to the name and update

item.name = item.name + pd.Timestamp.now().isoformat() item.update()

# We can safely delete now

item.delete() print(f"Deleted as '{item.name}'") agg_def = client.tag_builder.aggregation.define( target=hour_tag, method="mean", position="center", window=pd.Timedelta(hours=3), ) agg = client.tag_builder.aggregation.create( name="ReusableTag", definition=agg_def, ) safe_delete(agg)

Name blocking also occurs for Tag Builder items which have been implicitly deleted because the folder they were in got deleted. For safely deleting a folder that may contain Tag Builder items, we can build a folder crawler-renamer function:

In \[18\]:

Copied!

```
from trendminer_interface import Formula, Aggregation, CustomCalculation, Prediction, MachineLearningModel, Folder


tag_builder_types = [Formula, Aggregation, CustomCalculation, Prediction, MachineLearningModel]


def rename_folder_tags(folder: Folder):

    # Rename tag builder items
    for content_type in tag_builder_types:
        for item in folder.search_contents(content_type=content_type).stream(max_pages=None):
            item.name = item.name + pd.Timestamp.now().isoformat()
            item.update()
            print(f"Renamed to '{item.name}'")

    # Recursively rename items in subfolders
    for subfolder in folder.search_contents(content_type=Folder).stream(max_pages=None):
        rename_folder_tags(subfolder)


# As an example, create an aggregation in the existing folder
client.tag_builder.aggregation.create(
    name="ReusableTag",
    definition=agg_def,
    folder=folder,
)

# Rename all tag builder items in the folder
rename_folder_tags(folder)

# Folder can be safely deleted
folder.delete()
```

from trendminer_interface import Formula, Aggregation, CustomCalculation, Prediction, MachineLearningModel, Folder tag_builder_types = [Formula, Aggregation, CustomCalculation, Prediction, MachineLearningModel] def rename_folder_tags(folder: Folder):

# Rename tag builder items

for content_type in tag_builder_types: for item in folder.search_contents(content_type=content_type).stream(max_pages=None): item.name = item.name + pd.Timestamp.now().isoformat() item.update() print(f"Renamed to '{item.name}'")

# Recursively rename items in subfolders

for subfolder in folder.search_contents(content_type=Folder).stream(max_pages=None): rename_folder_tags(subfolder)

# As an example, create an aggregation in the existing folder

client.tag_builder.aggregation.create( name="ReusableTag", definition=agg_def, folder=folder, )

# Rename all tag builder items in the folder

rename_folder_tags(folder)

# Folder can be safely deleted

folder.delete()

## The upsert pattern[¶](#the-upsert-pattern)

Robust scripts check whether an item already exists before creating a new one. This prevents duplicate items with the same name from being created every time the script is run, and avoids an error for Tag Builder items (which need a unique name).

For example, to create a folder directly in our home folder only if it does not exist already, we can use the snippet below. We can run this snippet as many times as we want without creating any duplicates.

In \[19\]:

Copied!

```
from trendminer_interface.exceptions import ResourceNotFound

folder_name = "Project Folder"

# If the folder does not exist at the root level, create it
try:
    folder = client.work.folder.from_path(names=[folder_name])
except ResourceNotFound:
    folder = client.work.folder.create(
        name=folder_name,
        folder=None,
    )

folder
```

from trendminer_interface.exceptions import ResourceNotFound folder_name = "Project Folder"

# If the folder does not exist at the root level, create it

try: folder = client.work.folder.from_path(names=[folder_name]) except ResourceNotFound: folder = client.work.folder.create( name=folder_name, folder=None, ) folder

For items whose definition can change, we should make sure existing items get updated to the latest configuration (insert/update → upsert).

However, it is good to have the option to skip the update of existing items for when you know no changes to the definition have occurred. Especially for Tag Builder items, you want to avoid needlessly updating the items on the server, as this will remove existing indexes of the resulting tags.

In the example below, we check whether a value-based search with a given name exists specifically in our project folder, and update it if it does.

In \[20\]:

Copied!

```
update_existing = True

vbs_name = "MySearch"
vbs_def = client.search.value.define(
    queries=[(hour_tag, ">", 12)],
)

try:
    vbs = folder.get_item(name=vbs_name, content_type=ValueBasedSearch)
    if update_existing:
        vbs.definition = vbs_def
        vbs = vbs.update()
except ResourceNotFound:
    vbs = client.search.value.create(
        name=vbs_name,
        folder=folder,
        definition=vbs_def,
    )

vbs
```

update_existing = True vbs_name = "MySearch" vbs_def = client.search.value.define( queries=[(hour_tag, ">", 12)], ) try: vbs = folder.get_item(name=vbs_name, content_type=ValueBasedSearch) if update_existing: vbs.definition = vbs_def vbs = vbs.update() except ResourceNotFound: vbs = client.search.value.create( name=vbs_name, folder=folder, definition=vbs_def, ) vbs
