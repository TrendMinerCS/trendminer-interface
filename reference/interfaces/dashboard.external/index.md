# `client.dashboard.external`

## trendminer_interface.\_client.dashboard.external.ExternalContentTileFacade

Facade for creating external content tiles

### config

```
config(
    show_title: bool = True,
) -> ExternalContentTileConfiguration
```

Create a new external content tile configuration

Parameters:

| Name         | Type   | Description                    | Default |
| ------------ | ------ | ------------------------------ | ------- |
| `show_title` | `bool` | Whether to show the tile title | `True`  |

Returns:

| Type                               | Description |
| ---------------------------------- | ----------- |
| `ExternalContentTileConfiguration` |             |

### new

```
new(
    position: tuple[int, int, int, int],
    url: str | None = None,
    title: str = "",
    refresh_rate: Timedelta = Timedelta(minutes=5),
    config: ExternalContentTileConfiguration | None = None,
) -> ExternalContentTile
```

Create a new external content tile

Parameters:

| Name           | Type                               | Description                                                              | Default                |
| -------------- | ---------------------------------- | ------------------------------------------------------------------------ | ---------------------- |
| `position`     | `tuple[int, int, int, int]`        | x, y, width and height of the tile on the dashboard                      | *required*             |
| `url`          | `str`                              | The URL of the external content to display                               | `None`                 |
| `title`        | `str`                              | Title of the tile, by default ""                                         | `''`                   |
| `refresh_rate` | `Timedelta`                        | How often the tile is refreshed if the dashboard is live. Default is 5m. | `Timedelta(minutes=5)` |
| `config`       | `ExternalContentTileConfiguration` | The configuration of the tile. Default configuration when not provided.  | `None`                 |

Returns:

| Type                  | Description |
| --------------------- | ----------- |
| `ExternalContentTile` |             |
