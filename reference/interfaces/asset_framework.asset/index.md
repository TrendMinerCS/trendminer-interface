# `client.asset_framework.asset`

## trendminer_interface.\_client.asset_framework.asset.AssetFacade

Facade to retrieve and create TrendMiner asset instances

### create

```
create(
    name: str, parent: Asset, description: str | None = None
) -> Asset
```

Create a new asset in the asset framework

Parameters:

| Name          | Type    | Description                                                  | Default    |
| ------------- | ------- | ------------------------------------------------------------ | ---------- |
| `name`        | `str`   | Name of the asset                                            | *required* |
| `parent`      | `Asset` | Parent Asset under which the asset will be placed as a child | *required* |
| `description` | `str`   | Asset description                                            | `None`     |

Returns:

| Type    | Description         |
| ------- | ------------------- |
| `Asset` | Newly created asset |

Notes

The creation of a root asset (i.e., an asset without a parent) happens indirectly through the creation of an asset framework

### from_identifier

```
from_identifier(identifier: str) -> Asset
```

Get an asset from its UUID

Parameters:

| Name         | Type  | Description             | Default    |
| ------------ | ----- | ----------------------- | ---------- |
| `identifier` | `str` | Identifier of the asset | *required* |

Returns:

| Type    | Description                     |
| ------- | ------------------------------- |
| `Asset` | Asset with the given identifier |

Raises:

| Type               | Description                                   |
| ------------------ | --------------------------------------------- |
| `ResourceNotFound` | If no asset with the given identifier exists. |

### from_hex_path

```
from_hex_path(hex_path: str) -> Asset
```

Get an asset from its hex path

Parameters:

| Name       | Type  | Description                                                                                                                    | Default    |
| ---------- | ----- | ------------------------------------------------------------------------------------------------------------------------------ | ---------- |
| `hex_path` | `str` | Path of hexadecimal level identifiers of the asset, as available on Asset.hex_path. For example, "0000025e.0000025f.00000260". | *required* |

Returns:

| Type    | Description                                  |
| ------- | -------------------------------------------- |
| `Asset` | Asset corresponding to the provided hex path |

Raises:

| Type               | Description                                    |
| ------------------ | ---------------------------------------------- |
| `ResourceNotFound` | If no asset corresponds to the given hex path. |

### from_path

```
from_path(names: list[str]) -> Asset
```

Retrieve an asset from the asset framework by its path

Parameters:

| Name    | Type        | Description                                                                                                                              | Default    |
| ------- | ----------- | ---------------------------------------------------------------------------------------------------------------------------------------- | ---------- |
| `names` | `List[str]` | List of asset names, representing the path of the asset in the asset framework. For example, ["MyRootAsset", "MyAsset", "MyChildAsset"]. | *required* |

Returns:

| Type    | Description                              |
| ------- | ---------------------------------------- |
| `Asset` | Asset corresponding to the provided path |

Raises:

| Type                | Description                                |
| ------------------- | ------------------------------------------ |
| `ResourceNotFound`  | If no asset matches a segment of the path. |
| `AmbiguousResource` | If a path segment matches multiple assets. |

See Also

Asset.get_child_asset : Retrieve a single child asset by name and/or template. Asset.get_child_attribute : Retrieve a single child attribute by name and/or template.

### search

```
search(
    name: str | None = None,
    description: str | None = None,
    template: str | None = None,
    frameworks: list[AssetFramework] | None = None,
    ancestor: Asset | None = None,
    root_only=False,
    page: int = 0,
    size: int = 1000,
    resolve_tag_data: bool = False,
) -> PagedList[Asset]
```

Search Assets

Parameters:

| Name               | Type                   | Description                                                                                   | Default |
| ------------------ | ---------------------- | --------------------------------------------------------------------------------------------- | ------- |
| `name`             | `str`                  | Name search condition. Wildcard '\*' is supported.                                            | `None`  |
| `description`      | `str`                  | Description search condition. Wildcard '\*' is supported.                                     | `None`  |
| `template`         | `str`                  | Template search condition. Wildcard '\*' is supported.                                        | `None`  |
| `frameworks`       | `list[AssetFramework]` | Asset frameworks to search in. Searches in all asset frameworks by default.                   | `None`  |
| `ancestor`         | `Asset`                | If given, only returns assets that are (direct or indirect) descendants of the given asset    | `None`  |
| `root_only`        | `bool`                 | Whether to only return root assets (i.e., assets without a parent). False by default.         | `False` |
| `page`             | `int`                  | Page number of results to return. By default, start at the first page of results (0-indexed). | `0`     |
| `size`             | `int`                  | Number of results to return per page.                                                         | `1000`  |
| `resolve_tag_data` | `bool`                 | Whether to load tag data for attributes. Results in a much slower request.                    | `False` |

Returns:

| Type               | Description                                             |
| ------------------ | ------------------------------------------------------- |
| `PagedList[Asset]` | Paginated list of assets matching the search conditions |
