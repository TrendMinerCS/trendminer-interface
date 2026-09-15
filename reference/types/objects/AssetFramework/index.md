## trendminer_interface.objects.AssetFramework

Asset framework definition

Attributes:

| Name        | Type   | Description                                                                                               |
| ----------- | ------ | --------------------------------------------------------------------------------------------------------- |
| `name`      | `str`  | Name of the asset framework                                                                               |
| `published` | `bool` | Whether the asset framework is published or not. Unpublished asset frameworks are only visible to admins. |

### name

```
name: str = name
```

### published

```
published: bool = published
```

### identifier

```
identifier: str
```

UUID of the asset framework

### framework_type

```
framework_type: AssetFrameworkType
```

Type of the asset framework: "csv" or "datasource".

### synced_at

```
synced_at: Timestamp | None
```

Timestamp of the last synchronization of the asset framework

### get_root_asset

```
get_root_asset() -> Asset
```

Get the root asset of the asset framework

Returns:

| Name         | Type    | Description                       |
| ------------ | ------- | --------------------------------- |
| `root_asset` | `Asset` | Root asset of the asset framework |

### delete

```
delete() -> None
```

Delete the asset framework
