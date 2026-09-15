## trendminer_interface.objects.ContextIntervalFilter

Filter on context item event or creation time through fixed interval

Attributes:

| Name       | Type                         | Description                                                                         |
| ---------- | ---------------------------- | ----------------------------------------------------------------------------------- |
| `interval` | `Interval`                   | The time interval on which to filter                                                |
| `scope`    | `{'event', 'creation date'}` | Whether to filter on the context item timestamps or the context item creation date. |

Notes

For a conditional filter on creation date, use ContextCreationDateFilter instead.

### interval

```
interval: Interval
```

### scope

```
scope: ContextIntervalScope
```
