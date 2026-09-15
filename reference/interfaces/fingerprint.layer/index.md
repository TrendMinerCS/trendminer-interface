# `client.fingerprint.layer`

## trendminer_interface.\_client.fingerprint.layer.FingerprintLayerFacade

Facade for instantiating new fingerprint layers

### new

```
new(
    interval: Interval,
    base: bool,
    name: str = "",
    line_style: LineStyle | None = None,
    hidden_references: list[Tag | Attribute] | None = None,
) -> FingerprintLayer
```

Define a new fingerprint layer

Parameters:

| Name                | Type        | Description                                                                                                                                               | Default                                                                             |
| ------------------- | ----------- | --------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------- |
| `interval`          | `Interval`  | Time interval set in the layer.                                                                                                                           | *required*                                                                          |
| `base`              | `bool`      | Whether the layer is a base layer. Base layers always have a solid line style, and cannot be shifted. Every fingerprint must contain a single base layer. | *required*                                                                          |
| `name`              | `str`       | Name of the layer, displayed in TrendHub. Default is an empty string, which will be displayed as 'Layer' in TrendHub.                                     | `''`                                                                                |
| `line_style`        | `LineStyle` | Line style of the layer. If not specified, defaults to 'solid' for base layers and 'dash' for non-base layers.                                            | `None`                                                                              |
| `hidden_references` | \`list\[Tag | Attribute\]\`                                                                                                                                             | List of tags and attributes that are hidden in the layer. Default is an empty list. |

Returns:

| Type               | Description |
| ------------------ | ----------- |
| `FingerprintLayer` |             |
