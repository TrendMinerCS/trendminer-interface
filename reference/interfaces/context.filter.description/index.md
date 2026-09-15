# `client.context.filter.description`

## trendminer_interface.\_client.context.filter.description_filter.ContextDescriptionFilterFacade

Facade for creating context description filters

### new

```
new(
    values: list[str] | None = None,
    mode: EmptyMode | None = None,
) -> ContextDescriptionFilter
```

Context filter on item description

Parameters:

| Name     | Type                     | Description                                                                                                                                                                                               | Default   |
| -------- | ------------------------ | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------- |
| `values` | `list of str`            | Non-empty list of string queries to filter on the description. Can use '\*' as wildcard character.                                                                                                        | `None`    |
| `mode`   | `('empty', 'not empty')` | Filter mode. If None, the filter will be applied on the values. If "empty", the filter will return items with empty description. If "not empty", the filter will return items with non-empty description. | `"empty"` |

Notes

Either values or mode should be provided. They cannot be combined.

Returns:

| Type                       | Description |
| -------------------------- | ----------- |
| `ContextDescriptionFilter` |             |
