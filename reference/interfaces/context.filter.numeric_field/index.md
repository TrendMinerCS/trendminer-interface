# `client.context.filter.numeric_field`

## trendminer_interface.\_client.context.filter.numeric_field_filter.ContextNumericFieldFilterFacade

Facade for creating context numeric field filters

### new

```
new(
    field: ContextField,
    queries: list[
        tuple[
            Literal["=", "!=", ">", "<", ">=", "<="], float
        ]
    ]
    | None = None,
    mode: EmptyMode | None = None,
) -> ContextNumericFieldFilter
```

Filter on context numeric field values

Parameters:

| Name      | Type                                                        | Description                                                                | Default                                     |
| --------- | ----------------------------------------------------------- | -------------------------------------------------------------------------- | ------------------------------------------- |
| `field`   | `ContextField`                                              | The context field on which to filter. Must be of 'numeric' type.           | *required*                                  |
| `queries` | \`list of tuple[{"=", "!=", ">", "\<", ">=", "\<="}, float] | None\`                                                                     | List of operator-value tuples to filter on. |
| `mode`    | `('empty', 'not empty')`                                    | When not None, filter on empty/non-empty field instead of specific values. | `"empty"`                                   |

Returns:

| Type                        | Description |
| --------------------------- | ----------- |
| `ContextNumericFieldFilter` |             |
