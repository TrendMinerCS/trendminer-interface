# `client.dashboard.monitor`

## trendminer_interface.\_client.dashboard.monitor.MonitorTileFacade

Facade for creating monitor tiles

### config

```
config(
    show_title: bool = True, fill_background: bool = False
) -> MonitorTileConfiguration
```

Default configuration for monitor tiles

Parameters:

| Name              | Type   | Description                                                                                 | Default |
| ----------------- | ------ | ------------------------------------------------------------------------------------------- | ------- |
| `show_title`      | `bool` | Whether to show the tile title, by default True                                             | `True`  |
| `fill_background` | `bool` | Whether to fill the tile background with color based on the monitor state, by default False | `False` |

Returns:

| Type                       | Description |
| -------------------------- | ----------- |
| `MonitorTileConfiguration` |             |

### new

```
new(
    position: tuple[int, int, int, int],
    monitor: Monitor,
    active: MonitorTileCondition = (
        "alert-circle",
        "",
        "#FF0010",
    ),
    inactive: MonitorTileCondition = (
        "circle-success",
        "",
        "#2BCE48",
    ),
    title: str = "",
    refresh_rate: Timedelta = Timedelta(minutes=1),
    config: MonitorTileConfiguration | None = None,
) -> MonitorTile
```

Instantiate a new monitor tile

Parameters:

| Name           | Type                        | Description                                                                                                         | Default                             |
| -------------- | --------------------------- | ------------------------------------------------------------------------------------------------------------------- | ----------------------------------- |
| `position`     | `tuple[int, int, int, int]` | Position of the tile on the dashboard (x, y, width, height)                                                         | *required*                          |
| `monitor`      | `Monitor`                   | Monitor to display in the tile                                                                                      | *required*                          |
| `active`       | `MonitorTileCondition`      | Condition to display when the monitor is active (icon, text, color), by default ("alert-circle", "", "#FF0010")     | `('alert-circle', '', '#FF0010')`   |
| `inactive`     | `MonitorTileCondition`      | Condition to display when the monitor is inactive (icon, text, color), by default ("circle-success", "", "#2BCE48") | `('circle-success', '', '#2BCE48')` |
| `title`        | `str`                       | Title of the tile, by default ""                                                                                    | `''`                                |
| `refresh_rate` | `Timedelta`                 | Refresh rate of the tile, by default 1m.                                                                            | `Timedelta(minutes=1)`              |
| `config`       | `MonitorTileConfiguration`  | Configuration of the tile. If None, default configuration is used.                                                  | `None`                              |

Returns:

| Type          | Description |
| ------------- | ----------- |
| `MonitorTile` |             |
