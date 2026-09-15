# `client.asset_framework.attribute`

## trendminer_interface.\_client.asset_framework.attribute.AttributeFacade

Facade to retrieve and create TrendMiner attribute instances

### create

```
create(
    name: str,
    parent: Asset,
    tag: Tag,
    description: str | None = None,
) -> Attribute
```

Create a new attribute in the asset framework

Parameters:

| Name          | Type    | Description                                                      | Default    |
| ------------- | ------- | ---------------------------------------------------------------- | ---------- |
| `name`        | `str`   | Name of the attribute                                            | *required* |
| `parent`      | `Asset` | Parent Asset under which the attribute will be placed as a child | *required* |
| `tag`         | `Tag`   | Tag that the attribute refers to                                 | *required* |
| `description` | `str`   | Attribute description                                            | `None`     |

Returns:

| Type        | Description             |
| ----------- | ----------------------- |
| `Attribute` | Newly created attribute |

### from_identifier

```
from_identifier(identifier: str) -> Attribute
```

Get an attribute from its UUID

Parameters:

| Name         | Type  | Description                 | Default    |
| ------------ | ----- | --------------------------- | ---------- |
| `identifier` | `str` | Identifier of the attribute | *required* |

Returns:

| Type        | Description                         |
| ----------- | ----------------------------------- |
| `Attribute` | Attribute with the given identifier |

Raises:

| Type               | Description                                       |
| ------------------ | ------------------------------------------------- |
| `ResourceNotFound` | If no attribute with the given identifier exists. |

### search

```
search(
    name: str | None = None,
    description: str | None = None,
    template: str | None = None,
    frameworks: list[AssetFramework] | None = None,
    ancestor: Asset | None = None,
    page: int = 0,
    size: int = 1000,
    resolve_tag_data: bool = False,
) -> PagedList[Attribute]
```

Search Attributes

Parameters:

| Name               | Type                   | Description                                                                                     | Default |
| ------------------ | ---------------------- | ----------------------------------------------------------------------------------------------- | ------- |
| `name`             | `str`                  | Name search condition. Wildcard '\*' is supported.                                              | `None`  |
| `description`      | `str`                  | Description search condition. Wildcard '\*' is supported.                                       | `None`  |
| `template`         | `str`                  | Template search condition. Wildcard '\*' is supported.                                          | `None`  |
| `frameworks`       | `list[AssetFramework]` | Asset frameworks to search in. Searches all frameworks by default.                              | `None`  |
| `ancestor`         | `Asset`                | If given, only returns attributes that are (direct or indirect) descendants of the given asset. | `None`  |
| `page`             | `int`                  | Page number of results to return. By default, start at the first page of results (0-indexed).   | `0`     |
| `size`             | `int`                  | Number of results to return per page.                                                           | `1000`  |
| `resolve_tag_data` | `bool`                 | Whether to load tag data for attributes. Results in a much slower request.                      | `False` |

Returns:

| Type                   | Description                                                 |
| ---------------------- | ----------------------------------------------------------- |
| `PagedList[Attribute]` | Paginated list of attributes matching the search conditions |
