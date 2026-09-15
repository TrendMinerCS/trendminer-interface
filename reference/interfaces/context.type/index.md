# `client.context.type`

## trendminer_interface.\_client.context.type.ContextTypeFacade

Facade for retrieving and creating context types

### create

```
create(
    key: str,
    name: str,
    workflow: ContextWorkflow | None,
    fields: list[ContextField],
    color: str = "#4A75E2",
    icon: ContextTypeIcon = "information",
    description: str | None = None,
    approvals_enabled: bool = False,
    audit_trail_enabled: bool = False,
) -> ContextType
```

Create a new context type

Parameters:

| Name                  | Type                 | Description                                                                                                                                                                                                                                                                                                            | Default         |
| --------------------- | -------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------- |
| `key`                 | `str`                | Unique key that is used as the identifier of the context type. Must be unique across all context types and cannot be changed after creation.                                                                                                                                                                           | *required*      |
| `name`                | `str`                | Name that is visible to the users in the appliance                                                                                                                                                                                                                                                                     | *required*      |
| `workflow`            | `ContextWorkflow`    | Workflow associated with the context type. When None, the context type can only have a single associated timestamp.                                                                                                                                                                                                    | *required*      |
| `fields`              | `list[ContextField]` | List of fields that are associated with the context type.                                                                                                                                                                                                                                                              | *required*      |
| `color`               | `str`                | Color of the context type in hex format (e.g. "#FF0000")                                                                                                                                                                                                                                                               | `"#4A75E2"`     |
| `icon`                | `ContextTypeIcon`    | Icon of the context type. Possible values are: "alert-circle", "arrows-round", "bucket", "circle-success", "clipboard", "cracked", "file-check", "flame", "flask", "flow-line", "information", "person", "ruler", "snowflake", "spoon", "trending-down", "warning", "waterdrops", "waves", "wheelbarrow", or "wrench". | `"information"` |
| `description`         | `str`                | Description of the context type                                                                                                                                                                                                                                                                                        | `None`          |
| `approvals_enabled`   | `bool`               | Whether context items of this type can be approved.                                                                                                                                                                                                                                                                    | `False`         |
| `audit_trail_enabled` | `bool`               | Whether context item edit history will be saved as metadata to the item.                                                                                                                                                                                                                                               | `False`         |

Returns:

| Type          | Description               |
| ------------- | ------------------------- |
| `ContextType` | The created context type. |

### from_key

```
from_key(key: str) -> ContextType
```

Get a context type by its key

Parameters:

| Name  | Type  | Description                         | Default    |
| ----- | ----- | ----------------------------------- | ---------- |
| `key` | `str` | Key of the context type to retrieve | *required* |

Returns:

| Type          | Description                     |
| ------------- | ------------------------------- |
| `ContextType` | Context type with the given key |

Raises:

| Type               | Description                                   |
| ------------------ | --------------------------------------------- |
| `ResourceNotFound` | If no context type with the given key exists. |

### from_name

```
from_name(name: str) -> ContextType
```

Get a context type by its name

Parameters:

| Name   | Type  | Description                          | Default    |
| ------ | ----- | ------------------------------------ | ---------- |
| `name` | `str` | Name of the context type to retrieve | *required* |

Returns:

| Type          | Description                      |
| ------------- | -------------------------------- |
| `ContextType` | Context type with the given name |

Raises:

| Type                | Description                                     |
| ------------------- | ----------------------------------------------- |
| `ResourceNotFound`  | If no context type with the given name exists.  |
| `AmbiguousResource` | If multiple context types match the given name. |

### search

```
search(
    key: str | None = None,
    name: str | None = None,
    page=0,
    size=2000,
) -> PagedList[ContextType]
```

Search for context types

Parameters:

| Name   | Type  | Description                                                                                   | Default |
| ------ | ----- | --------------------------------------------------------------------------------------------- | ------- |
| `key`  | `str` | Search for context types with keys matching this query. Can use the '\*' symbol as wildcard.  | `None`  |
| `name` | `str` | Search for context types with names matching this query. Can use the '\*' symbol as wildcard. | `None`  |
| `page` | `int` | Page number to start the search from (0-indexed). Default is 0.                               | `0`     |
| `size` | `int` | Number of results to return per page. Default is 2000 (the maximum supported by the backend). | `2000`  |

Returns:

| Type                     | Description                                           |
| ------------------------ | ----------------------------------------------------- |
| `PagedList[ContextType]` | Page with context types matching the search criteria. |
