# `client.trend.chart.trend`

## trendminer_interface.\_client.trend.chart.trend.TrendChartPropertiesFacade

Facade for creating new trend chart properties

### new

```
new(
    locked: bool = False,
    label_type: ChartLabelType = "alias",
    grid_lines: bool = False,
    filling: bool = False,
    context: bool = True,
    collapsed_filters: bool = False,
) -> TrendChartProperties
```

Create a new trend chart properties instance

Parameters:

| Name                | Type             | Description                                                 | Default   |
| ------------------- | ---------------- | ----------------------------------------------------------- | --------- |
| `locked`            | `bool`           | Whether to lock the focus chart duration                    | `False`   |
| `label_type`        | `ChartLabelType` | Property by which to label the view tags and attributes     | `"alias"` |
| `grid_lines`        | `bool`           | Whether to show grid lines                                  | `False`   |
| `context`           | `bool`           | Whether to display context items                            | `True`    |
| `filling`           | `bool`           | Whether to fill the area below the trend                    | `False`   |
| `collapsed_filters` | `bool`           | Whether to collapse rather than mark filtered-out intervals | `False`   |
