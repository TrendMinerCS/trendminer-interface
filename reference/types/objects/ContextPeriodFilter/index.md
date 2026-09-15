## trendminer_interface.objects.ContextPeriodFilter

Filter on context item event time with dynamic period

Attributes:

| Name     | Type        | Description                                                                                                       |
| -------- | ----------- | ----------------------------------------------------------------------------------------------------------------- |
| `period` | `Timedelta` | Duration marking a time interval running up to the current time, on which to filter the context items.            |
| `live`   | `bool`      | Whether a ContextHubView having this filter needs to update live. Does not impact the retrieval of context items. |

### period

```
period: Timedelta
```

### live

```
live: bool
```
