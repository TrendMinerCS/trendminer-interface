## trendminer_interface.objects.ContextType

Configuration of a context type

Attributes:

| Name                  | Type                          | Description                                                                                                                                                                                                                                                                                                            |
| --------------------- | ----------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `name`                | `str`                         | Name that is visible to the users in the appliance                                                                                                                                                                                                                                                                     |
| `description`         | `(str, optional)`             | Description of the context type                                                                                                                                                                                                                                                                                        |
| `workflow`            | `(ContextWorkflow, optional)` | Workflow associated with the context type. When None, the context type can only have a single associated timestamp.                                                                                                                                                                                                    |
| `fields`              | `list of ContextField`        | List of fields that are associated with the context type.                                                                                                                                                                                                                                                              |
| `color`               | `str`                         | Color of the context type in hex format (e.g. "#FF0000")                                                                                                                                                                                                                                                               |
| `icon`                | `ContextTypeIcon`             | Icon of the context type. Possible values are: "alert-circle", "arrows-round", "bucket", "circle-success", "clipboard", "cracked", "file-check", "flame", "flask", "flow-line", "information", "person", "ruler", "snowflake", "spoon", "trending-down", "warning", "waterdrops", "waves", "wheelbarrow", or "wrench". |
| `approvals_enabled`   | `bool`                        | Whether context items of this type can be approved.                                                                                                                                                                                                                                                                    |
| `audit_trail_enabled` | `bool`                        | Whether context item edit history will be saved as metadata to the item.                                                                                                                                                                                                                                               |

### name

```
name: str = name
```

### workflow

```
workflow: ContextWorkflow | None = workflow
```

### fields

```
fields: list[ContextField] = fields
```

### color

```
color: str = color
```

### icon

```
icon: ContextTypeIcon = icon
```

### description

```
description: str | None = description
```

### approvals_enabled

```
approvals_enabled: bool = approvals_enabled
```

### audit_trail_enabled

```
audit_trail_enabled: bool = audit_trail_enabled
```

### key

```
key: str
```

Unique key that is used as the identifier of the context type

### update

```
update() -> ContextType
```

Update the appliance context type to the current instance configuration

Returns:

| Type          | Description          |
| ------------- | -------------------- |
| `ContextType` | Updated context type |

### delete

```
delete() -> None
```

Permanently delete the context type
