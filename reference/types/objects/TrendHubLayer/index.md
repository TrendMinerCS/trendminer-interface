## trendminer_interface.objects.TrendHubLayer

Configuration for a TrendHub layer

A layer itself does not directly specify a time interval. What time interval a layer refers to is determined by the properties (live, locked) of the TrendHub view it is attached to.

Attributes:

| Name                | Type        | Description                              |
| ------------------- | ----------- | ---------------------------------------- |
| `name`              | `str`       | Name of the layer, displayed in TrendHub |
| `hidden_references` | \`list\[Tag | Attribute\]\`                            |

### name

```
name: str = name
```

### hidden_references

```
hidden_references: list[Tag | Attribute] = hidden_references
```

### stored_interval

```
stored_interval: Interval
```

The interval as configured when the view was saved.

This is NOT the interval currently represented by the layer for live views. The stored interval does not update.

### base

```
base: bool
```

Whether the layer is a base layer or an additional layer

### line_style

```
line_style: LineStyle
```

The line style of the layer

### visible

```
visible: bool
```

Whether the layer is visible in the view
