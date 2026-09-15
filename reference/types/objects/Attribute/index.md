## trendminer_interface.objects.Attribute

Bases: `NodeBase`

Attribute node in the asset framework

Attributes:

| Name          | Type                          | Description                                                                                                                                                                                                                       |
| ------------- | ----------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `name`        | `str`                         | Name of the attribute                                                                                                                                                                                                             |
| `tag`         | \`Tag                         | None\`                                                                                                                                                                                                                            |
| `description` | `str`                         | Description of the attribute                                                                                                                                                                                                      |
| `parent`      | `Asset`                       | Parent asset of the attribute.                                                                                                                                                                                                    |
| `shift`       | `Timedelta`                   | Time shift of the attribute. Only relevant for visualization in TrendHub views. By default, attributes will have a shift of 0.                                                                                                    |
| `visible`     | `bool`                        | Whether the tag is visible in TrendHub. This is used for visualization purposes in TrendHub, and has an impact on fingerprints. Attributes retrieved from anywhere but a TrendHub view or Fingerprint will be visible by default. |
| `color`       | `str`                         | The color of the attribute, as a hex color code (e.g., "#FF0000" for red). This is used for visualization purposes in TrendHub.                                                                                                   |
| `scale`       | `tuple[float, float] or None` | The manually set scale of the attribute, as a tuple of (min, max) values, as used in TrendHub visualization. If no manual scale is set (None), the attribute will be autoscaled.                                                  |
| `alias`       | `str or None`                 | The alias of the attribute, as set in TrendHub.                                                                                                                                                                                   |
| `accuracy`    | \`float                       | None\`                                                                                                                                                                                                                            |

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

### tag

```
tag: Tag | None = tag
```

### shift

```
shift: Timedelta = shift
```

### visible

```
visible: bool = visible
```

### color

```
color: str = color
```

### scale

```
scale: tuple[float, float] | None = scale
```

### alias

```
alias: str | None = alias
```

### accuracy

```
accuracy: float | None = accuracy
```

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

### update

```
update() -> Attribute
```

Update the attribute in TrendMiner to the instance state.

Returns:

| Type        | Description                                                                |
| ----------- | -------------------------------------------------------------------------- |
| `Attribute` | Updated attribute instance reflecting the state in TrendMiner after saving |

### delete

```
delete() -> None
```

Delete the current attribute from the asset framework
