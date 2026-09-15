# `client.dashboard.value`

## trendminer_interface.\_client.dashboard.value.CurrentValueTileFacade

Facade for creating current value tiles

### config

```
config(
    show_title: bool = True,
    accuracy: float | None = None,
    show_graph: bool = True,
    graph_duration: Timedelta = Timedelta(hours=1),
    fill_background: bool = False,
    show_component_names: bool = True,
    show_timestamp: bool = True,
    use_chart_alias: bool = False,
) -> CurrentValueTileConfiguration
```

Create a new current value tile configuration

Parameters:

| Name                   | Type            | Description                                                                          | Default |
| ---------------------- | --------------- | ------------------------------------------------------------------------------------ | ------- |
| `show_title`           | `bool`          | Whether to show the tile title, by default True                                      | `True`  |
| `accuracy`             | `float or None` | Accuracy to which values are displayed (..., 10, 1, 0.1, 0.01, ...), by default None | `None`  |
| `show_graph`           | `bool`          | Whether to show the trend graph, by default True                                     | `True`  |
| `graph_duration`       | `Timedelta`     | Duration of the trend graph                                                          | `1h`    |
| `fill_background`      | `bool`          | Whether to fill the background, by default False                                     | `False` |
| `show_component_names` | `bool`          | Whether to show component names, by default True                                     | `True`  |
| `show_timestamp`       | `bool`          | Whether to show timestamp of latest datapoint, by default True                       | `True`  |
| `use_chart_alias`      | `bool`          | Whether to use chart aliases, by default False                                       | `False` |

Returns:

| Type                            | Description |
| ------------------------------- | ----------- |
| `CurrentValueTileConfiguration` |             |

### new

```
new(
    position: tuple[int, int, int, int],
    entries: list[CurrentValueTileEntry],
    title: str = "",
    refresh_rate: Timedelta = Timedelta(minutes=1),
    config: CurrentValueTileConfiguration | None = None,
) -> CurrentValueTile
```

Create a new current value tile

Parameters:

| Name           | Type                            | Description                                                             | Default                |
| -------------- | ------------------------------- | ----------------------------------------------------------------------- | ---------------------- |
| `position`     | `tuple[int, int, int, int]`     | Position of the tile on the dashboard (x, y, width, height)             | *required*             |
| `entries`      | `list[CurrentValueTileEntry]`   | Entries to show in the tile                                             | *required*             |
| `title`        | `str`                           | Title of the tile, by default ""                                        | `''`                   |
| `refresh_rate` | `Timedelta`                     | Refresh rate of the tile when the dashboard is live. Default is 1m.     | `Timedelta(minutes=1)` |
| `config`       | `CurrentValueTileConfiguration` | Configuration of the tile, defaults to a standard configuration if None | `None`                 |

Returns:

| Type               | Description |
| ------------------ | ----------- |
| `CurrentValueTile` |             |
