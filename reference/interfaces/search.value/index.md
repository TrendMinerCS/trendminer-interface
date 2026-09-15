# `client.search.value`

## trendminer_interface.\_client.search.value.ValueBasedSearchFacade

Bases: `WorkFacadeBase[ValueBasedSearch]`

Facade for getting saved value based search objects

### define

```
define(
    queries: list[ValueBasedSearchQuery],
    calculations: dict[str, SearchCalculation]
    | None = None,
    duration=Timedelta(minutes=2),
    mode: ValueBasedSearchMode = "and",
) -> ValueBasedSearchDefinition
```

Define a new value based search

Parameters:

| Name           | Type                           | Description                                                                                                      | Default                |
| -------------- | ------------------------------ | ---------------------------------------------------------------------------------------------------------------- | ---------------------- |
| `queries`      | `list[ValueBasedSearchQuery]`  | List of queries to include in the search. Each query is a (Tag, operator, value) tuple.                          | *required*             |
| `calculations` | `dict[str, SearchCalculation]` | Dictionary of calculations to include in the search, by default None                                             | `None`                 |
| `duration`     | `Timedelta`                    | Duration of the search, by default 2 minutes                                                                     | `Timedelta(minutes=2)` |
| `mode`         | `('and', 'or')`                | How to combine multiple queries: "and" requires all queries to match simultaneously, "or" requires at least one. | `"and"`                |

Returns:

| Type                         | Description                            |
| ---------------------------- | -------------------------------------- |
| `ValueBasedSearchDefinition` | The new value based search definition. |

Examples:

```
>>> definition = client.search.value.define(
...     queries=[(tag, ">", 100.0), (other_tag, "=", "running")],
...     mode="and",
... )
```

### create

```
create(
    definition: ValueBasedSearchDefinition,
    name: str,
    description: str | None = None,
    folder: Folder | None = None,
) -> ValueBasedSearch
```

Create a new value-based search in TrendMiner

Parameters:

| Name          | Type                         | Description                              | Default                                    |
| ------------- | ---------------------------- | ---------------------------------------- | ------------------------------------------ |
| `definition`  | `ValueBasedSearchDefinition` | Definition of the new value-based search | *required*                                 |
| `name`        | `str`                        | Name of the saved search                 | *required*                                 |
| `description` | \`str                        | None\`                                   | Description of the saved search            |
| `folder`      | \`Folder                     | None\`                                   | The folder in which to save the new search |

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
