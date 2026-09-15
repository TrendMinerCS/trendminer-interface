## trendminer_interface.objects.GaugeTile

Bases: `TileBase[GaugeTileConfiguration]`

Gauge tile

Attributes:

| Name            | Type                   | Description                                               |
| --------------- | ---------------------- | --------------------------------------------------------- |
| `component`     | \`Tag                  | Attribute\`                                               |
| `mode`          | `GaugeTileMode`        | Display mode of the gauge.                                |
| `default_range` | `GaugeTileRange`       | Default range for the gauge: (min, max, label, color)     |
| `ranges`        | `list[GaugeTileRange]` | Additional ranges for the gauge tile                      |
| `target`        | \`float                | None\`                                                    |
| `refresh_rate`  | `Timedelta`            | How often the tile is refreshed if the dashboard is live. |

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

### component

```
component: Tag | Attribute
```

### mode

```
mode: GaugeTileMode
```

### default_range

```
default_range: GaugeTileRange
```

### ranges

```
ranges: list[GaugeTileRange]
```

### target

```
target: float | None
```

### refresh_rate

```
refresh_rate: Timedelta
```
