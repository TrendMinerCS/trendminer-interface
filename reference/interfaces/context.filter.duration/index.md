# `client.context.filter.duration`

## trendminer_interface.\_client.context.filter.duration_filter.ContextDurationFilterFacade

Facade for creating context duration filters

### new

```
new(
    queries: list[tuple[DurationOperator, Timedelta]],
) -> ContextDurationFilter
```

Filter on context item duration

Parameters:

| Name      | Type                                       | Description                   | Default    |
| --------- | ------------------------------------------ | ----------------------------- | ---------- |
| `queries` | `list[tuple[DurationOperator, Timedelta]]` | Duration queries to filter on | *required* |

Returns:

| Type                    | Description |
| ----------------------- | ----------- |
| `ContextDurationFilter` |             |
