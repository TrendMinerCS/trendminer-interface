## trendminer_interface.objects.DraftGaugeTile

Bases: `TileBase[GaugeTileConfiguration]`

Draft Gauge tile

Attributes:

| Name            | Type                   | Description                                               |
| --------------- | ---------------------- | --------------------------------------------------------- |
| `component`     | \`Tag                  | Attribute                                                 |
| `mode`          | \`GaugeTileMode        | None\`                                                    |
| `default_range` | \`GaugeTileRange       | None\`                                                    |
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
component: Tag | Attribute | None
```

### mode

```
mode: GaugeTileMode | None
```

### default_range

```
default_range: GaugeTileRange | None
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
