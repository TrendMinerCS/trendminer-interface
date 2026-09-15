# `client.context.filter.interval`

## trendminer_interface.\_client.context.filter.interval_filter.ContextIntervalFilterFacade

Facade for creating context interval filters

### new

```
new(
    interval: Interval,
    scope: Literal["event", "creation date"] = "event",
) -> ContextIntervalFilter
```

Filter on context item event or creation time through fixed interval

Parameters:

| Name       | Type                                | Description                                                                         | Default    |
| ---------- | ----------------------------------- | ----------------------------------------------------------------------------------- | ---------- |
| `interval` | `Interval`                          | The time interval on which to filter                                                | *required* |
| `scope`    | `Literal['event', 'creation date']` | Whether to filter on the context item timestamps or the context item creation date. | `'event'`  |

Returns:

| Type                    | Description |
| ----------------------- | ----------- |
| `ContextIntervalFilter` |             |
