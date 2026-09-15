## trendminer_interface.objects.tag_builder.aggregation.AggregationDefinition

Definition for tag builder aggregation

Attributes:

| Name       | Type                     | Description                                 |
| ---------- | ------------------------ | ------------------------------------------- |
| `target`   | `Tag`                    | The tag that is aggregated                  |
| `method`   | `TagAggregationMethod`   | Method by which to aggregate the target tag |
| `position` | `TagAggregationPosition` | Position on which to aggregate the tag      |
| `window`   | `Timedelta`              | Aggregation window                          |
| `units`    | `str or None`            | Units of the resulting aggregation tag.     |

### target

```
target: Tag = target
```

### method

```
method: TagAggregationMethod = method
```

### position

```
position: TagAggregationPosition = position
```

### window

```
window: Timedelta = window
```

### units

```
units: str | None = units
```
