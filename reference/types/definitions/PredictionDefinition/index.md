## trendminer_interface.objects.tag_builder.prediction.PredictionDefinition

Definition for a tag builder prediction

The prediction definition is the outcome of a workflow in TrendMiner. Most attributes cannot be directly edited by the user.

Attributes:

| Name    | Type          | Description                            |
| ------- | ------------- | -------------------------------------- |
| `units` | `str or None` | Units of the resulting prediction tag. |

### units

```
units = units
```

### formula

```
formula: str
```

The prediction formula

### target

```
target: Tag
```

The target tag predicted by linear regression

### mapping

```
mapping: dict[str, tuple[Tag, float]]
```

The linear regression formula variables mapping to a tag and its coefficient

### intercept

```
intercept: float
```

The linear regression intercept

### interval

```
interval: Interval
```

The interval on which the prediction was calculated

### accuracy

```
accuracy: float
```

The accuracy of the prediction (0-100) for the calculation interval

### calculated_at

```
calculated_at: Timestamp
```

The timestamp on which the prediction was calculated
