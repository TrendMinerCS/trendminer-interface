## trendminer_interface.objects.DashboardDefinition

Dashboard definition

Attributes:

| Name                   | Type                     | Description                                                                                                                                            |
| ---------------------- | ------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `tiles`                | `list`                   | Tiles that are on the dashboard                                                                                                                        |
| `live`                 | `bool`                   | Whether the dashboard is updating live                                                                                                                 |
| `global_timeframe`     | `dict`                   | Global timeframe configuration for the dashboard. Currently configured as a raw dictionary. Setting/editing the global timeframe is not yet supported. |
| `chart_aliases`        | \`dict\[Tag              | Attribute, str\]\`                                                                                                                                     |
| `dynamic_font_sizing`  | `bool`                   | Whether dynamic font sizing is enabled                                                                                                                 |
| `override_tile_config` | `bool`                   | Whether the dashboard configuration overrides individual tile settings                                                                                 |
| `config`               | `DashboardConfiguration` | Dashboard configuration settings                                                                                                                       |
| `scrollable`           | `bool`                   | Whether the dashboard is scrollable. Should be True for new dashboards. Exists for backwards compatibility.                                            |

### tiles

```
tiles = tiles
```

### live

```
live = live
```

### global_timeframe

```
global_timeframe = global_timeframe
```

### dynamic_font_sizing

```
dynamic_font_sizing = dynamic_font_sizing
```

### override_tile_config

```
override_tile_config = override_tile_config
```

### config

```
config = config
```

### scrollable

```
scrollable = scrollable
```

### chart_aliases

```
chart_aliases = chart_aliases
```
