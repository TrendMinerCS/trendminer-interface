# `client.context.filter.state`

## trendminer_interface.\_client.context.filter.state_filter.ContextStateFilterFacade

Facade for creating context state filters

### new

```
new(
    states: list[str] | None = None,
    mode: Literal["open", "closed"] | None = None,
) -> ContextStateFilter
```

Filter on context item current state

Parameters:

| Name     | Type                 | Description                                                                                       | Default                                               |
| -------- | -------------------- | ------------------------------------------------------------------------------------------------- | ----------------------------------------------------- |
| `states` | \`list of str        | None\`                                                                                            | Allowed context item states. Ignored when using mode. |
| `mode`   | `('open', 'closed')` | When not None, filter for only open (ongoing) or closed context items, ignoring any given states. | `"open"`                                              |

Returns:

| Type                 | Description |
| -------------------- | ----------- |
| `ContextStateFilter` |             |
