# `client.dashboard.context`

## trendminer_interface.\_client.dashboard.context.ContextHubViewTileFacade

Facade for creating ContextHub view tiles

### config

```
config(
    show_title: bool = True,
    show_legend: bool = True,
    show_timeframe: bool = True,
) -> ContextHubViewTileConfiguration
```

Default configuration for ContextHub view tiles

Parameters:

| Name             | Type   | Description                                                                | Default |
| ---------------- | ------ | -------------------------------------------------------------------------- | ------- |
| `show_title`     | `bool` | Whether to show the tile title, by default True                            | `True`  |
| `show_legend`    | `bool` | Whether to show the colored points legend in scatter mode, by default True | `True`  |
| `show_timeframe` | `bool` | Whether to show the timeframe, by default True                             | `True`  |

Returns:

| Type                              | Description |
| --------------------------------- | ----------- |
| `ContextHubViewTileConfiguration` |             |

### new

```
new(
    position: tuple[int, int, int, int],
    view: ContextHubView,
    mode: ContextHubViewTileMode = "count",
    title: str = "",
    refresh_rate: Timedelta = Timedelta(minutes=5),
    config: ContextHubViewTileConfiguration | None = None,
) -> ContextHubViewTile
```

Instantiate a new ContextHub view tile

Parameters:

| Name           | Type                              | Description                                                                         | Default                |
| -------------- | --------------------------------- | ----------------------------------------------------------------------------------- | ---------------------- |
| `position`     | `tuple[int, int, int, int]`       | Position of the tile on the dashboard (x, y, width, height)                         | *required*             |
| `view`         | `ContextHubView`                  | ContextHub view to display in the tile                                              | *required*             |
| `mode`         | `ContextHubViewTileMode`          | Display mode of the tile ("table", "gantt", "scatter" or "count"). Default "count". | `'count'`              |
| `title`        | `str`                             | Title of the tile, by default ""                                                    | `''`                   |
| `refresh_rate` | `Timedelta`                       | Refresh rate of the tile. Default is 5m.                                            | `Timedelta(minutes=5)` |
| `config`       | `ContextHubViewTileConfiguration` | Configuration of the tile. If None, default configuration is used.                  | `None`                 |

Returns:

| Type                 | Description |
| -------------------- | ----------- |
| `ContextHubViewTile` |             |
