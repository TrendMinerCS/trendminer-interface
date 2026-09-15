## trendminer_interface.objects.ContextNumericFieldFilter

Filter on context numeric field values

Attributes:

| Name      | Type                                                      | Description                                                      |
| --------- | --------------------------------------------------------- | ---------------------------------------------------------------- |
| `field`   | `ContextField`                                            | The context field on which to filter. Must be of 'numeric' type. |
| `queries` | `list of tuple[{"=", "!=", ">", "<", ">=", "<="}, float]` | List of operator-value tuples to filter on.                      |
| `mode`    | \`{'empty', 'not empty'}                                  | None\`                                                           |

### field

```
field: ContextField
```

### queries

```
queries: list[tuple[NumericFieldOperator, float]] | None
```

### mode

```
mode: EmptyMode | None
```
