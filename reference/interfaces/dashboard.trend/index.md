# `client.dashboard.trend`

## trendminer_interface.\_client.dashboard.trend.TrendHubViewTileFacade

Facade for creating TrendHub view tiles

### config

```
config(
    show_title: bool = True,
    show_context_items: bool = True,
    show_timeframe: bool = True,
    show_component_names: bool = True,
    show_legend: bool = True,
) -> TrendHubViewTileConfiguration
```

New configuration for TrendHub view tiles

Parameters:

| Name                   | Type   | Description                                                | Default |
| ---------------------- | ------ | ---------------------------------------------------------- | ------- |
| `show_title`           | `bool` | Whether to show the tile title, by default True            | `True`  |
| `show_context_items`   | `bool` | Whether to show context items, by default True             | `True`  |
| `show_timeframe`       | `bool` | Whether to show the timeframe, by default True             | `True`  |
| `show_component_names` | `bool` | Whether to show data reference labels, by default True     | `True`  |
| `show_legend`          | `bool` | Whether to show the colored points legend, by default True | `True`  |

Returns:

| Type                            | Description |
| ------------------------------- | ----------- |
| `TrendHubViewTileConfiguration` |             |

### new

```
new(
    position: tuple[int, int, int, int],
    view: TrendHubView,
    mode: TrendHubViewTileMode = "plot",
    title: str = "",
    refresh_rate: Timedelta = Timedelta(minutes=5),
    config: TrendHubViewTileConfiguration | None = None,
) -> TrendHubViewTile
```

Instantiate a new TrendHub view tile

Parameters:

| Name           | Type                            | Description                                                             | Default                |
| -------------- | ------------------------------- | ----------------------------------------------------------------------- | ---------------------- |
| `position`     | `tuple[int, int, int, int]`     | Position of the tile on the dashboard (x, y, width, height)             | *required*             |
| `view`         | `TrendHubView`                  | TrendHub view to display in the tile                                    | *required*             |
| `mode`         | `str`                           | Display mode of the tile: "plot" or "statistics table". Default "plot". | `'plot'`               |
| `title`        | `str`                           | Title of the tile, by default ""                                        | `''`                   |
| `refresh_rate` | `Timedelta`                     | Refresh rate of the tile, by default 5m.                                | `Timedelta(minutes=5)` |
| `config`       | `TrendHubViewTileConfiguration` | Configuration of the tile. If None, default configuration is used.      | `None`                 |

Returns:

| Type               | Description |
| ------------------ | ----------- |
| `TrendHubViewTile` |             |
