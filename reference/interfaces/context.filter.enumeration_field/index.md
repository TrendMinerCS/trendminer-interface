# `client.context.filter.enumeration_field`

## trendminer_interface.\_client.context.filter.enumeration_field_filter.ContextEnumerationFieldFilterFacade

Facade for creating context enumeration field filters

### new

```
new(
    field: ContextField,
    values: list[str] | None = None,
    mode: EmptyMode | None = None,
) -> ContextEnumerationFieldFilter
```

Filter on context enumeration field values

Parameters:

| Name     | Type                     | Description                                                                | Default                                                           |
| -------- | ------------------------ | -------------------------------------------------------------------------- | ----------------------------------------------------------------- |
| `field`  | `ContextField`           | The context field on which to filter. Must be of 'enumeration' type.       | *required*                                                        |
| `values` | \`list of str            | None\`                                                                     | List of values to filter on. Must be values allowed by the field. |
| `mode`   | `('empty', 'not empty')` | When not None, filter on empty/non-empty field instead of specific values. | `"empty"`                                                         |

Returns:

| Type                            | Description |
| ------------------------------- | ----------- |
| `ContextEnumerationFieldFilter` |             |
