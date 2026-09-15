## trendminer_interface.objects.Tag

TrendMiner tag instance

Attributes:

| Name       | Type                          | Description                                                                                                                                                                                                                                                                                                                                                                                                            |
| ---------- | ----------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `shift`    | `Timedelta`                   | Time shift of the tag. Any methods returning timestamped data for the tag will consider this shift. A positive shift values means the tag is moved forward in time (i.e., shifted to the right on the time axis). This results in older data being returned on the same timestamps, or the same data being returned on a later timestamp than if no shift were present. The inverse applies for negative shift values. |
| `visible`  | `bool`                        | Whether the tag is visible in TrendHub. This is used for visualization purposes in TrendHub, and has an impact on fingerprints. Tags retrieved from anywhere but a TrendHub view or Fingerprint will be visible by default.                                                                                                                                                                                            |
| `color`    | `str`                         | The color of the tag, as a hex color code (e.g., "#FF0000" for red). This is used for visualization purposes in TrendHub.                                                                                                                                                                                                                                                                                              |
| `scale`    | `tuple[float, float] or None` | The manually set scale of the tag, as a tuple of (min, max) values, as used in TrendHub visualization. If no manual scale is set (None), the tag will be autoscaled.                                                                                                                                                                                                                                                   |
| `alias`    | `str or None`                 | The alias of the tag, as set in TrendHub.                                                                                                                                                                                                                                                                                                                                                                              |
| `accuracy` | `float or None`               | The accuracy to which tag value representations are rounded in TrendHub. A power of 10 (..., 10, 1, 0.1, 0.01, ...). If None, no rounding is applied.                                                                                                                                                                                                                                                                  |

### shift

```
shift: Timedelta = shift
```

### visible

```
visible: bool = visible
```

### color

```
color: str = color
```

### scale

```
scale: tuple[float, float] | None = scale
```

### alias

```
alias: str | None = alias
```

### accuracy

```
accuracy: float | None = accuracy
```

### identifier

```
identifier: str
```

UUID of the tag

### name

```
name: str
```

Name of the tag

### description

```
description: str
```

Description of the tag

### tag_type

```
tag_type: TagType
```

Type of the tag

### units

```
units: str
```

Units of the tag

### datasource

```
datasource: Datasource
```

Datasource of the tag

### add_aggregation

```
add_aggregation(
    events: DataFrame,
    method: IntervalAggregationMethod,
    name: str,
) -> DataFrame
```

Add a tag aggregation as a column to an event DataFrame

Parameters:

| Name     | Type                        | Description                                               | Default    |
| -------- | --------------------------- | --------------------------------------------------------- | ---------- |
| `events` | `DataFrame`                 | Events DataFrame with a pd.IntervalIndex.                 | *required* |
| `method` | `IntervalAggregationMethod` | Aggregation method to apply over each interval.           | *required* |
| `name`   | `str`                       | Column name under which the aggregation result is stored. | *required* |

Returns:

| Type        | Description                                                             |
| ----------- | ----------------------------------------------------------------------- |
| `DataFrame` | Copy of the input DataFrame with the aggregation added as a new column. |

### get_aggregation

```
get_aggregation(
    intervals: IntervalIndex,
    method: IntervalAggregationMethod,
) -> Series
```

Fetch tag aggregation values for the given intervals

Parameters:

| Name        | Type                        | Description                                     | Default    |
| ----------- | --------------------------- | ----------------------------------------------- | ---------- |
| `intervals` | `IntervalIndex`             | Intervals over which to aggregate the tag.      | *required* |
| `method`    | `IntervalAggregationMethod` | Aggregation method to apply over each interval. | *required* |

Returns:

| Type     | Description                                                                                                                  |
| -------- | ---------------------------------------------------------------------------------------------------------------------------- |
| `Series` | Aggregation results aligned to the input index. float64 for numeric tags, category for digital tags, string for string tags. |

### get_data

```
get_data(interval: Interval, freq: Timedelta) -> Series
```

