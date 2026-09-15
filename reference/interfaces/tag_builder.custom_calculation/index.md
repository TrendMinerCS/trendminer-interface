# `client.tag_builder.custom_calculation`

## trendminer_interface.\_client.tag_builder.custom_calculation.CustomCalculationFacade

Bases: `WorkFacadeBase[CustomCalculation]`

Facade for getting saved custom calculation objects

### define

```
define(
    script: str,
    dependencies: list[Tag] | None = None,
    tag_type: NumericTagType = "analog",
    units: str | None = None,
) -> CustomCalculationDefinition
```

Define a new custom calculation definition

Parameters:

| Name           | Type             | Description                                                                                         | Default                                       |
| -------------- | ---------------- | --------------------------------------------------------------------------------------------------- | --------------------------------------------- |
| `script`       | `str`            | The Python script for the custom calculation                                                        | *required*                                    |
| `dependencies` | `list[Tag]`      | The tags the custom calculation is dependent on. The indexes of these tags will be kept up to date. | `None`                                        |
| `tag_type`     | `NumericTagType` | Custom calculation tag type                                                                         | `'analog'`                                    |
| `units`        | \`str            | None\`                                                                                              | Units of the resulting custom calculation tag |

Returns:

| Type                          | Description                             |
| ----------------------------- | --------------------------------------- |
| `CustomCalculationDefinition` | Resulting custom calculation definition |

### create

```
create(
    definition: CustomCalculationDefinition,
    name: str,
    description: str | None = None,
    folder: Folder | None = None,
) -> CustomCalculation
```

Create a new custom calculation in TrendMiner

Parameters:

| Name          | Type                          | Description                                                         | Default                                                |
| ------------- | ----------------------------- | ------------------------------------------------------------------- | ------------------------------------------------------ |
| `definition`  | `CustomCalculationDefinition` | Definition of the new custom calculation                            | *required*                                             |
| `name`        | `str`                         | Name of the saved custom calculation. This will equal the tag name. | *required*                                             |
| `description` | \`str                         | None\`                                                              | Description of the saved custom calculation            |
| `folder`      | \`Folder                      | None\`                                                              | The folder in which to save the new custom calculation |

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
