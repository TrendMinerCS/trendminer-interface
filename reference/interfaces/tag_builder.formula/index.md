# `client.tag_builder.formula`

## trendminer_interface.\_client.tag_builder.formula.FormulaFacade

Bases: `WorkFacadeBase[Formula]`

Facade for getting saved formula objects

### define

```
define(
    formula: str,
    mapping: dict[str, Tag],
    units: str | None = None,
) -> FormulaDefinition
```

Define a new formula definition

Parameters:

| Name      | Type             | Description                                                                                                                                                                                                              | Default    |
| --------- | ---------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ---------- |
| `formula` | `str`            | The formula text                                                                                                                                                                                                         | *required* |
| `mapping` | `dict[str, Tag]` | The mapping of formula text variables to tags. All variables must be mapped. An empty dict should be provided in case the formula has no variables. The Tag.shift attributes will be taken into account for the mapping. | *required* |
| `units`   | `str`            | Units of resulting formula tags created from the definition                                                                                                                                                              | `None`     |

Returns:

| Type                | Description                  |
| ------------------- | ---------------------------- |
| `FormulaDefinition` | Resulting formula definition |

### create

```
create(
    definition: FormulaDefinition,
    name: str,
    description: str | None = None,
    folder: Folder | None = None,
) -> Formula
```

Create a new formula in TrendMiner

Parameters:

| Name          | Type                | Description                                              | Default                                     |
| ------------- | ------------------- | -------------------------------------------------------- | ------------------------------------------- |
| `definition`  | `FormulaDefinition` | Definition of the new formula                            | *required*                                  |
| `name`        | `str`               | Name of the saved formula. This will equal the tag name. | *required*                                  |
| `description` | \`str               | None\`                                                   | Description of the saved formula            |
| `folder`      | \`Folder            | None\`                                                   | The folder in which to save the new formula |

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
