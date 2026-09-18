# `client.trend.view`

## trendminer_interface.\_client.trend.view.TrendHubViewFacade

Bases: `WorkFacadeBase[TrendHubView]`

Facade for getting saved trend hub view objects

### define

```
define(
    entries: Sequence[Tag | Attribute | TrendHubEntryGroup],
    layers: Sequence[TrendHubLayer],
    context_interval: Interval,
    chart_properties: ChartProperties | None = None,
    live: bool = False,
    filter_entries: Sequence[tuple[Filter, bool]]
    | None = None,
    fingerprint_entries: Sequence[
        tuple[Fingerprint, bool, Interval]
    ]
    | None = None,
) -> TrendHubViewDefinition
```

Define a new TrendHub view

Parameters:

| Name                  | Type                                       | Description                                                                                                                                               | Default                |
| --------------------- | ------------------------------------------ | --------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------- |
| `entries`             | \`list\[Tag                                | Attribute                                                                                                                                                 | TrendHubEntryGroup\]\` |
| `layers`              | `list[TrendHubLayer]`                      | List of layers to show in the view. Layers are expected to have intervals of the same length. A single layer must have been configured as the base layer. | *required*             |
| `context_interval`    | `Interval`                                 | Context interval for the view.                                                                                                                            | *required*             |
| `chart_properties`    | `ChartProperties`                          | View chart configuration. Defaults to standard stacked plot representation.                                                                               | `None`                 |
| `live`                | `bool`                                     | Whether the view base layer should always update to end at the current time.                                                                              | `False`                |
| `filter_entries`      | `list[tuple[Filter, bool]]`                | List of filters included in the view, with their active state                                                                                             | `None`                 |
| `fingerprint_entries` | `list[tuple[Fingerprint, bool, Interval]]` | List of fingerprints included in the view, with their active state and interval to which they apply                                                       | `None`                 |

Returns:

| Type                     | Description |
| ------------------------ | ----------- |
| `TrendHubViewDefinition` |             |

Raises:

| Type         | Description                                            |
| ------------ | ------------------------------------------------------ |
| `ValueError` | If the input layers do not all have the same duration. |

Notes

Statistics and layer comparison table formats are currently not configurable

### create

```
create(
    definition: TrendHubViewDefinition,
    name: str,
    description: str | None = None,
    folder: Folder | None = None,
) -> TrendHubView
```

Create a new TrendHub view in TrendMiner

Parameters:

| Name          | Type                     | Description                         | Default                                  |
| ------------- | ------------------------ | ----------------------------------- | ---------------------------------------- |
| `definition`  | `TrendHubViewDefinition` | Definition of the new TrendHub view | *required*                               |
| `name`        | `str`                    | Name of the saved view              | *required*                               |
| `description` | \`str                    | None\`                              | Description of the saved view            |
| `folder`      | \`Folder                 | None\`                              | The folder in which to save the new view |

Returns:

| Type           | Description                           |
| -------------- | ------------------------------------- |
| `TrendHubView` | The saved view created in TrendMiner. |

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
