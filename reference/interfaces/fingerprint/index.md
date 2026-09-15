# `client.fingerprint`

## trendminer_interface.\_client.fingerprint.FingerprintFacade

Bases: `WorkFacadeBase[Fingerprint]`

Facade for getting saved fingerprint objects

### layer

```
layer: FingerprintLayerFacade
```

Facade for instantiating new fingerprint layers

### define

```
define(
    entries: list[Attribute | Tag],
    layers: list[FingerprintLayer],
) -> FingerprintDefinition
```

Create a fingerprint definition

Parameters:

| Name      | Type                     | Description                                                                                                                                                          | Default                                          |
| --------- | ------------------------ | -------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------ |
| `entries` | \`list\[Tag              | Attribute\]\`                                                                                                                                                        | List of time series entries for the fingerprint. |
| `layers`  | `list[FingerprintLayer]` | List of layers included in the fingerprint. Layers are expected to contain intervals of the same length. A single layer must have been configured as the base layer. | *required*                                       |

Returns:

| Type                    | Description                    |
| ----------------------- | ------------------------------ |
| `FingerprintDefinition` | The new fingerprint definition |

Raises:

| Type         | Description                                                                                              |
| ------------ | -------------------------------------------------------------------------------------------------------- |
| `ValueError` | If the layers do not contain exactly one base layer, or if the layers do not all have the same duration. |

### create

```
create(
    definition: FingerprintDefinition,
    name: str,
    description: str = "",
    folder: Folder | None = None,
) -> Fingerprint
```

Create a new fingerprint in TrendMiner

Parameters:

| Name          | Type                    | Description                                     | Default    |
| ------------- | ----------------------- | ----------------------------------------------- | ---------- |
| `definition`  | `FingerprintDefinition` | Definition of the new fingerprint               | *required* |
| `name`        | `str`                   | Name of the saved fingerprint                   | *required* |
| `description` | `str`                   | Description of the saved fingerprint            | `''`       |
| `folder`      | `Folder`                | The folder in which to save the new fingerprint | `None`     |

Returns:

| Type          | Description                                 |
| ------------- | ------------------------------------------- |
| `Fingerprint` | The saved fingerprint created in TrendMiner |

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
