## trendminer_interface.objects.MonitorTile

Bases: `TileBase[MonitorTileConfiguration]`

Monitor tile

Attributes:

| Name           | Type                   | Description                                                                                  |
| -------------- | ---------------------- | -------------------------------------------------------------------------------------------- |
| `monitor`      | `Monitor`              | The monitor to display in the tile                                                           |
| `active`       | `MonitorTileCondition` | Condition to display when the monitor is active (triggered): (icon, text label, color)       |
| `inactive`     | `MonitorTileCondition` | Condition to display when the monitor is inactive (not triggered): (icon, text label, color) |
| `refresh_rate` | `Timedelta`            | How often the tile is refreshed if the dashboard is live.                                    |

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

### monitor

```
monitor: Monitor
```

### active

```
active: MonitorTileCondition
```

### inactive

```
inactive: MonitorTileCondition
```

### refresh_rate

```
refresh_rate: Timedelta
```
