## trendminer_interface.objects.ContextDurationFilter

Filter on context item duration

Attributes:

| Name      | Type                                                                 | Description                   |
| --------- | -------------------------------------------------------------------- | ----------------------------- |
| `queries` | `list of tuple[{"<", ">", "<=", ">=", "=", "!="}, pandas.Timedelta]` | Duration queries to filter on |

### queries

```
queries: list[tuple[DurationOperator, Timedelta]]
```
