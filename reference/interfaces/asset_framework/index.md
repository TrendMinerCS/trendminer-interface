# `client.asset_framework`

## trendminer_interface.\_client.asset_framework.AssetFrameworkFacade

Facade to retrieve and create TrendMiner asset framework instances

### asset

```
asset: AssetFacade
```

Facade for retrieving and creating assets in the asset framework

### attribute

```
attribute: AttributeFacade
```

Facade for retrieving and creating attributes in the asset framework

### create

```
create(
    name: str, published: bool = False
) -> AssetFramework
```

Create a new asset framework

Parameters:

| Name        | Type   | Description                                                              | Default    |
| ----------- | ------ | ------------------------------------------------------------------------ | ---------- |
| `name`      | `str`  | Name of the asset framework                                              | *required* |
| `published` | `bool` | Whether the asset framework should be published or not, by default False | `False`    |

Returns:

| Type             | Description                 |
| ---------------- | --------------------------- |
| `AssetFramework` | The created asset framework |

### search

```
search(
    name: str | None = None,
    published: bool | None = None,
    framework_type: AssetFrameworkType | None = None,
    page: int = 0,
    size: int = 500,
) -> PagedList[AssetFramework]
```

Search for asset frameworks matching the given criteria

Calling this method without parameters will return all asset frameworks the authenticated user has access to.

Parameters:

| Name             | Type                 | Description                                                                                   | Default                                                                     |
| ---------------- | -------------------- | --------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------- |
| `name`           | `str`                | Filter on (partial) name of the asset framework. Wildcard character * is supported.           | `None`                                                                      |
| `published`      | `bool`               | Filter on published status of the asset framework.                                            | `None`                                                                      |
| `framework_type` | \`AssetFrameworkType | None\`                                                                                        | Filter on the type of the asset framework. Should be "csv" or "datasource". |
| `page`           | `int`                | Page number of results to return. By default, start at the first page of results (0-indexed). | `0`                                                                         |
| `size`           | `int`                | Number of results to return per page.                                                         | `500`                                                                       |

Returns:

| Type                        | Description                                                     |
| --------------------------- | --------------------------------------------------------------- |
| `PagedList[AssetFramework]` | Paginated list of asset frameworks matching the search criteria |

Notes

Asset frameworks to which the user has no permissions are also returned by the API. These are filtered out before returning to the user, with the downside that the `total_elements` results is unavailable (`None`) and pages may not contain the number of results requested.

### from_identifier

```
from_identifier(identifier: str) -> AssetFramework
```

Get an asset framework by its identifier

Parameters:

| Name         | Type  | Description                 | Default    |
| ------------ | ----- | --------------------------- | ---------- |
| `identifier` | `str` | UUID of the asset framework | *required* |

Returns:

| Type             | Description                                   |
| ---------------- | --------------------------------------------- |
| `AssetFramework` | The asset framework with the given identifier |

Raises:

| Type               | Description                                             |
| ------------------ | ------------------------------------------------------- |
| `ResourceNotFound` | If no asset framework with the given identifier exists. |

### from_name

```
from_name(
    name: str,
    published: bool | None = None,
    framework_type: AssetFrameworkType | None = None,
) -> AssetFramework
```

Get an asset framework by its name

Parameters:

| Name             | Type   | Description                                                                                   | Default    |
| ---------------- | ------ | --------------------------------------------------------------------------------------------- | ---------- |
| `name`           | `str`  | Name of the asset framework                                                                   | *required* |
| `published`      | `bool` | Only retrieve asset framework with the given published status.                                | `None`     |
| `framework_type` | `str`  | Only retrieve asset framework with the given framework type. Should be "csv" or "datasource". | `None`     |

Returns:

| Type             | Description                             |
| ---------------- | --------------------------------------- |
| `AssetFramework` | The asset framework with the given name |

Raises:

| Type                | Description                                        |
| ------------------- | -------------------------------------------------- |
| `ResourceNotFound`  | If no asset framework with the given name exists.  |
| `AmbiguousResource` | If multiple asset frameworks match the given name. |
