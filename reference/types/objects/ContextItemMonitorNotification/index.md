## trendminer_interface.objects.ContextItemMonitorNotification

Context item monitor notification

Attributes:

| Name           | Type                                    | Description                                |
| -------------- | --------------------------------------- | ------------------------------------------ |
| `enabled`      | `bool`                                  | Whether the notification is enabled        |
| `context_type` | `(ContextType, optional)`               | The context item type                      |
| `component`    | `(Tag or Attribute or Asset, optional)` | The component the item will be attached to |
| `description`  | `str`                                   | The context item description               |
| `fields`       | `dict`                                  | The context item fields                    |
| `keywords`     | `list of str`                           | The keywords attached to the context item  |

### enabled

```
enabled: bool = enabled
```

### context_type

```
context_type: object | None = context_type
```

### component

```
component: Tag | Asset | Attribute | None = component
```

### description

```
description: str = description
```

### fields

```
fields: dict[str, str | float] = fields
```

### keywords

```
keywords: list[str] = keywords
```

### enabled_at

```
enabled_at: Timestamp | None
```

The timestamp the notification was enabled
