# `client.dashboard.notebook`

## trendminer_interface.\_client.dashboard.notebook.NotebookTileFacade

Facade for creating notebook tiles

### config

```
config(
    show_title: bool = True,
) -> NotebookTileConfiguration
```

Default configuration for notebook pipeline tiles

Parameters:

| Name         | Type   | Description                                     | Default |
| ------------ | ------ | ----------------------------------------------- | ------- |
| `show_title` | `bool` | Whether to show the tile title, by default True | `True`  |

Returns:

| Type                        | Description |
| --------------------------- | ----------- |
| `NotebookTileConfiguration` |             |

### new

```
new(
    position: tuple[int, int, int, int],
    pipeline: Pipeline | None = None,
    title: str = "",
    refresh_rate: Timedelta = Timedelta(minutes=5),
    config: NotebookTileConfiguration | None = None,
) -> NotebookTile
```

Instantiate a new notebook pipeline tile

Parameters:

| Name           | Type                        | Description                                                        | Default                |
| -------------- | --------------------------- | ------------------------------------------------------------------ | ---------------------- |
| `position`     | `tuple[int, int, int, int]` | Position of the tile on the dashboard (x, y, width, height)        | *required*             |
| `pipeline`     | `Pipeline`                  | Notebook pipeline to display in the tile                           | `None`                 |
| `title`        | `str`                       | Title of the tile, by default ""                                   | `''`                   |
| `refresh_rate` | `Timedelta`                 | Refresh rate of the tile, by default 5m.                           | `Timedelta(minutes=5)` |
| `config`       | `NotebookTileConfiguration` | Configuration of the tile. If None, default configuration is used. | `None`                 |

Returns:

| Type           | Description |
| -------------- | ----------- |
| `NotebookTile` |             |
