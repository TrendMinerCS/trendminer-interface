# `client.context.filter.period`

## trendminer_interface.\_client.context.filter.period_filter.ContextPeriodFilterFacade

Facade for creating context period filters

### new

```
new(
    period: Timedelta, live: bool = False
) -> ContextPeriodFilter
```

Filter on context item event time with dynamic period

Parameters:

| Name     | Type        | Description                                                                                                       | Default    |
| -------- | ----------- | ----------------------------------------------------------------------------------------------------------------- | ---------- |
| `period` | `Timedelta` | Duration marking a time interval running up to the current time, on which to filter the context items.            | *required* |
| `live`   | `bool`      | Whether a ContextHubView having this filter needs to update live. Does not impact the retrieval of context items. | `False`    |

Returns:

| Type                  | Description |
| --------------------- | ----------- |
| `ContextPeriodFilter` |             |
