# `client.tag.index_details`

## trendminer_interface.\_client.tag.index_details.IndexDetailsFacade

Facade to retrieve indexing details of tags

### from_name

```
from_name(
    name: str, datasource: Datasource | None = None
) -> IndexDetails
```

Get index details for a tag from its name.

Parameters:

| Name         | Type         | Description                                                                                             | Default    |
| ------------ | ------------ | ------------------------------------------------------------------------------------------------------- | ---------- |
| `name`       | `str`        | The name of the tag in TrendMiner.                                                                      | *required* |
| `datasource` | `Datasource` | The datasource of the tag. By default, the index details of any tag matching the name will be returned. | `None`     |

Returns:

| Type           | Description                                           |
| -------------- | ----------------------------------------------------- |
| `IndexDetails` | The index details for the tag with the provided name. |

Raises:

| Type                | Description                            |
| ------------------- | -------------------------------------- |
| `ResourceNotFound`  | If no tag with the given name exists.  |
| `AmbiguousResource` | If multiple tags match the given name. |

### search

```
search(
    name: str | None = None,
    statuses: list[IndexStatus] | None = None,
    datasources: list[Datasource] | None = None,
    delayed: bool | None = None,
    freq: Timedelta
    | tuple[Timedelta, Timedelta]
    | None = None,
    page: int = 0,
    size: int = 10000,
) -> PagedList[IndexDetails]
```

Search index details

Parameters:

| Name          | Type                                       | Description                                                                                                                                                                                                         | Default |
| ------------- | ------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------- |
| `name`        | `str`                                      | Tag name search query                                                                                                                                                                                               | `None`  |
| `statuses`    | `List[str]`                                | Options: "ok", "in progress", "out of date", "stale", "incomplete", "dormant"                                                                                                                                       | `None`  |
| `datasources` | `List[Datasource]`                         | Filter on specific datasources                                                                                                                                                                                      | `None`  |
| `delayed`     | `bool`                                     | Filter on only delayed or non-delayed indexes. A tag is considered delayed if its last index update is longer ago than 4 times the configured index update frequency.                                               | `None`  |
| `freq`        | `Timedelta or tuple[Timedelta, Timedelta]` | The configured index update frequency: - 2m as the monitor policy - 1h as a default policy - 24h for reduced policy When a tuple is given, the first value is considered the minimum, the second value the maximum. | `None`  |
| `page`        | `int`                                      | Page number of results to return. By default, start at the first page of results (0-indexed).                                                                                                                       | `0`     |
| `size`        | `int`                                      | Number of results to return per page.                                                                                                                                                                               | `10000` |

Returns:

| Type                      | Description                                                  |
| ------------------------- | ------------------------------------------------------------ |
| `PagedList[IndexDetails]` | Paginated list of index details matching the search criteria |

Notes

If no parameters are given, all index details are returned.
