## trendminer_interface.objects.tag_builder.formula.FormulaDefinition

Definition for a tag builder formula

Attributes:

| Name      | Type             | Description                                                              |
| --------- | ---------------- | ------------------------------------------------------------------------ |
| `formula` | `str`            | The formula as a string, using the variable names defined in the mapping |
| `mapping` | `dict[str, Tag]` | Mapping of variable names used in the formula to Tag objects             |
| `units`   | `str or None`    | Units of the resulting formula tag.                                      |

### formula

```
formula: str = formula
```

### mapping

```
mapping: dict[str, Tag] = mapping
```

### units

```
units: str | None = units
```
