# `client.trend.group`

## trendminer_interface.\_client.trend.group.TrendHubEntryGroupFacade

Facade for instantiating new TrendHub entry groups

### new

```
new(
    entries: list[Tag | Attribute],
    name: str,
    scale: tuple[float, float] | None = None,
    accuracy: float | None = None,
) -> TrendHubEntryGroup
```

Create a new TrendHub group of tags and attributes

Parameters:

| Name       | Type                  | Description                                  | Default                                                                                                                                           |
| ---------- | --------------------- | -------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------- |
| `entries`  | \`list\[Tag           | Attribute\]\`                                | List of at least two tags and/or attributes to group.                                                                                             |
| `name`     | `str`                 | Name of the group, as displayed in TrendHub. | *required*                                                                                                                                        |
| `scale`    | \`tuple[float, float] | None\`                                       | Scale to use for the group. Autoscale if None.                                                                                                    |
| `accuracy` | \`float               | None\`                                       | The accuracy to which tag value representations are rounded. A natural exponent of 10 (..., 10, 0.1, 0.01, ...). If None, no rounding is applied. |

Returns:

| Type                 | Description |
| -------------------- | ----------- |
| `TrendHubEntryGroup` |             |
