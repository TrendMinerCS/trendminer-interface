## trendminer_interface.objects.CurrentValueTile

Bases: `TileBase[CurrentValueTileConfiguration]`

Dashboard current value tile

Attributes:

| Name           | Type                           | Description                                               |
| -------------- | ------------------------------ | --------------------------------------------------------- |
| `entries`      | `list[CurrentValueTileEntry]`  | List of current value entries to display in the tile      |
| `refresh_rate` | `pandas.Timedelta, default 1m` | How often the tile is refreshed if the dashboard is live. |

### position

```
position: tuple[int, int, int, int]
```

### title

```
title: str
```

### config

```
config: TConfig
```

### entries

```
entries: list[CurrentValueTileEntry]
```

### refresh_rate

```
refresh_rate: Timedelta
```
