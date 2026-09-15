## trendminer_interface.objects.trend.trendhub_view.TrendHubViewDefinition

Definition for a trend hub view

Attributes:

| Name                  | Type                                       | Description                                                                                         |
| --------------------- | ------------------------------------------ | --------------------------------------------------------------------------------------------------- |
| `entries`             | `list[TrendHubEntry]`                      | List of entries (tags, attributes, groups) included in the view                                     |
| `layers`              | `list[TrendHubLayer]`                      | List of layers included in the view                                                                 |
| `context_interval`    | `Interval`                                 | Context interval of the view                                                                        |
| `filter_entries`      | `list[tuple[Filter, bool]]`                | List of filters included in the view, with their active state                                       |
| `fingerprint_entries` | `list[tuple[Fingerprint, bool, Interval]]` | List of fingerprints included in the view, with their active state and interval to which they apply |

Notes

fingerprint_entries and filter_entries may reference saved items which no longer exist. Attempting to access the attributes of these items will result in a ResourceNotFound error.

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

### generate_url

```
generate_url() -> str
```

Generate a unique link to the defined view in TrendHub

Returns:

| Type  | Description                  |
| ----- | ---------------------------- |
| `str` | Link to the view in TrendHub |
