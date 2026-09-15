# `client.context.field`

## trendminer_interface.\_client.context.field.ContextFieldFacade

Facade for retrieving and creating context fields

### create

```
create(
    key: str,
    name: str,
    field_type: ContextFieldType,
    placeholder: str = "",
    options: list[str] | None = None,
) -> ContextField
```

Create a new context field

Parameters:

| Name          | Type               | Description                                                                               | Default    |
| ------------- | ------------------ | ----------------------------------------------------------------------------------------- | ---------- |
| `key`         | `str`              | Key of the context field. Must be unique across all context fields.                       | *required* |
| `name`        | `str`              | Name of the context field. Does not have to be unique.                                    | *required* |
| `field_type`  | `ContextFieldType` | Type of the context field. Can be 'string', 'numeric', or 'enumeration'.                  | *required* |
| `placeholder` | `str`              | Placeholder text for the context field. Default is an empty string.                       | `""`       |
| `options`     | `list of str`      | Options for enumeration fields. Must be None for non-enumeration fields. Default is None. | `None`     |

Returns:

| Type           | Description                |
| -------------- | -------------------------- |
| `ContextField` | The created context field. |

### from_identifier

```
from_identifier(identifier: str) -> ContextField
```

Get a context field by its identifier

Parameters:

| Name         | Type  | Description                           | Default    |
| ------------ | ----- | ------------------------------------- | ---------- |
| `identifier` | `str` | UUID of the context field to retrieve | *required* |

Returns:

| Type           | Description                             |
| -------------- | --------------------------------------- |
| `ContextField` | Context field with the given identifier |

Raises:

| Type               | Description                                           |
| ------------------ | ----------------------------------------------------- |
| `ResourceNotFound` | If no context field with the given identifier exists. |

### from_key

```
from_key(key: str) -> ContextField
```

Get a context field by its key

Parameters:

| Name  | Type  | Description                          | Default    |
| ----- | ----- | ------------------------------------ | ---------- |
| `key` | `str` | Key of the context field to retrieve | *required* |

Returns:

| Type           | Description                      |
| -------------- | -------------------------------- |
| `ContextField` | Context field with the given key |

Raises:

| Type                | Description                                     |
| ------------------- | ----------------------------------------------- |
| `ResourceNotFound`  | If no context field with the given key exists.  |
| `AmbiguousResource` | If multiple context fields match the given key. |

### from_name

```
from_name(name: str) -> ContextField
```

Get a context field by its name

Parameters:

| Name   | Type  | Description                           | Default    |
| ------ | ----- | ------------------------------------- | ---------- |
| `name` | `str` | Name of the context field to retrieve | *required* |

Returns:

| Type           | Description                       |
| -------------- | --------------------------------- |
| `ContextField` | Context field with the given name |

Raises:

| Type                | Description                                      |
| ------------------- | ------------------------------------------------ |
| `ResourceNotFound`  | If no context field with the given name exists.  |
| `AmbiguousResource` | If multiple context fields match the given name. |

### search

```
search(
    key: str | None = None,
    name: str | None = None,
    page=0,
    size=2000,
) -> PagedList[ContextField]
```

Search for context fields

Parameters:

| Name   | Type  | Description                                                                                    | Default |
| ------ | ----- | ---------------------------------------------------------------------------------------------- | ------- |
| `key`  | `str` | Search for context fields with keys matching this query. Can use the '\*' symbol as wildcard.  | `None`  |
| `name` | `str` | Search for context fields with names matching this query. Can use the '\*' symbol as wildcard. | `None`  |
| `page` | `int` | Page number to start the search from (0-indexed). Default is 0.                                | `0`     |
| `size` | `int` | Number of results to return per page. Default is 2000 (the maximum supported by the backend).  | `2000`  |

Returns:

| Type                      | Description                                            |
| ------------------------- | ------------------------------------------------------ |
| `PagedList[ContextField]` | Page with context fields matching the search criteria. |
