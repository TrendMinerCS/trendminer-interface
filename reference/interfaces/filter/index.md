# `client.filter`

## trendminer_interface.\_client.filter.FilterFacade

Bases: `WorkFacadeBase[Filter]`

Facade for getting saved filter objects

### define

```
define(
    condition: IntervalIndex | tuple[Search, bool],
) -> FilterDefinition
```

Define a new TrendHub Filter

Parameters:

| Name        | Type            | Description           | Default                                                                                                                                                                                                                                                  |
| ----------- | --------------- | --------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `condition` | \`IntervalIndex | tuple[Search, bool]\` | The filter condition. Either the intervals to be filtered out, or a tuple with the saved search on which to filter and whether to invert the search results (False: filter out search results; True: filter out everything that is not a search result). |

Returns:

| Type               | Description                              |
| ------------------ | ---------------------------------------- |
| `FilterDefinition` | Definition that can be passed to create. |

### create

```
create(
    definition: FilterDefinition,
    name: str,
    description: str | None = None,
    folder: Folder | None = None,
) -> Filter
```

Create a new filter in TrendMiner

Parameters:

| Name          | Type               | Description                                             | Default                                    |
| ------------- | ------------------ | ------------------------------------------------------- | ------------------------------------------ |
| `definition`  | `FilterDefinition` | Definition of the new filter                            | *required*                                 |
| `name`        | `str`              | Name of the saved filter. This will equal the tag name. | *required*                                 |
| `description` | \`str              | None\`                                                  | Description of the saved filter            |
| `folder`      | \`Folder           | None\`                                                  | The folder in which to save the new filter |

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
