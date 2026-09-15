# `client.dashboard.gauge`

## trendminer_interface.\_client.dashboard.gauge.GaugeTileFacade

Facade for creating gauge tiles

### config

```
config(
    show_title: bool = True,
    accuracy: float | None = None,
    colored_value: bool = False,
    percentage_ranges: bool = False,
    percentage_delta: bool = False,
    percentage_value: bool = False,
    show_range_labels: bool = True,
    show_delta: bool = False,
    show_ticks: bool = True,
    show_timestamp: bool = True,
    use_chart_alias: bool = False,
) -> GaugeTileConfiguration
```

Default configuration for gauge tiles

Parameters:

| Name                | Type    | Description                                                                | Default |
| ------------------- | ------- | -------------------------------------------------------------------------- | ------- |
| `show_title`        | `bool`  | Whether to show the tile title, by default True                            | `True`  |
| `accuracy`          | `float` | Number of decimal places to show for the value, by default None            | `None`  |
| `colored_value`     | `bool`  | Whether to color the value based on the range colors, by default False     | `False` |
| `percentage_ranges` | `bool`  | Whether to display the ranges as percentages, by default False             | `False` |
| `percentage_delta`  | `bool`  | Whether to display the target difference as a percentage, by default False | `False` |
| `percentage_value`  | `bool`  | Whether to display the value as a percentage, by default False             | `False` |
| `show_range_labels` | `bool`  | Whether to show the range labels, by default True                          | `True`  |
| `show_delta`        | `bool`  | Whether to show the target difference, by default False                    | `False` |
| `show_ticks`        | `bool`  | Whether to show the ticks on the gauge, by default True                    | `True`  |
| `show_timestamp`    | `bool`  | Whether to show the timestamp of the value, by default True                | `True`  |
| `use_chart_alias`   | `bool`  | Whether to use the chart alias for the component, by default False         | `False` |

Returns:

| Type                     | Description |
| ------------------------ | ----------- |
| `GaugeTileConfiguration` |             |

### new

```
new(
    position: tuple[int, int, int, int],
    component: Tag | Attribute,
    default_range: GaugeTileRange,
    ranges: list[GaugeTileRange] | None = None,
    mode: GaugeTileMode = "angular",
    target: float | None = None,
    title: str = "",
    refresh_rate: Timedelta = Timedelta(minutes=1),
    config: GaugeTileConfiguration | None = None,
) -> GaugeTile
```

Instantiate a new gauge tile

Parameters:

| Name            | Type                        | Description                                                                                   | Default                |
| --------------- | --------------------------- | --------------------------------------------------------------------------------------------- | ---------------------- |
| `position`      | `tuple[int, int, int, int]` | Position of the tile on the dashboard (x, y, width, height)                                   | *required*             |
| `component`     | `Tag or Attribute`          | Time-series component to display in the gauge tile                                            | *required*             |
| `default_range` | `GaugeTileRange`            | Default range for the gauge tile (min, max, label, color)                                     | *required*             |
| `ranges`        | `list[GaugeTileRange]`      | Additional ranges for the gauge tile. List of (min, max, label, color), by default None       | `None`                 |
| `mode`          | `GaugeTileMode`             | Type of gauge tile ("vertical", "horizontal", "angular" or "speedometer"). Default "angular". | `'angular'`            |
| `target`        | `float`                     | Target value to display in the gauge tile, by default None                                    | `None`                 |
| `title`         | `str`                       | Title of the tile, by default ""                                                              | `''`                   |
| `refresh_rate`  | `Timedelta`                 | Refresh rate of the tile, by default 1m.                                                      | `Timedelta(minutes=1)` |
| `config`        | `GaugeTileConfiguration`    | Configuration of the tile. If None, default configuration is used.                            | `None`                 |

Returns:

| Type        | Description |
| ----------- | ----------- |
| `GaugeTile` |             |
