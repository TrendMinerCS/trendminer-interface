## trendminer_interface.objects.NotebookTile

Bases: `TileBase[NotebookTileConfiguration]`

Notebook pipeline dashboard tile

Attributes:

| Name           | Type                           | Description                                               |
| -------------- | ------------------------------ | --------------------------------------------------------- |
| `pipeline`     | \`Pipeline                     | None\`                                                    |
| `refresh_rate` | `pandas.Timedelta, default 5m` | How often the tile is refreshed if the dashboard is live. |

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

### pipeline

```
pipeline: Pipeline | None
```

### refresh_rate

```
refresh_rate: Timedelta
```
