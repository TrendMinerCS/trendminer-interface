# `client.tag_builder.imported`

## trendminer_interface.\_client.tag_builder.imported.TagImportFacade

Facade for creating new imported tags and retrieving existing imports

### create

```
create(
    name: str,
    data: Series,
    tag_type: ImportTagType,
    description: str | None = None,
    units: str | None = None,
) -> None
```

Import a new tag or overwrite an existing imported tag with the same name

Parameters:

| Name          | Type            | Description                                                                                                      | Default                             |
| ------------- | --------------- | ---------------------------------------------------------------------------------------------------------------- | ----------------------------------- |
| `name`        | `str`           | The name of the imported tag                                                                                     | *required*                          |
| `data`        | `Series`        | The time series data of the imported tag. Must have DatetimeIndex and a data dtype compatible with the tag type. | *required*                          |
| `tag_type`    | `ImportTagType` | The type of the imported tag                                                                                     | *required*                          |
| `description` | \`str           | None\`                                                                                                           | The description of the imported tag |
| `units`       | \`str           | None\`                                                                                                           | The units of the imported tag       |

Returns:

| Type   | Description |
| ------ | ----------- |
| `None` |             |

Notes

- The resulting tag will not be automatically indexed.
- If the DatetimeIndex is not timezone-aware, it will be assumed to be in the client timezone

### search

```
search(
    query: str | None = None,
    page: int = 0,
    size: int = 1000,
) -> PagedList[TagImport]
```

Search for tag imports

Parameters:

| Name    | Type  | Description                                                                                   | Default |
| ------- | ----- | --------------------------------------------------------------------------------------------- | ------- |
| `query` | `str` | Query for tag name or description. Wildcard character '\*' is supported.                      | `None`  |
| `page`  | `int` | Page number of results to return. By default, start at the first page of results (0-indexed). | `0`     |
| `size`  | `int` | Number of results to return per page.                                                         | `1000`  |

### from_name

```
from_name(name: str) -> TagImport
```

Get a tag import instance from its tag name

Parameters:

| Name   | Type  | Description                  | Default    |
| ------ | ----- | ---------------------------- | ---------- |
| `name` | `str` | The name of the imported tag | *required* |

Returns:

| Type        | Description |
| ----------- | ----------- |
| `TagImport` |             |

Raises:

| Type                | Description                                     |
| ------------------- | ----------------------------------------------- |
| `ResourceNotFound`  | If no imported tag with the given name exists.  |
| `AmbiguousResource` | If multiple imported tags match the given name. |
