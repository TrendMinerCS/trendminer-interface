## trendminer_interface.objects.trend.trendhub_view.TrendHubViewDefinition

Definition for a trend hub view

Attributes:

| Name                  | Type                                       | Description                                                                                         |
| --------------------- | ------------------------------------------ | --------------------------------------------------------------------------------------------------- |
| `entries`             | `list[TrendHubEntry]`                      | List of entries (tags, attributes, groups) included in the view                                     |
| `layers`              | `list[TrendHubLayer]`                      | List of layers included in the view                                                                 |
| `context_interval`    | `Interval`                                 | Context interval of the view                                                                        |
| `chart_properties`    | `ChartProperties`                          | Chart configuration                                                                                 |
| `filter_entries`      | `list[tuple[Filter, bool]]`                | List of filters included in the view, with their active state                                       |
| `fingerprint_entries` | `list[tuple[Fingerprint, bool, Interval]]` | List of fingerprints included in the view, with their active state and interval to which they apply |

Notes

- fingerprint_entries and filter_entries may reference saved items which no longer exist. Attempting to access the attributes of these items will result in a ResourceNotFound error.
- Statistics and layer comparison table formats are currently not configurable

### entries

```
entries: list[TrendHubEntry] = entries
```

### layers

```
layers: list[TrendHubLayer] = layers
```

### context_interval

```
context_interval: Interval = context_interval
```

### chart_properties

```
chart_properties: ChartProperties = chart_properties
```

### filter_entries

```
filter_entries: list[tuple[Filter, bool]] = filter_entries
```

### fingerprint_entries

```
fingerprint_entries: list[
    tuple[Fingerprint, bool, Interval]
] = fingerprint_entries
```

### live

```
live = live
```

### base_layer

```
base_layer: TrendHubLayer
```

The view's base layer

### intervals

```
intervals: IntervalIndex
```

Get the Intervals currently represented by the view layers

This accounts for view live mode and chart lock settings

### generate_url

```
generate_url() -> str
```

Generate a unique link to the defined view in TrendHub

Returns:

| Type  | Description                  |
| ----- | ---------------------------- |
| `str` | Link to the view in TrendHub |

### get_data

```
get_data(freq: Timedelta) -> list[DataFrame]
```

Retrieve interpolated timeseries data for underlying tags

Parameters:

| Name   | Type        | Description      | Default    |
| ------ | ----------- | ---------------- | ---------- |
| `freq` | `Timedelta` | Data resolution. | *required* |

Returns:

| Type              | Description                                                             |
| ----------------- | ----------------------------------------------------------------------- |
| `list[DataFrame]` | A dataframe with DatetimeIndex and tag names as columns for every layer |

Notes

- Any tag time shift will be taken into account: the returned data will be for the shifted tag.
- A call to get TrendMiner data does not automatically trigger indexing of the tag. It is up to the user to ensure the tag is indexed for the required period prior to requesting the data (cfr. Tag.index).
