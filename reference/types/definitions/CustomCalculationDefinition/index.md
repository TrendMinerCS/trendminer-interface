## trendminer_interface.objects.tag_builder.custom_calculation.CustomCalculationDefinition

Definition for a tag builder custom calculation

Attributes:

| Name           | Type             | Description                                                               |
| -------------- | ---------------- | ------------------------------------------------------------------------- |
| `script`       | `str`            | The custom calculation Python script as a string.                         |
| `dependencies` | `list[Tag]`      | The dependency tags that are referenced in the custom calculation script. |
| `tag_type`     | `NumericTagType` | The type of the resulting custom calculation tag.                         |
| `units`        | `str or None`    | Units of the resulting custom calculation tag.                            |

### script

```
script: str = script
```

### dependencies

```
dependencies: list[Tag] = dependencies
```

### tag_type

```
tag_type: NumericTagType = tag_type
```

### units

```
units: str | None = units
```
