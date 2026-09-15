# `client.dashboard`

## trendminer_interface.\_client.dashboard.DashboardFacade

Bases: `WorkFacadeBase[Dashboard]`

Facade for getting saved dashboard objects

### context

```
context: ContextHubViewTileFacade
```

Facade for creating ContextHub view tiles

### external

```
external: ExternalContentTileFacade
```

Facade for creating external content tiles

### gauge

```
gauge: GaugeTileFacade
```

Facade for creating gauge tiles

### monitor

```
monitor: MonitorTileFacade
```

Facade for creating monitor tiles

### notebook

```
notebook: NotebookTileFacade
```

Facade for creating notebook tiles

### text

```
text: TextTileFacade
```

Facade for creating text tiles

### trend

```
trend: TrendHubViewTileFacade
```

Facade for creating TrendHub view tiles

### value

```
value: CurrentValueTileFacade
```

Facade for creating current value tiles

### config

```
config(
    context: ContextHubViewTileConfiguration | None = None,
    external: ExternalContentTileConfiguration
    | None = None,
    gauge: GaugeTileConfiguration | None = None,
    monitor: MonitorTileConfiguration | None = None,
    notebook: NotebookTileConfiguration | None = None,
    text: TextTileConfiguration | None = None,
    trend: TrendHubViewTileConfiguration | None = None,
    value: CurrentValueTileConfiguration | None = None,
) -> DashboardConfiguration
```

Create a global dashboard configuration object

Can override settings for the different tile types. Takes the configurations of the different tile types as input. If a configuration is not provided, the default configuration of the respective tile factory is used.

Parameters:

| Name       | Type                               | Description                                     | Default |
| ---------- | ---------------------------------- | ----------------------------------------------- | ------- |
| `context`  | `ContextHubViewTileConfiguration`  | Global configuration for ContextHub view tiles  | `None`  |
| `external` | `ExternalContentTileConfiguration` | Global configuration for External content tiles | `None`  |
| `gauge`    | `GaugeTileConfiguration`           | Global configuration for Gauge tiles            | `None`  |
| `monitor`  | `MonitorTileConfiguration`         | Global configuration for Monitor tiles          | `None`  |
| `notebook` | `NotebookTileConfiguration`        | Global configuration for Notebook tiles         | `None`  |
| `text`     | `TextTileConfiguration`            | Global configuration for Text tiles             | `None`  |
| `trend`    | `TrendHubViewTileConfiguration`    | Global configuration for TrendHub view tiles    | `None`  |
| `value`    | `CurrentValueTileConfiguration`    | Global configuration for Current value tiles    | `None`  |

Returns:

| Type                     | Description |
| ------------------------ | ----------- |
| `DashboardConfiguration` |             |

### define

```
define(
    tiles: list[DashboardTile],
    live: bool = False,
    dynamic_font_sizing: bool = True,
    override_tile_config: bool = False,
    config: DashboardConfiguration | None = None,
    chart_aliases: dict[Tag | Attribute, str] | None = None,
) -> DashboardDefinition
```

Initialize a new dashboard

Parameters:

| Name                   | Type                     | Description                                                                                                                            | Default    |
| ---------------------- | ------------------------ | -------------------------------------------------------------------------------------------------------------------------------------- | ---------- |
| `tiles`                | `list[TileBase]`         | Tiles to add to the dashboard                                                                                                          | *required* |
| `live`                 | `bool`                   | Whether the dashboard will be updated live                                                                                             | `False`    |
| `dynamic_font_sizing`  | `bool`                   | Whether dynamic font sizing is enabled                                                                                                 | `True`     |
| `override_tile_config` | `bool`                   | Whether the dashboard configuration overrides individual tile settings                                                                 | `False`    |
| `config`               | `DashboardConfiguration` | Dashboard global configuration settings. Overrides tile settings when override_tile_config is True, otherwise does not have an effect. | `None`     |
| `chart_aliases`        | \`dict\[Tag              | Attribute, str\]                                                                                                                       | None\`     |

Returns:

| Type                  | Description |
| --------------------- | ----------- |
| `DashboardDefinition` |             |

Notes

The dashboard grid has a width of 24, but no length limit as dashboards are scrollable.

### create

```
create(
    definition: DashboardDefinition,
    name: str,
    description: str | None = None,
    folder: Folder | None = None,
) -> Dashboard
```

Create a new dashboard in TrendMiner

Parameters:

| Name          | Type                  | Description                     | Default                                       |
| ------------- | --------------------- | ------------------------------- | --------------------------------------------- |
| `definition`  | `DashboardDefinition` | Definition of the new dashboard | *required*                                    |
| `name`        | `str`                 | Name of the saved dashboard     | *required*                                    |
| `description` | \`str                 | None\`                          | Description of the saved dashboard            |
| `folder`      | \`Folder              | None\`                          | The folder in which to save the new dashboard |

### from_identifier

```
from_identifier(identifier: str) -> T
```

Get an item by its unique identifier

Parameters:

| Name         | Type  | Description                              | Default    |
| ------------ | ----- | ---------------------------------------- | ---------- |
| `identifier` | `str` | The unique identifier of the item to get | *required* |

Returns:

| Name   | Type | Description                    |
| ------ | ---- | ------------------------------ |
| `item` | `T`  | Item with the given identifier |

Raises:

| Type               | Description                                  |
| ------------------ | -------------------------------------------- |
| `ResourceNotFound` | If no item with the given identifier exists. |

### from_name

```
from_name(name: str, scope: WorkScope = 'my work') -> T
```

Get an item from its name

Parameters:

| Name    | Type  | Description                                                                                                                                                                                                                                                                                                                                              | Default     |
| ------- | ----- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------- |
| `name`  | `str` | The name of the item to get                                                                                                                                                                                                                                                                                                                              | *required*  |
| `scope` | `str` | Searching scope for getting the item. - 'my work': The authenticated user's work organizer (default) - 'shared': Another user's work shared to the authenticated user - 'favorites': The authenticated user's favorites, which can include items from own work and shared items. - 'system': Any user's work. Only accessible for system administrators. | `'my work'` |

Returns:

| Name   | Type | Description                  |
| ------ | ---- | ---------------------------- |
| `item` | `T`  | The item with the given name |

Raises:

| Type                | Description                                         |
| ------------------- | --------------------------------------------------- |
| `ResourceNotFound`  | If no item with the given name exists in the scope. |
| `AmbiguousResource` | If multiple items match the given name.             |

### search

```
search(
    query: str | None = None,
    scope: WorkScope = "my work",
    page: int = 0,
    size: int = 2000,
) -> PagedList[T]
```

Search items by name or description

Parameters:

| Name    | Type  | Description                                                                                                                                                                                                                                                                                                                         | Default     |
| ------- | ----- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------- |
| `query` | `str` | The search query. The '\*' can be used as a wildcard. Returns all items if query is None (default).                                                                                                                                                                                                                                 | `None`      |
| `scope` | `str` | Searching scope. - 'my work': The authenticated user's work organizer (default) - 'shared': Another user's work shared to the authenticated user - 'favorites': The authenticated user's favorites, which can include items from own work and shared items. - 'system': Any user's work. Only accessible for system administrators. | `'my work'` |
| `page`  | `int` | Page number of results to return. By default, start at the first page of results (0-indexed).                                                                                                                                                                                                                                       | `0`         |
| `size`  | `int` | Number of results to return per page.                                                                                                                                                                                                                                                                                               | `2000`      |

Returns:

| Name    | Type           | Description                                       |
| ------- | -------------- | ------------------------------------------------- |
| `items` | `PagedList[T]` | Paginated list of items matching the search query |