Retrieve interpolated time series data for the tag

Parameters:

| Name       | Type        | Description                                                                                                                            | Default    |
| ---------- | ----------- | -------------------------------------------------------------------------------------------------------------------------------------- | ---------- |
| `interval` | `Interval`  | Time interval for which the data needs to be retrieved. The interval.closed attribute is taken into account when returning datapoints. | *required* |
| `freq`     | `Timedelta` | Data resolution. Time between subsequent datapoints.                                                                                   | *required* |

Returns:

| Name   | Type     | Description                                                                                                                                                                                                        |
| ------ | -------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `data` | `Series` | Tag data with the following properties: - name is equal to the tag name - index is a DatetimeIndex in the client timezone. - dtype is float64 for numeric tags, category for digital tags, string for string tags. |

Notes

Data is obtained from linear interpolation of the indexed data in TrendMiner. Asking for a high resolution data will not perform a datasource call to obtain datapoints that are not in the index.

Any tag time shift will be taken into account: the returned data will be for the shifted tag.

The returned timestamps result from the interval start time (interval.left) and the provided frequency. If the interval start time is irregular, the resulting timestamps will also be irregular (e.g., 9:15:17.032, 19:15:47.032, ...). If regular intervals are required, it is the user's responsibility to provide a regular (rounded) input interval.

A call to get TrendMiner data does not automatically trigger indexing of the tag. It is up to the user to ensure the tag is indexed for the required period prior to requesting the data (cfr. Tag.index).

If an analog tag is not fully indexed for the requested interval, NaN values will be present for the interval. For stepped tags (discrete, digital and string), the values up to the current timestamp will be forward filled, and only timestamps after the current time will be NaN (discrete) or NA (digital, string).

### search_state_labels

```
search_state_labels(
    name: str | None = None, page: int = 0, size: int = 2000
) -> PagedDict[int, str]
```

Get state index to state name mapping for selected states

Parameters:

| Name   | Type  | Description                                                                                                                                                | Default |
| ------ | ----- | ---------------------------------------------------------------------------------------------------------------------------------------------------------- | ------- |
| `name` | `str` | The name of the state label to search for. Can use '\*' as wildcard. By default, all state labels are returned.                                            | `None`  |
| `page` | `int` | Page number of results to return. By default, start at the first page of results (0-indexed).                                                              | `0`     |
| `size` | `int` | Number of results to return per page. Default is set to 2000, which is the maximum size supported by the API. Set a smaller size for exploratory purposes. | `2000`  |

Returns:

| Type                  | Description                                                                                    |
| --------------------- | ---------------------------------------------------------------------------------------------- |
| `PagedDict[int, str]` | Paginated mapping of state indices to state names for the states matching the search criteria. |

### index

```
index() -> IndexDetails
```

Trigger indexing of the tag in TrendMiner

This method triggers indexing of the tag in TrendMiner. Indexing is required to obtain data for a tag, but it is not automatically triggered when requesting data. It is up to the user to ensure the tag is indexed for the required period prior to requesting the data.

Returns:

| Name            | Type           | Description                                                                  |
| --------------- | -------------- | ---------------------------------------------------------------------------- |
| `index_details` | `IndexDetails` | The indexing details of the tag in TrendMiner after triggering the indexing. |

### delete_index

```
delete_index() -> None
```

Delete the tag index in TrendMiner

This method fully deletes the tag index in TrendMiner.

### refresh_index

```
refresh_index() -> None
```

Refresh the tag index in TrendMiner

This method sends a request to refresh the tag index in TrendMiner, which fully removes the existing index and triggers a new indexing process, fully refreshing the index data.

### get_index_details

```
get_index_details() -> IndexDetails | None
```

Get the indexing status of the tag in TrendMiner

Returns:

| Name     | Type                   | Description                                                                                |
| -------- | ---------------------- | ------------------------------------------------------------------------------------------ |
| `status` | `IndexDetails or None` | The indexing status of the tag in TrendMiner. If the tag is not indexed, None is returned. |
