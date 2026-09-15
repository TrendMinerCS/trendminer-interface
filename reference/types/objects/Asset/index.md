## trendminer_interface.objects.Asset

Bases: `NodeBase`

Asset node in the asset framework

Attributes:

| Name          | Type    | Description              |
| ------------- | ------- | ------------------------ |
| `name`        | `str`   | Name of the asset        |
| `description` | `str`   | Description of the asset |
| `parent`      | \`Asset | None\`                   |

### name

```
name: str = name
```

### description

```
description: str = description
```

### parent

```
parent: Asset | None = parent
```

### identifier

```
identifier: str
```

Unique UUID.

### source

```
source: AssetFramework
```

Source asset framework.

### template

```
template: str | None
```

Asset framework template, if any.

### hex_path

```
hex_path: str
```

Path of hexadecimal level identifiers of the node

The path contains the hexadecimal identifier of every level in the asset framework, from the root asset down to the node itself, joined by dots (e.g., "0000025e.0000025f.00000260"). The hex path of a node is therefore always prefixed by the hex path of its parent. TrendMiner references asset framework nodes by this path rather than by UUID in several parts of its API, such as access rules and node creation.

Notes

The format of the individual segments is determined by TrendMiner and should be treated as opaque. Use the hex path as a whole, or compare it to the hex path of another node in the same asset framework.

For assets and attributes referenced by a context item of which the underlying node no longer exists in the asset framework, the path is the placeholder "deleted-asset" or "deleted-attribute", consistent with the behavior of `identifier`.

Raises:

| Type              | Description                                                                       |
| ----------------- | --------------------------------------------------------------------------------- |
| `PermissionError` | If the user has no permission for the node, and can therefore not access its path |
| `ValueError`      | If the node is an attribute of which the parent asset no longer exists            |

### get_access_rules

```
get_access_rules() -> list[AssetAccessRule]
```

Get access rules for the node

Returns:

| Type                      | Description                                       |
| ------------------------- | ------------------------------------------------- |
| `list of AssetAccessRule` | List of all access rules set directly on the node |

### get_inherited_access_rules

```
get_inherited_access_rules() -> list[AssetAccessRule]
```

Get inherited access rules for the node

Returns:

| Type                      | Description                                                                 |
| ------------------------- | --------------------------------------------------------------------------- |
| `list of AssetAccessRule` | List of all access rules inherited from parent nodes in the asset framework |

### add_access_rule

```
add_access_rule(
    subject: User | UserGroup,
    permission: AssetAccessPermission,
) -> AssetAccessRule
```

Add an access rule to the node

Parameters:

| Name         | Type                         | Description                                                                                                                                                                                                                                                                             | Default    |
| ------------ | ---------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------- |
| `subject`    | `User or UserGroup`          | The user or user group who is granted the permissions                                                                                                                                                                                                                                   | *required* |
| `permission` | `('read', 'browse', 'none')` | Access permission to be added for the subject. - "read": allows reading context items of the asset/attribute, and thus also browsing. - "browse": allows browsing the asset/attribute, but not reading context items. - "none": explicit denial of permissions for the asset/attribute. | `"read"`   |

Returns:

| Type              | Description             |
| ----------------- | ----------------------- |
| `AssetAccessRule` | The created access rule |

### search_children

```
search_children(
    name: str | None = None,
    description: str | None = None,
    template: str | None = None,
    child_type: None = None,
    page: int = 0,
    size: int = 1000,
) -> PagedList[Asset | Attribute]
```

```
search_children(
    name: str | None = None,
    description: str | None = None,
    template: str | None = None,
    child_type: type[Attribute] = ...,
    page: int = 0,
    size: int = 1000,
) -> PagedList[Attribute]
```

```
search_children(
    name: str | None = None,
    description: str | None = None,
    template: str | None = None,
    child_type: type[Asset] = ...,
    page: int = 0,
    size: int = 1000,
) -> PagedList[Asset]
```

```
search_children(
    name: str | None = None,
    description: str | None = None,
    template: str | None = None,
    child_type: type[Asset] | type[Attribute] | None = None,
    page: int = 0,
    size: int = 1000,
) -> (
    PagedList[Asset]
    | PagedList[Attribute]
    | PagedList[Asset | Attribute]
)
```

Get direct children of the asset in the asset framework

Parameters:

| Name          | Type          | Description                                                                                   | Default                                                                                  |
| ------------- | ------------- | --------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------- |
| `name`        | \`str         | None\`                                                                                        | Name of the child asset or attribute to filter for.                                      |
| `description` | \`str         | None\`                                                                                        | Description of the child asset or attribute to filter for.                               |
| `template`    | \`str         | None\`                                                                                        | Template name to filter for. Only children based on the given template will be returned. |
| `child_type`  | \`type[Asset] | type[Attribute]                                                                               | None\`                                                                                   |
| `page`        | `int`         | Page number of results to return. By default, start at the first page of results (0-indexed). | `0`                                                                                      |
| `size`        | `int`         | Number of results to return per page.                                                         | `1000`                                                                                   |

Returns:

| Type               | Description   |
| ------------------ | ------------- |
| \`PagedList\[Asset | Attribute\]\` |

Notes

Calling this method without any parameters will return all direct children of the asset.

### get_child_attribute

```
get_child_attribute(
    name: str | None = None, template: str | None = None
) -> Attribute
```

Get a child attribute of the asset by name

At least one of name or template must be provided to identify the attribute.

Parameters:

| Name       | Type  | Description                            | Default |
| ---------- | ----- | -------------------------------------- | ------- |
| `name`     | `str` | Name of the child attribute to get     | `None`  |
| `template` | `str` | Template of the child attribute to get | `None`  |

Returns:

| Type        | Description                                         |
| ----------- | --------------------------------------------------- |
| `Attribute` | Child attribute with the given name and/or template |

Raises:

| Type                | Description                                                        |
| ------------------- | ------------------------------------------------------------------ |
| `ResourceNotFound`  | If no child attribute matches the given name and/or template.      |
| `AmbiguousResource` | If multiple child attributes match the given name and/or template. |

### get_child_asset

```
get_child_asset(
    name: str | None = None, template: str | None = None
) -> Asset
```

Get a child asset of the asset by name

At least one of name or template must be provided to identify the asset.

Parameters:

| Name       | Type  | Description                        | Default |
| ---------- | ----- | ---------------------------------- | ------- |
| `name`     | `str` | Name of the child asset to get     | `None`  |
| `template` | `str` | Template of the child asset to get | `None`  |

Returns:

| Type    | Description                                     |
| ------- | ----------------------------------------------- |
| `Asset` | Child asset with the given name and/or template |

Raises:

| Type                | Description                                                    |
| ------------------- | -------------------------------------------------------------- |
| `ResourceNotFound`  | If no child asset matches the given name and/or template.      |
| `AmbiguousResource` | If multiple child assets match the given name and/or template. |

### update

```
update() -> Asset
```

Update the asset in TrendMiner to the instance state.

Returns:

| Type    | Description                                                              |
| ------- | ------------------------------------------------------------------------ |
| `Asset` | Updated asset instance reflecting the state in TrendMiner after updating |

### delete

```
delete() -> None
```

Delete the current asset from the asset framework

Notes

Child assets and attributes will not be deleted, but moved up one level in the asset tree.

### get_hierarchy

```
get_hierarchy() -> list[Asset]
```

Get hierarchy from the root asset down to the current asset

Returns:

| Type          | Description     |
| ------------- | --------------- |
| `list[Asset]` | Asset hierarchy |
