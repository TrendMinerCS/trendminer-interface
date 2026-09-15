# `client.dashboard.text`

## trendminer_interface.\_client.dashboard.text.TextTileFacade

Facade for creating text tiles

### config

```
config(show_title: bool = True) -> TextTileConfiguration
```

Create a new text tile configuration

Parameters:

| Name         | Type   | Description                    | Default |
| ------------ | ------ | ------------------------------ | ------- |
| `show_title` | `bool` | Whether to show the tile title | `True`  |

Returns:

| Type                    | Description |
| ----------------------- | ----------- |
| `TextTileConfiguration` |             |

### new

```
new(
    position: tuple[int, int, int, int],
    content: str,
    title: str = "",
    config: TextTileConfiguration | None = None,
) -> TextTile
```

Create a new text tile

Parameters:

| Name       | Type                        | Description                                                             | Default    |
| ---------- | --------------------------- | ----------------------------------------------------------------------- | ---------- |
| `position` | `tuple[int, int, int, int]` | x, y, width and height of the tile on the dashboard                     | *required* |
| `content`  | `str`                       | The content to display in the text tile                                 | *required* |
| `title`    | `str`                       | The tile title                                                          | `''`       |
| `config`   | `TextTileConfiguration`     | The configuration of the tile. Default configuration when not provided. | `None`     |

Returns:

| Type       | Description |
| ---------- | ----------- |
| `TextTile` |             |
