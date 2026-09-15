# `client.context.filter.string_field`

## trendminer_interface.\_client.context.filter.string_field_filter.ContextStringFieldFilterFacade

Facade for creating context string field filters

### new

```
new(
    field: ContextField,
    values: list[str] | None = None,
    mode: EmptyMode | None = None,
) -> ContextStringFieldFilter
```

Filter on context string field values

Parameters:

| Name     | Type                     | Description                                                                | Default                                                      |
| -------- | ------------------------ | -------------------------------------------------------------------------- | ------------------------------------------------------------ |
| `field`  | `ContextField`           | The context field on which to filter. Must be of 'string' type.            | *required*                                                   |
| `values` | \`list of str            | None\`                                                                     | List of values to filter on. Allows wildcard character '\*'. |
| `mode`   | `('empty', 'not empty')` | When not None, filter on empty/non-empty field instead of specific values. | `"empty"`                                                    |

Returns:

| Type                       | Description |
| -------------------------- | ----------- |
| `ContextStringFieldFilter` |             |
