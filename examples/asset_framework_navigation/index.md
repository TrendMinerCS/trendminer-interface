# Asset Framework Navigation[¶](#asset-framework-navigation)

An asset framework provides as structure to your collection of tags that make them easier to understand and navigate. Furthermore an asset framework allows cross-asset functionalities, as illustrated in the [Cross-Asset Rollout](https://trendminercs.github.io/trendminer-interface/examples/cross_asset_rollout/index.md) example.

## Setup[¶](#setup)

We start by [authenticating a client](https://trendminercs.github.io/trendminer-interface/creating-a-client/index.md) and retrieving the tags we need for our example. Keep in mind the authenticated user will need access to the asset framework.

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

## Retrieving specific assets[¶](#retrieving-specific-assets)

The deterministic way of retrieving a specific path is by its path of asset names, starting with the root asset. The root asset has the same name as the asset framework.

In \[2\]:

Copied!

```
framework_name = "DO NOT EDIT"

asset = client.asset_framework.asset.from_path(
    names=[framework_name, "Houston", "Time"]
)
asset
```

framework_name = "DO NOT EDIT" asset = client.asset_framework.asset.from_path( names=[framework_name, "Houston", "Time"] ) asset

We can always get the full hierarchy from an `Asset` instance:

In \[3\]:

Copied!

```
asset.get_hierarchy()
```

asset.get_hierarchy()

## Navigating the tree[¶](#navigating-the-tree)

From an asset, we can always retrieve its children (which can be `Asset` or `Attribute` instances), as well as its parent `Asset`.

In \[4\]:

Copied!

```
asset.search_children().collect()
```

asset.search_children().collect()

In \[5\]:

Copied!

```
asset.parent
```

asset.parent

Sometimes we will want to grab a specific child asset or attribute.

In \[6\]:

Copied!

```
asset.get_child_attribute(name="Hour")
```

asset.get_child_attribute(name="Hour")

## Searching for assets[¶](#searching-for-assets)

We often want to search for a specific set of assets, so we can apply the same operation to them. For example, we can look for all of the assets with a certain name in a specific asset framework:

In \[7\]:

Copied!

```
framework = client.asset_framework.from_name(framework_name)

assets = client.asset_framework.asset.search(
    name="Time",
    frameworks=[framework],
).collect()

assets
```

framework = client.asset_framework.from_name(framework_name) assets = client.asset_framework.asset.search( name="Time", frameworks=[framework], ).collect() assets

A more robust approach is to explicitly define asset templates in our framework, and use these to search.

In \[8\]:

Copied!

```
assets[0].template
```

assets[0].template

In \[9\]:

Copied!

```
client.asset_framework.asset.search(
    template="time tags",
    frameworks=[framework],
).collect()
```

client.asset_framework.asset.search( template="time tags", frameworks=[framework], ).collect()

Or we might want to navigate to a specific parent asset first, and then search in its direct children. Note that the `*` is a wildcard character in the search.

In \[10\]:

Copied!

```
from trendminer_interface import Asset

parent_asset = client.asset_framework.asset.from_path(
    names=["cip"],
)

assets = parent_asset.search_children(
    name="CIP Unit *",
    child_type=Asset,
).collect()

assets
```

from trendminer_interface import Asset parent_asset = client.asset_framework.asset.from_path( names=["cip"], ) assets = parent_asset.search_children( name="CIP Unit \*", child_type=Asset, ).collect() assets

We can also search in all decendants of an asset (direct or indirect):

In \[13\]:

Copied!

```
client.asset_framework.asset.search(
    name="CIP Unit *",
    ancestor=parent_asset,
).collect()
```

client.asset_framework.asset.search( name="CIP Unit \*", ancestor=parent_asset, ).collect()
