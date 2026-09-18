# `client.trend.chart.scatter`

## trendminer_interface.\_client.trend.chart.scatter.ScatterChartPropertiesFacade

Facade for creating new scatter chart properties

### new

```
new(
    locked: bool = False,
    label_type: ChartLabelType = "alias",
    grid_lines: bool = False,
) -> ScatterChartProperties
```

Create a new scatter chart properties instance

Parameters:

| Name         | Type             | Description                                             | Default   |
| ------------ | ---------------- | ------------------------------------------------------- | --------- |
| `locked`     | `bool`           | Whether to lock the focus chart duration                | `False`   |
| `label_type` | `ChartLabelType` | Property by which to label the view tags and attributes | `"alias"` |
| `grid_lines` | `bool`           | Whether to show grid lines                              | `False`   |

Notes

Other scatter plot chart properties such as colors, layer selection and reference lines are currently not configurable, and will be set to default.
