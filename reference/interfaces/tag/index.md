# `client.tag`

## trendminer_interface.\_client.tag.TagFacade

Facade to retrieve and create TrendMiner tag instances

### index_details

```
index_details: IndexDetailsFacade
```

Get facade for retrieving indexing details of tags.

### from_identifier

```
from_identifier(identifier: str) -> Tag
```

Get a tag instance from its identifier.

Parameters:

| Name         | Type  | Description                        | Default    |
| ------------ | ----- | ---------------------------------- | ---------- |
| `identifier` | `str` | The UUID of the tag in TrendMiner. | *required* |

Returns:

| Type  | Description                                    |
| ----- | ---------------------------------------------- |
| `Tag` | The tag instance with the provided identifier. |

Raises:

| Type               | Description                                 |
| ------------------ | ------------------------------------------- |
| `ResourceNotFound` | If no tag with the given identifier exists. |

### from_name

```
from_name(
    name: str, datasource: Datasource | None = None
) -> Tag
```

Get a tag instance from its name.

Parameters:

| Name         | Type         | Description                                                                                                            | Default    |
| ------------ | ------------ | ---------------------------------------------------------------------------------------------------------------------- | ---------- |
| `name`       | `str`        | The name of the tag in TrendMiner.                                                                                     | *required* |
| `datasource` | `Datasource` | The datasource to which the tag belongs. By default, the tag with the given name from any datasource will be returned. | `None`     |

Returns:

| Type  | Description                              |
| ----- | ---------------------------------------- |
| `Tag` | The tag instance with the provided name. |

Raises:

| Type                | Description                            |
| ------------------- | -------------------------------------- |
| `ResourceNotFound`  | If no tag with the given name exists.  |
| `AmbiguousResource` | If multiple tags match the given name. |

### search

```
search(
    name: str | None = None,
    description: str | None = None,
    datasources: list[Datasource] | None = None,
    page: int = 0,
    size: int = 2000,
) -> PagedList[Tag]
```

Search tags

Parameters:

| Name          | Type               | Description                                                                                                                                                | Default |
| ------------- | ------------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------- | ------- |
| `name`        | `str`              | Tag name filter, can use '\*' as wildcard                                                                                                                  | `None`  |
| `description` | `str`              | Tag description filter, can use '\*' as wildcard                                                                                                           | `None`  |
| `datasources` | `List[Datasource]` | Datasources to which to limit the search. By default, all accessible datasources are searched.                                                             | `None`  |
| `page`        | `int`              | Page number of results to return. By default, start at the first page of results (0-indexed).                                                              | `0`     |
| `size`        | `int`              | Number of results to return per page. Default is set to 2000, which is the maximum size supported by the API. Set a smaller size for exploratory purposes. | `2000`  |

Returns:

| Type             | Description                                         |
| ---------------- | --------------------------------------------------- |
| `PagedList[Tag]` | Paginated list of tags matching the search criteria |
