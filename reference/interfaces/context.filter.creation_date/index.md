# `client.context.filter.creation_date`

## trendminer_interface.\_client.context.filter.creation_date_filter.ContextCreationDateFilterFacade

Facade for creating context creation date filters

### new

```
new(
    operator: Literal[">", ">=", "<", "<="],
    timestamp: Timestamp,
) -> ContextCreationDateFilter
```

Conditional filter on context item creation date

Parameters:

| Name        | Type                     | Description                                                        | Default    |
| ----------- | ------------------------ | ------------------------------------------------------------------ | ---------- |
| `operator`  | `('>', '>=', '<', '<=')` | The operator to apply to the timestamp criterion                   | `">"`      |
| `timestamp` | `Timestamp`              | The timestamp criterion to apply to the context item creation date | *required* |

Returns:

| Type                        | Description |
| --------------------------- | ----------- |
| `ContextCreationDateFilter` |             |
