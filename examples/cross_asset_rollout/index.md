# Cross-Asset Rollout[¶](#cross-asset-rollout)

The SDK provides a way to do bulk creation of work items by iterating over a set of assets. In this example, we will programatically create aggregation tags, TrendHub views, searches, monitors, ContextHub vies and dashboards for Cleaning in Place (CIP) assets.

If no asset framework is available, you can opt to iterate over tags instead by programatically inferring the tag names if the the names are systematically structured. If tag names are not uniform you can create a file of tag names for the script to read, though generating such a file would roughly be the same amount of effort as the cleaner and more permanent solution of building an asset framework in TrendMiner.

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

## Creating/updating items[¶](#creatingupdating-items)

As described in [Managing Work Items](https://trendminercs.github.io/trendminer-interface/examples/managing_work_items/index.md), we take care to not create duplicate items whenever we rerun the script. We define a parameter that defines what should be done if an item already exists throughout our entire script.

As long as we are simply adding additional items, we will want to ignore existing items, while if we make any changes in configuration, we will want to update the existing items as well.

In \[2\]:

Copied!

```
update_existing = True
```

update_existing = True

## Asset retrieval[¶](#asset-retrieval)

All CIP assets are named `CIP Unit *`, and sit under the `cip` parent.

In \[3\]:

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

## Folder structure[¶](#folder-structure)

All items will be stored under the same project folder, with a dedicated subfolder per asset.

In \[4\]:

Copied!

```
from trendminer_interface import Folder
from trendminer_interface.exceptions import ResourceNotFound

project_folder_name = "CIP"

# Get folder or create a new one
try:
    project_folder = client.work.folder.from_path(
        names=[project_folder_name]
    )
except ResourceNotFound:
    project_folder = client.work.folder.create(
        name=project_folder_name,
        folder=None,  # place in root directory
    )

project_folder
```

from trendminer_interface import Folder from trendminer_interface.exceptions import ResourceNotFound project_folder_name = "CIP"

# Get folder or create a new one

try: project_folder = client.work.folder.from_path( names=[project_folder_name] ) except ResourceNotFound: project_folder = client.work.folder.create( name=project_folder_name, folder=None, # place in root directory ) project_folder

We simply name the folder after the asset. We keep the folders accessible for later use.

In \[5\]:

Copied!

```
folder_dict = {}

for asset in assets:
    try:
        asset_folder = project_folder.get_item(
            name=asset.name,
            content_type=Folder,
        )
    except ResourceNotFound:
        asset_folder = client.work.folder.create(
            name=asset.name,
            folder=project_folder,
        )
        
    folder_dict[asset] = asset_folder
```

folder_dict = {} for asset in assets: try: asset_folder = project_folder.get_item( name=asset.name, content_type=Folder, ) except ResourceNotFound: asset_folder = client.work.folder.create( name=asset.name, folder=project_folder, ) folder_dict[asset] = asset_folder

## Tag Builder tags[¶](#tag-builder-tags)

The first object to create are additional Tag Builder tags, since additional objects will depend on them. In this example, we want to have a smoothed version of every asset's flow measurement by using a mean-value aggregation.

To avoid name clashes with other users, we will prefix the names of the tags we created with our username. Furthermore, we of course need to make sure any derived tag names are unique.

We will store the resulting tags (not the Aggregation work items) for future use.

In \[6\]:

Copied!

```
import pandas as pd
from trendminer_interface import Aggregation

aggregation_tag_dict = {}

for asset in assets:

    asset_folder = folder_dict[asset]
    
    conductivity = asset.get_child_attribute("Flow")

    aggregation_name = f"[{client.user.self.name}][{asset.name}][Flow][10m]"

    aggregation_def = client.tag_builder.aggregation.define(
        target=conductivity.tag,
        method="mean",
        position="center",
        window=pd.Timedelta(minutes=10),
        units="m3/h",
    )
    
    try:
        aggregation = asset_folder.get_item(
            name=aggregation_name, 
            content_type=Aggregation,
        )
        if update_existing:
            aggregation.definition = aggregation_def
            aggregation = aggregation.update()
    except ResourceNotFound:
        aggregation = client.tag_builder.aggregation.create(
            name=aggregation_name,
            folder=asset_folder,
            definition=aggregation_def,
        )

    aggregation_tag = client.tag.from_name(aggregation_name)
    aggregation_tag_dict[asset] = aggregation_tag

    # Request to update tag index
    aggregation_tag.index()
```

import pandas as pd from trendminer_interface import Aggregation aggregation_tag_dict = {} for asset in assets: asset_folder = folder_dict[asset] conductivity = asset.get_child_attribute("Flow") aggregation_name = f"[{client.user.self.name}][{asset.name}][Flow][10m]" aggregation_def = client.tag_builder.aggregation.define( target=conductivity.tag, method="mean", position="center", window=pd.Timedelta(minutes=10), units="m3/h", ) try: aggregation = asset_folder.get_item( name=aggregation_name, content_type=Aggregation, ) if update_existing: aggregation.definition = aggregation_def aggregation = aggregation.update() except ResourceNotFound: aggregation = client.tag_builder.aggregation.create( name=aggregation_name, folder=asset_folder, definition=aggregation_def, ) aggregation_tag = client.tag.from_name(aggregation_name) aggregation_tag_dict[asset] = aggregation_tag

# Request to update tag index

aggregation_tag.index()

## TrendHub views[¶](#trendhub-views)

We will create the TrendHub views that we will later add to the dashboards. We fix attribute and tag colors and scales for a uniform look.

In \[7\]:

Copied!

```
from trendminer_interface import TrendHubView

thv_dict = {}


for asset in assets:

    asset_folder = folder_dict[asset]

    # Phase attribute
    phase = asset.get_child_attribute("Phase")

    # Flow attribute and smoothed flow tag
    smoothed_flow_tag = aggregation_tag_dict[asset]
    smoothed_flow_tag.color = "#050dfa"

    flow = asset.get_child_attribute(name="Flow")
    flow.color = "#adbfdb"
    
    flow_group = client.trend.group.new(
        entries=[
            smoothed_flow_tag,
            flow,
        ],
        name="Flow",
        scale=(0, 70),
    )

    # Temperature
    temperature = asset.get_child_attribute("Temperature")

    # Single layer from start of September until current time
    # We will set the same interval for the context bar
    interval = pd.Interval(
        pd.Timestamp("2026-09-01", tz=client.tz),
        pd.Timestamp.now(tz=client.tz),
    )
    layer = client.trend.layer.new(
        interval=interval,
        base=True,  # base layer
    )

    # View definition
    thv_def = client.trend.view.define(
        entries=[phase, flow_group, temperature],
        layers=[layer],
        context_interval=interval,
        live=True,
    )

    # Create/update
    thv_name = asset.name + " Overview"
    try:
        thv = asset_folder.get_item(
            name=thv_name,
            content_type=TrendHubView,
        )
        if update_existing or True:
            thv.definition = thv_def
            thv.update()
    except ResourceNotFound:
        thv = client.trend.view.create(
            name=thv_name,
            folder=asset_folder,
            definition=thv_def,
        )

    thv_dict[asset] = thv
```

from trendminer_interface import TrendHubView thv_dict = {} for asset in assets: asset_folder = folder_dict[asset]

# Phase attribute

phase = asset.get_child_attribute("Phase")

# Flow attribute and smoothed flow tag

smoothed_flow_tag = aggregation_tag_dict[asset] smoothed_flow_tag.color = "#050dfa" flow = asset.get_child_attribute(name="Flow") flow.color = "#adbfdb" flow_group = client.trend.group.new( entries=[ smoothed_flow_tag, flow, ], name="Flow", scale=(0, 70), )

# Temperature

temperature = asset.get_child_attribute("Temperature")

# Single layer from start of September until current time

# We will set the same interval for the context bar

interval = pd.Interval( pd.Timestamp("2026-09-01", tz=client.tz), pd.Timestamp.now(tz=client.tz), ) layer = client.trend.layer.new( interval=interval, base=True, # base layer )

# View definition

thv_def = client.trend.view.define( entries=[phase, flow_group, temperature], layers=[layer], context_interval=interval, live=True, )

# Create/update

thv_name = asset.name + " Overview" try: thv = asset_folder.get_item( name=thv_name, content_type=TrendHubView, ) if update_existing or True: thv.definition = thv_def thv.update() except ResourceNotFound: thv = client.trend.view.create( name=thv_name, folder=asset_folder, definition=thv_def, ) thv_dict[asset] = thv

## Searches and monitors[¶](#searches-and-monitors)

We create a value-based search per asset, indicating whether the asset is active, as well as activate the monitor corresponding to the search. Note that creating a search automatically creates a matching monitor.

We will set up the monitor to create context items, of which we need to configure the context type.

In \[8\]:

Copied!

```
context_type = client.context.type.from_name("Operational")
context_type
```

context_type = client.context.type.from_name("Operational") context_type

In \[9\]:

Copied!

```
from trendminer_interface import ValueBasedSearch

vbs_dict = {}

for asset in assets:
    
    active = asset.get_child_attribute("Active")
    
    asset_folder = folder_dict[asset]

    vbs_name = asset.name + " Active"

    vbs_def = client.search.value.define(
        queries=[(active.tag, "=", "ON")],
    )

    # only update the monitor when we create/update the search
    update_monitor = False

    try:
        vbs = asset_folder.get_item(
            name=vbs_name, 
            content_type=ValueBasedSearch,
        )
        if update_existing:
            vbs.definition = vbs_def
            vbs = vbs.update()
            update_monitor = True
    except ResourceNotFound:
        vbs = client.search.value.create(
            name=vbs_name,
            folder=asset_folder,
            definition=vbs_def,
        )
        update_monitor = True
    
    vbs_dict[asset] = vbs

    if update_monitor:
        
        monitor = vbs.get_monitor()

        # Create context items on the asset
        monitor.context.component = asset
        monitor.context.context_type = context_type
        monitor.context.keywords = ["cip"]
        monitor.context.enabled = True

        # Send emails
        monitor.email.subject = asset.name + " started"
        monitor.email.message = f"CIP has started on asset '{asset.name}'"
        monitor.email.to = ["cip@trendminer.com"]
        monitor.email.enabled = True

        # Update and activate the monitor
        monitor.update()
        monitor.enable()
```

from trendminer_interface import ValueBasedSearch vbs_dict = {} for asset in assets: active = asset.get_child_attribute("Active") asset_folder = folder_dict[asset] vbs_name = asset.name + " Active" vbs_def = client.search.value.define( queries=[(active.tag, "=", "ON")], )

# only update the monitor when we create/update the search

update_monitor = False try: vbs = asset_folder.get_item( name=vbs_name, content_type=ValueBasedSearch, ) if update_existing: vbs.definition = vbs_def vbs = vbs.update() update_monitor = True except ResourceNotFound: vbs = client.search.value.create( name=vbs_name, folder=asset_folder, definition=vbs_def, ) update_monitor = True vbs_dict[asset] = vbs if update_monitor: monitor = vbs.get_monitor()

# Create context items on the asset

monitor.context.component = asset monitor.context.context_type = context_type monitor.context.keywords = ["cip"] monitor.context.enabled = True

# Send emails

monitor.email.subject = asset.name + " started" monitor.email.message = f"CIP has started on asset '{asset.name}'" monitor.email.to = ["cip@trendminer.com"] monitor.email.enabled = True

# Update and activate the monitor

monitor.update() monitor.enable()

## ContextHub views[¶](#contexthub-views)

We can now create ContextHub views which capture the context items created from the monitors we just set up. The views created below get all context items of the specified type of the last 30d, attached to the specific CIP asset. Furthermore we filter to only retreive items we created ourselves. This is best practice to avoid other user's context items interfering with our views.

In \[10\]:

Copied!

```
from trendminer_interface import ContextHubView

chv_dict = {}

for asset in assets:

    asset_folder = folder_dict[asset]

    chv_name = asset.name + " runs"
    
    chv_def = client.context.view.define(
        filters=[
            client.context.filter.period.new(pd.Timedelta(days=30)),
            client.context.filter.components.new([(asset, "self")]),
            client.context.filter.context_types.new([context_type]),
            client.context.filter.created_by.new([client.user.self]),
        ],
        view_type="grid",
    )

    try:
        chv = asset_folder.get_item(
            name=chv_name, 
            content_type=ContextHubView,
        )
        if update_existing:
            chv.definition = chv_def
            chv = chv.update()
    except ResourceNotFound:
        chv = client.context.view.create(
            name=chv_name,
            folder=asset_folder,
            definition=chv_def,
        )

    chv_dict[asset] = chv
```

from trendminer_interface import ContextHubView chv_dict = {} for asset in assets: asset_folder = folder_dict[asset] chv_name = asset.name + " runs" chv_def = client.context.view.define( filters=\[ client.context.filter.period.new(pd.Timedelta(days=30)), client.context.filter.components.new([(asset, "self")]), client.context.filter.context_types.new([context_type]), client.context.filter.created_by.new([client.user.self]), \], view_type="grid", ) try: chv = asset_folder.get_item( name=chv_name, content_type=ContextHubView, ) if update_existing: chv.definition = chv_def chv = chv.update() except ResourceNotFound: chv = client.context.view.create( name=chv_name, folder=asset_folder, definition=chv_def, ) chv_dict[asset] = chv

## Dashboards[¶](#dashboards)

Everything is now in place to create a dashboard per CIP unit. Furthermore, we will create a single dashboard showing an overview of all units. We will link the overview dashboard to the unit dashboards and vice versa via text tiles.

We start by getting an overview dashboard. In this case the overview dashboard starts out without any tiles. Then we create the unit dashboards and add tiles to the overview dashboard in one go. Every unit will get its own row on the overview dashboard. Note that we can only link the unit dashboard in the overview dashboard once the unit dashboard has been saved.

In \[12\]:

Copied!

```
from trendminer_interface import Dashboard
from urllib.parse import urljoin


def db_url(db: Dashboard):
    """Helper function to get dashboard url"""
    return urljoin(
        client.url,
        f"dashhub/#/dashboard/{db.identifier}",
)


overview_db_name = "CIP Overview"

overview_db_def = client.dashboard.define(
    tiles=[],
    live=True,
)

try:
    overview_db = project_folder.get_item(
        name=overview_db_name,
        content_type=Dashboard,
    )
    if update_existing:
        overview_db.definition = overview_db_def
        overview_db = overview_db.update()
except ResourceNotFound:
    overview_db = client.dashboard.create(
        name=overview_db_name,
        folder=project_folder,
        definition=overview_db_def,
    )


for i, asset in enumerate(assets):

    asset_folder = folder_dict[asset]

    # UNIT DASHBOARD
    tiles = []

    # Text tile - link back to overview
    overview_tile = client.dashboard.text.new(
        position=(0, 0, 4, 4),
        content=f'<h2><a href="{db_url(overview_db)}">To Overview</a></h2>'
    )
    tiles.append(overview_tile)

    # Flow rate gauge
    flow_gauge_config = client.dashboard.gauge.config(
        show_timestamp=False,
        show_range_labels=False,
    )
    flow_gauge_tile = client.dashboard.gauge.new(
        position=(4, 0, 4, 4),
        component=asset.get_child_attribute("Flow"),
        default_range=(0, 75, "off", "#ffffff"),
        ranges=[
            (1, 25, "low", "#2f8400"),  # green
            (25, 50, "increased", "#ffa03d"),  # orange
            (50, 75, "high", "#af1a00"),  # red
        ],
        title="Flow",
        config=flow_gauge_config,
    )
    tiles.append(flow_gauge_tile)

    # Temperature current value tile
    temperature = asset.get_child_attribute("Temperature")
    temp_value_config = client.dashboard.value.config(
        show_component_names=False,
        show_timestamp=False,
        show_title=False,
    )
    temp_value_tile = client.dashboard.value.new(
            position=(8, 0, 4, 4),
            entries=[(temperature, "", "#4070d6", [])],
            config=temp_value_config,
    )
    tiles.append(temp_value_tile)

    # 30d run counter
    counter_tile = client.dashboard.context.new(
        position=(12, 0, 4, 4),
        view=chv_dict[asset],
        mode="count",
        title="Runs last 30d",
    )
    tiles.append(counter_tile)

    # TrendHub view tile
    thv_tile_config = client.dashboard.trend.config(
        show_title=False,
        show_context_items=False,
    )
    thv_tile = client.dashboard.trend.new(
        position=(0, 4, 24, 8),
        view=thv_dict[asset],
        config=thv_tile_config,
    )
    tiles.append(thv_tile)


    # Create the unit dashboard
    db_name = asset.name
    db_def = client.dashboard.define(
        tiles=tiles,
        live=True,
    )
    try:
        db = asset_folder.get_item(
            name=db_name,
            content_type=Dashboard,
        )
        if update_existing:
            db.definition = db_def
            db.update()
    except ResourceNotFound:
        db = client.dashboard.create(
            name=db_name,
            folder=asset_folder,
            definition=db_def,
        )
        
    # OVERVIEW DASHBOARD
    # Row per asset in overview, 4 high
    overview_y_pos = 4*i  

    # Overview text tile - link to unit dashboard
    unit_tile = client.dashboard.text.new(
        position=(0, overview_y_pos, 4, 4),
        content=f'<h2><a href="{db_url(db)}">{asset.name}</a></h2>'
    )
    overview_db.definition.tiles.append(unit_tile)

    # Reuse some of the unit tiles, but at different position
    flow_gauge_tile.position = (4, overview_y_pos, 4, 4)
    temp_value_tile.position = (8, overview_y_pos, 4, 4)
    counter_tile.position = (12, overview_y_pos, 4, 4)
    
    overview_db.definition.tiles.extend([
        counter_tile, 
        temp_value_tile,
        flow_gauge_tile,
    ])

# Update the overview dashboard
overview_db.update()
```

from trendminer_interface import Dashboard from urllib.parse import urljoin def db_url(db: Dashboard): """Helper function to get dashboard url""" return urljoin( client.url, f"dashhub/#/dashboard/{db.identifier}", ) overview_db_name = "CIP Overview" overview_db_def = client.dashboard.define( tiles=[], live=True, ) try: overview_db = project_folder.get_item( name=overview_db_name, content_type=Dashboard, ) if update_existing: overview_db.definition = overview_db_def overview_db = overview_db.update() except ResourceNotFound: overview_db = client.dashboard.create( name=overview_db_name, folder=project_folder, definition=overview_db_def, ) for i, asset in enumerate(assets): asset_folder = folder_dict[asset]

# UNIT DASHBOARD

tiles = []

# Text tile - link back to overview

overview_tile = client.dashboard.text.new( position=(0, 0, 4, 4), content=f'

## [To Overview](<https://trendminercs.github.io/trendminer-interface/examples/cross_asset_rollout/%7Bdb_url(overview_db)%7D>)

' ) tiles.append(overview_tile)

# Flow rate gauge

flow_gauge_config = client.dashboard.gauge.config( show_timestamp=False, show_range_labels=False, ) flow_gauge_tile = client.dashboard.gauge.new( position=(4, 0, 4, 4), component=asset.get_child_attribute("Flow"), default_range=(0, 75, "off", "#ffffff"), ranges=[ (1, 25, "low", "#2f8400"), # green (25, 50, "increased", "#ffa03d"), # orange (50, 75, "high", "#af1a00"), # red ], title="Flow", config=flow_gauge_config, ) tiles.append(flow_gauge_tile)

# Temperature current value tile

temperature = asset.get_child_attribute("Temperature") temp_value_config = client.dashboard.value.config( show_component_names=False, show_timestamp=False, show_title=False, ) temp_value_tile = client.dashboard.value.new( position=(8, 0, 4, 4), entries=\[(temperature, "", "#4070d6", [])\], config=temp_value_config, ) tiles.append(temp_value_tile)

# 30d run counter

counter_tile = client.dashboard.context.new( position=(12, 0, 4, 4), view=chv_dict[asset], mode="count", title="Runs last 30d", ) tiles.append(counter_tile)

# TrendHub view tile

thv_tile_config = client.dashboard.trend.config( show_title=False, show_context_items=False, ) thv_tile = client.dashboard.trend.new( position=(0, 4, 24, 8), view=thv_dict[asset], config=thv_tile_config, ) tiles.append(thv_tile)

# Create the unit dashboard

db_name = asset.name db_def = client.dashboard.define( tiles=tiles, live=True, ) try: db = asset_folder.get_item( name=db_name, content_type=Dashboard, ) if update_existing: db.definition = db_def db.update() except ResourceNotFound: db = client.dashboard.create( name=db_name, folder=asset_folder, definition=db_def, )

# OVERVIEW DASHBOARD

# Row per asset in overview, 4 high

overview_y_pos = 4\*i

# Overview text tile - link to unit dashboard

unit_tile = client.dashboard.text.new( position=(0, overview_y_pos, 4, 4), content=f'

## [{asset.name}](<https://trendminercs.github.io/trendminer-interface/examples/cross_asset_rollout/%7Bdb_url(db)%7D>)

' ) overview_db.definition.tiles.append(unit_tile)

# Reuse some of the unit tiles, but at different position

flow_gauge_tile.position = (4, overview_y_pos, 4, 4) temp_value_tile.position = (8, overview_y_pos, 4, 4) counter_tile.position = (12, overview_y_pos, 4, 4) overview_db.definition.tiles.extend([ counter_tile, temp_value_tile, flow_gauge_tile, ])

# Update the overview dashboard

overview_db.update()
