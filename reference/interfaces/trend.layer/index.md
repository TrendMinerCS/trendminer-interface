# `client.trend.layer`

## trendminer_interface.\_client.trend.layer.TrendHubLayerFacade

Facade for instantiating new TrendHub layers

### new

```
new(
    interval: Interval,
    base: bool,
    name: str = "",
    line_style: LineStyle | None = None,
    visible: bool = True,
    hidden_references: list[Tag | Attribute] | None = None,
) -> TrendHubLayer
```

Define a new TrendHub view layer

Parameters:

| Name                | Type        | Description                                                                                                                                                                                                                                       | Default                                                                             |
| ------------------- | ----------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------- |
| `interval`          | `Interval`  | Time interval set in the layer. Matches the interval displayed in the TrendHub view only if the view is not live and there is no shift applied to the layer. The layers in a TrendHub view are expected to have intervals with the same duration. | *required*                                                                          |
| `base`              | `bool`      | Whether the layer is a base layer. Base layers are always visible, have a solid line style, and cannot be shifted. Every TrendHub view must have a single base layer.                                                                             | *required*                                                                          |
| `name`              | `str`       | Name of the layer, displayed in TrendHub. Default is an empty string, which will be shown as 'Layer' in TrendHub.                                                                                                                                 | `''`                                                                                |
| `line_style`        | `LineStyle` | Line style of the layer. If not specified, defaults to 'solid' for base layers and 'dash' for non-base layers.                                                                                                                                    | `None`                                                                              |
| `visible`           | `bool`      | Whether the layer is visible in the TrendHub view. Default is True. Base layers must be visible.                                                                                                                                                  | `True`                                                                              |
| `hidden_references` | \`list\[Tag | Attribute\]\`                                                                                                                                                                                                                                     | List of tags and attributes that are hidden in the layer. Default is an empty list. |

Returns:

| Type            | Description |
| --------------- | ----------- |
| `TrendHubLayer` |             |
