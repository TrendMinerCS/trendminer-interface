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

The text tile content will be rendered as HTML.

Parameters:

| Name       | Type                        | Description                                                             | Default    |
| ---------- | --------------------------- | ----------------------------------------------------------------------- | ---------- |
| `position` | `tuple[int, int, int, int]` | x, y, width and height of the tile on the dashboard                     | *required* |
| `content`  | `str`                       | The HTML content to display in the text tile                            | *required* |
| `title`    | `str`                       | The tile title                                                          | `''`       |
| `config`   | `TextTileConfiguration`     | The configuration of the tile. Default configuration when not provided. | `None`     |

Returns:

| Type       | Description |
| ---------- | ----------- |
| `TextTile` |             |

Examples:

```
>>> content = (
...     '<h2 style="border: 1px solid #E8663C; '
...     'border-radius: 6px; '
...     'padding: 8px 12px; '
...     'width: fit-content; '
...     'margin: 0 auto;">'
...     '<a href="https://community.trendminer.com/" '
...     'target="_blank" '
...     'style="color: #E8663C; text-decoration: none;">'
...     "TM Community"
...     "</a></h2>"
... )
>>> tile = client.dashboard.text.new(position=(0, 0, 4, 4), content=content)
```
