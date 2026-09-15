## trendminer_interface.objects.TrendHubViewTile

Bases: `TileBase[TrendHubViewTileConfiguration]`

TrendHub view tile

Attributes:

| Name           | Type                   | Description                                               |
| -------------- | ---------------------- | --------------------------------------------------------- |
| `view`         | `TrendHubView`         | The TrendHub view to display                              |
| `mode`         | `TrendHubViewTileMode` | The display mode of the TrendHub view                     |
| `refresh_rate` | `Timedelta`            | How often the tile is refreshed if the dashboard is live. |

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

### view

```
view: TrendHubView
```

### mode

```
mode: TrendHubViewTileMode
```

### refresh_rate

```
refresh_rate: Timedelta
```
