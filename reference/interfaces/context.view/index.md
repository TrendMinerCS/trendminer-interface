# `client.context.view`

## trendminer_interface.\_client.context.view.ContextHubViewFacade

Bases: `WorkFacadeBase[ContextHubView]`

Facade for getting saved context hub view objects

### define

```
define(
    filters: list[ContextFilter],
    calculations: dict[str, SearchCalculation]
    | None = None,
    view_type: ContextHubViewType = "grid",
) -> ContextHubViewDefinition
```

Define a new ContextHub view

Parameters:

| Name           | Type                           | Description                                       | Default                                                                |
| -------------- | ------------------------------ | ------------------------------------------------- | ---------------------------------------------------------------------- |
| `filters`      | `list[ContextFilter]`          | Filters to apply to the context items             | *required*                                                             |
| `calculations` | \`dict[str, SearchCalculation] | None\`                                            | Calculations to apply to the context items when getting search results |
| `view_type`    | `ContextHubViewType`           | The type of view to create (grid, gantt, scatter) | `'grid'`                                                               |

Returns:

| Type                       | Description                           |
| -------------------------- | ------------------------------------- |
| `ContextHubViewDefinition` | The definition of the ContextHub view |

### create

```
create(
    definition: ContextHubViewDefinition,
    name: str,
    description: str | None = None,
    folder: Folder | None = None,
) -> ContextHubView
```

Create a new ContextHub view in TrendMiner

Parameters:

| Name          | Type                       | Description                           | Default                                  |
| ------------- | -------------------------- | ------------------------------------- | ---------------------------------------- |
| `definition`  | `ContextHubViewDefinition` | Definition of the new ContextHub view | *required*                               |
| `name`        | `str`                      | Name of the saved view                | *required*                               |
| `description` | \`str                      | None\`                                | Description of the saved view            |
| `folder`      | \`Folder                   | None\`                                | The folder in which to save the new view |

Returns:

| Type             | Description                            |
| ---------------- | -------------------------------------- |
| `ContextHubView` | The created and saved ContextHub view. |

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
