## trendminer_interface.objects.ContextHubViewTile

Bases: `TileBase[ContextHubViewTileConfiguration]`

ContextHub view tile

Tile content is a ContextHub view

Attributes:

| Name           | Type                     | Description                                               |
| -------------- | ------------------------ | --------------------------------------------------------- |
| `view`         | `ContextHubView`         | The ContextHub view displayed in the tile                 |
| `mode`         | `ContextHubViewTileMode` | The display mode of the tile                              |
| `refresh_rate` | `Timedelta`              | How often the tile is refreshed if the dashboard is live. |

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
view: ContextHubView
```

### mode

```
mode: ContextHubViewTileMode
```

### refresh_rate

```
refresh_rate: Timedelta
```
