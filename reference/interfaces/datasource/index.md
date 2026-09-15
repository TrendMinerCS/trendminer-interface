# `client.datasource`

## trendminer_interface.\_client.datasource.DatasourceFacade

Facade to retrieve tag datasource instances

### from_identifier

```
from_identifier(identifier: str) -> Datasource
```

Retrieve a datasource by its identifier

Parameters:

| Name         | Type  | Description           | Default    |
| ------------ | ----- | --------------------- | ---------- |
| `identifier` | `str` | Datasource identifier | *required* |

Returns:

| Type         | Description                             |
| ------------ | --------------------------------------- |
| `Datasource` | Datasource with the provided identifier |

Raises:

| Type               | Description                                        |
| ------------------ | -------------------------------------------------- |
| `ResourceNotFound` | If no datasource with the given identifier exists. |

### from_name

```
from_name(name: str) -> Datasource
```

Retrieve a datasource by its name

Parameters:

| Name   | Type  | Description     | Default    |
| ------ | ----- | --------------- | ---------- |
| `name` | `str` | Datasource name | *required* |

Returns:

| Type         | Description                       |
| ------------ | --------------------------------- |
| `Datasource` | Datasource with the provided name |

Raises:

| Type                | Description                                   |
| ------------------- | --------------------------------------------- |
| `ResourceNotFound`  | If no datasource with the given name exists.  |
| `AmbiguousResource` | If multiple datasources match the given name. |

Notes

This method will return the datasource with the provided name, regardless of whether it is a built-in datasource or not.

### get_builtin

```
get_builtin() -> list[Datasource]
```

Get all built-in datasources

Returns:

| Type               | Description                  |
| ------------------ | ---------------------------- |
| `list[Datasource]` | List of built-in datasources |

### search

```
search(
    name: str | None = None, page: int = 0, size: int = 1000
) -> PagedList[Datasource]
```

Search for non-builtin datasources matching the provided search conditions.

Parameters:

| Name   | Type  | Description                                                                                                                                                                      | Default |
| ------ | ----- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------- |
| `name` | `str` | Name search condition. Only datasources with a partial name match will be returned. Wildcard characters (\*) are NOT supported. If None (default), all datasources are returned. | `None`  |
| `page` | `int` | Page number of results to return. By default, start at the first page of results (0-indexed).                                                                                    | `0`     |
| `size` | `int` | Number of results to return per page.                                                                                                                                            | `1000`  |

Returns:

| Type                    | Description                                          |
| ----------------------- | ---------------------------------------------------- |
| `PagedList[Datasource]` | Page with datasources matching the search conditions |

Notes

To get built-in datasources, use the `get_builtin` method.
