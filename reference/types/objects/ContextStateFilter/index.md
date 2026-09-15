## trendminer_interface.objects.ContextStateFilter

Filter on context item current state

Attributes:

| Name     | Type                         | Description                                                                                       |
| -------- | ---------------------------- | ------------------------------------------------------------------------------------------------- |
| `states` | `list of str`                | Allowed context item states. Ignored when using mode.                                             |
| `mode`   | `{'open', 'closed'} or None` | When not None, filter for only open (ongoing) or closed context items, ignoring any given states. |

### states

```
states: list[str]
```

### mode

```
mode: ClosedMode | None
```
