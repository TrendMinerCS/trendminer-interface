## trendminer_interface.objects.CurrentValueTileConfiguration

Configuration for current value tile

Attributes:

| Name                   | Type            | Description                                                         |
| ---------------------- | --------------- | ------------------------------------------------------------------- |
| `show_title`           | `bool`          | Whether to show the tile title                                      |
| `accuracy`             | `float or None` | Accuracy to which values are displayed (..., 10, 1, 0.1, 0.01, ...) |
| `show_graph`           | `bool`          | Whether to show the trend graph                                     |
| `graph_duration`       | `Timedelta`     | Duration of the trend graph                                         |
| `fill_background`      | `bool`          | Whether to fill the background                                      |
| `show_component_names` | `bool`          | Whether to show component names                                     |
| `show_timestamp`       | `bool`          | Whether to show timestamp of latest datapoint                       |
| `use_chart_alias`      | `bool`          | Whether to use chart alias                                          |

### show_title

```
show_title: bool
```

### accuracy

```
accuracy: float | None
```

### show_graph

```
show_graph: bool
```

### graph_duration

```
graph_duration: Timedelta
```

### fill_background

```
fill_background: bool
```

### show_component_names

```
show_component_names: bool
```

### show_timestamp

```
show_timestamp: bool
```

### use_chart_alias

```
use_chart_alias: bool
```
