## trendminer_interface.objects.DraftCurrentValueTile

Bases: `TileBase[CurrentValueTileConfiguration]`

Draft current value tile

Attributes:

| Name           | Type                           | Description                                               |
| -------------- | ------------------------------ | --------------------------------------------------------- |
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

### refresh_rate

```
refresh_rate: Timedelta
```
