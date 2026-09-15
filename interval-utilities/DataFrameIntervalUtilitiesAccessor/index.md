# `DataFrameIntervalUtilitiesAccessor`

## interval_utilities.DataFrameIntervalUtilitiesAccessor

Custom accessor for interval-based calculations and utilities

This accessor is applicable to any DataFrame which has an IntervalIndex based on timezone-aware timestamps. It contains a method for performing TrendMiner-based calculations on the intervals represented by the IntervalIndex, as well as some more generic utility methods for manipulating the IntervalIndex itself.

Methods always return a modified DataFrame, they do not edit in place.

The idea of this accessor is to provide users with an interface to chain multiple calculations and interval operations to gather the data needed for their analysis, directly in the format (a pandas DataFrame) in which their custom analysis will likely take place.

Raises:

| Type             | Description                                                                                                                                                                |
| ---------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `AttributeError` | If the DataFrame's index is not an IntervalIndex. This is checked on first .inu access, so accessing the namespace on a DataFrame with any other index raises immediately. |

### set_closed

```
set_closed(
    closed: Literal["left", "right", "both", "neither"],
) -> DataFrame
```

Set the closed attribute of the DataFrame index

Parameters:

| Name     | Type  | Description                  | Default    |
| -------- | ----- | ---------------------------- | ---------- |
| `closed` | `str` | left, right, both or neither | *required* |

Returns:

| Name | Type        | Description                                   |
| ---- | ----------- | --------------------------------------------- |
| `df` | `DataFrame` | DataFrame with altered DataFrame.index.closed |

### shift

```
shift(
    by: Timedelta,
    name: str | None = None,
    drop: bool = True,
) -> DataFrame
```

Shift intervals by a given timedelta

Parameters:

| Name   | Type        | Description                                                                                                                                                | Default    |
| ------ | ----------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------- |
| `by`   | `Timedelta` | How much to shift the IntervalIndex. Positive values shift the intervals forward to a later time, while negative values shift backwards to an earlier time | *required* |
| `name` | `str`       | Name of the new IntervalIndex                                                                                                                              | `None`     |
| `drop` | `bool`      | Whether to drop the original IntervalIndex, or keep it as a column in the DataFrame (under its original name)                                              | `True`     |

Returns:

| Name | Type        | Description                          |
| ---- | ----------- | ------------------------------------ |
| `df` | `DataFrame` | DataFrame with shifted IntervalIndex |

### grow

```
grow(
    left: Timedelta | None = None,
    right: Timedelta | None = None,
    name: str | None = None,
    drop: bool = True,
) -> DataFrame
```

Extend the intervals in the index outwards, setting a new IntervalIndex

Parameters:

| Name    | Type        | Description                                                                                                   | Default |
| ------- | ----------- | ------------------------------------------------------------------------------------------------------------- | ------- |
| `left`  | `Timedelta` | How much to extend the interval left (start) point                                                            | `None`  |
| `right` | `Timedelta` | How much to extend the interval right (end) point                                                             | `None`  |
| `name`  | `str`       | Name of the new IntervalIndex                                                                                 | `None`  |
| `drop`  | `bool`      | Whether to drop the original IntervalIndex, or keep it as a column in the DataFrame (under its original name) | `True`  |

Returns:

| Name | Type        | Description                           |
| ---- | ----------- | ------------------------------------- |
| `df` | `DataFrame` | DataFrame with extended IntervalIndex |

See Also

shrink : Shrink the intervals inwards.

### shrink

```
shrink(
    left: Timedelta | None = None,
    right: Timedelta | None = None,
    name: str | None = None,
    drop: bool = True,
) -> DataFrame
```

Shrink the intervals in the index inwards, setting a new IntervalIndex

Parameters:

| Name    | Type        | Description                                                                                                   | Default |
| ------- | ----------- | ------------------------------------------------------------------------------------------------------------- | ------- |
| `left`  | `Timedelta` | How much to shrink the interval left (start) point                                                            | `None`  |
| `right` | `Timedelta` | How much to shrink the interval right (end) point                                                             | `None`  |
| `name`  | `str`       | Name of the new IntervalIndex                                                                                 | `None`  |
| `drop`  | `bool`      | Whether to drop the original IntervalIndex, or keep it as a column in the DataFrame (under its original name) | `True`  |

Returns:

| Name | Type        | Description                           |
| ---- | ----------- | ------------------------------------- |
| `df` | `DataFrame` | DataFrame with shrunken IntervalIndex |

See Also

grow : Extend the intervals outwards.

### after_start

```
after_start(
    length: Timedelta,
    name: str | None = None,
    drop: bool = True,
) -> DataFrame
```

Set an IntervalIndex of given length with the same starts as the current IntervalIndex

Parameters:

| Name     | Type        | Description                                                                                                   | Default    |
| -------- | ----------- | ------------------------------------------------------------------------------------------------------------- | ---------- |
| `length` | `Timedelta` | The length of the intervals in the new IntervalIndex                                                          | *required* |
| `name`   | `str`       | Name of the new IntervalIndex                                                                                 | `None`     |
| `drop`   | `bool`      | Whether to drop the original IntervalIndex, or keep it as a column in the DataFrame (under its original name) | `True`     |

Returns:

| Name | Type        | Description                      |
| ---- | ----------- | -------------------------------- |
| `df` | `DataFrame` | DataFrame with new IntervalIndex |

### after_end

```
after_end(
    length: Timedelta,
    name: str | None = None,
    drop: bool = True,
) -> DataFrame
```

Set an IntervalIndex with intervals of given length that follows right after the current IntervalIndex

Parameters:

| Name     | Type        | Description                                                                                                   | Default    |
| -------- | ----------- | ------------------------------------------------------------------------------------------------------------- | ---------- |
| `length` | `Timedelta` | The length of the intervals in the new IntervalIndex                                                          | *required* |
| `name`   | `str`       | Name of the new IntervalIndex                                                                                 | `None`     |
| `drop`   | `bool`      | Whether to drop the original IntervalIndex, or keep it as a column in the DataFrame (under its original name) | `True`     |

Returns:

| Name | Type        | Description                      |
| ---- | ----------- | -------------------------------- |
| `df` | `DataFrame` | DataFrame with new IntervalIndex |

### before_start

```
before_start(
    length: Timedelta,
    name: str | None = None,
    drop: bool = True,
) -> DataFrame
```

Set an IntervalIndex with intervals of given length that falls right before the current IntervalIndex

Parameters:

| Name     | Type        | Description                                                                                                   | Default    |
| -------- | ----------- | ------------------------------------------------------------------------------------------------------------- | ---------- |
| `length` | `Timedelta` | The length of the intervals in the new IntervalIndex                                                          | *required* |
| `name`   | `str`       | Name of the new IntervalIndex                                                                                 | `None`     |
| `drop`   | `bool`      | Whether to drop the original IntervalIndex, or keep it as a column in the DataFrame (under its original name) | `True`     |

Returns:

| Name | Type        | Description                      |
| ---- | ----------- | -------------------------------- |
| `df` | `DataFrame` | DataFrame with new IntervalIndex |

### before_end

```
before_end(
    length: Timedelta,
    name: str | None = None,
    drop: bool = True,
) -> DataFrame
```

Set an IntervalIndex with intervals of given length with the same ends as the current IntervalIndex

Parameters:

| Name     | Type        | Description                                                                                                   | Default    |
| -------- | ----------- | ------------------------------------------------------------------------------------------------------------- | ---------- |
| `length` | `Timedelta` | The length of the intervals in the new IntervalIndex                                                          | *required* |
| `name`   | `str`       | Name of the new IntervalIndex                                                                                 | `None`     |
| `drop`   | `bool`      | Whether to drop the original IntervalIndex, or keep it as a column in the DataFrame (under its original name) | `True`     |

Returns:

| Name | Type        | Description                      |
| ---- | ----------- | -------------------------------- |
| `df` | `DataFrame` | DataFrame with new IntervalIndex |

### round

```
round(
    freq: Timedelta,
    left: Literal["shrink", "grow", "nearest"] = "shrink",
    right: Literal["shrink", "grow", "nearest"] = "shrink",
) -> DataFrame
```

Round the intervals to a given frequency

Parameters:

| Name    | Type        | Description                                                                                                                                                                                                            | Default    |
| ------- | ----------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------- |
| `freq`  | `Timedelta` | Rounding frequency                                                                                                                                                                                                     | *required* |
| `left`  | `str`       | 'shrink' round interval start timestamp inwards, shrinking the interval 'grow' round interval start timestamp outwards, growing the interval 'nearest' round interval start timestamp to the nearest rounded timestamp | `'shrink'` |
| `right` | `str`       | 'shrink' round interval end timestamp inwards, shrinking the interval 'grow' round interval end timestamp outwards, growing the interval 'nearest' round interval end timestamp to the nearest rounded timestamp       | `'shrink'` |

Returns:

| Name | Type        | Description                          |
| ---- | ----------- | ------------------------------------ |
| `df` | `DataFrame` | DataFrame with rounded IntervalIndex |

### group_overlapping

```
group_overlapping() -> DataFrameGroupBy
```

Group overlapping intervals

Returns:

| Type               | Description |
| ------------------ | ----------- |
| `DataFrameGroupBy` |             |

Notes

This method will not group intervals that simply touch (i.e. when one interval's `left` is the other interval's `right`, but the `IntervalIndex.closed` is `left`, `right` or `neither`).

### invert

```
invert(
    name: str, span: Interval | None = None
) -> DataFrame
```

Get the intervals in between the current intervals

The output will be sorted from oldest to newest intervals.

Parameters:

| Name   | Type       | Description                                                                                                                                                                                                                                                                                                                                                                                        | Default    |
| ------ | ---------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------- |
| `name` | `str`      | Name of the new, inverted IntervalIndex                                                                                                                                                                                                                                                                                                                                                            | *required* |
| `span` | `Interval` | Range over which the intervals need to be inverted. The time from the start of the span to the start of the leftmost interval, and the time from the rightmost interval to the end of the span are also returned as inverted intervals. Input intervals outside the given span are ignored. When no span is given, the intervals inbetween the input intervals are returned as inverted intervals. | `None`     |

Returns:

| Type        | Description                                 |
| ----------- | ------------------------------------------- |
| `DataFrame` | Empty DataFrame with inverted IntervalIndex |

Notes

- The `closed` attribute of the IntervalIndex will invert 'neither' \<-> 'both', while 'left' and 'right' will stay unchanged.

See Also

get_span : Interval encompassing all intervals in the index, usable as the `span` argument.

### get_span

```
get_span() -> Interval
```

Get the interval encompassing all intervals in the index

Returns:

| Name   | Type       | Description                                  |
| ------ | ---------- | -------------------------------------------- |
| `span` | `Interval` | The interval spanning the full IntervalIndex |

See Also

invert : Get the gaps between the intervals, optionally bounded by a span.

### sample

```
sample(
    duration: Timedelta,
    n: int = 1,
    overlap: bool = False,
    freq: Timedelta = Timedelta(minutes=1),
    drop: bool = True,
    name: str = "samples",
    seed: int | Generator | None = None,
) -> DataFrame
```

Sample random sub-intervals from a given list of intervals

Parameters:

| Name       | Type               | Description                                                                                                                    | Default     |
| ---------- | ------------------ | ------------------------------------------------------------------------------------------------------------------------------ | ----------- |
| `duration` | `Timedelta`        | Duration of the sample intervals                                                                                               | *required*  |
| `n`        | `int`              | Total number of sample intervals to return, drawn across all input intervals (not per interval)                                | `1`         |
| `overlap`  | `bool`             | Whether the returned sample intervals can overlap                                                                              | `False`     |
| `freq`     | `Timedelta`        | The resolution to which all inputs and outputs will be rounded.                                                                | `1m`        |
| `drop`     | `bool`             | Whether to drop the original IntervalIndex in the returned DataFrame                                                           | `True`      |
| `name`     | `str`              | Name of the new IntervalIndex column of samples                                                                                | `'samples'` |
| `seed`     | `int or Generator` | Seed or generator for the random sampling, for reproducible output. When omitted, a fresh non-deterministic generator is used. | `None`      |

Returns:

| Name      | Type        | Description                               |
| --------- | ----------- | ----------------------------------------- |
| `samples` | `DataFrame` | DataFrame with sampled intervals as index |

Notes

Intervals will be rounded down to the given freq before sampling.

The sampling method first determines how many samples should be taken per interval, and then iteratively samples that number of sub-intervals from each interval. The number of samples per interval is distributed randomly in proportion to the number of possible sample positions within an interval. An interval can be sampled in `(interval length - duration)/freq + 1` possible ways. For example, there is only 1 way to take a 1h sample out of a 1h interval, while for a freq of 1m there are 60 ways of taking a 1h sample out of a 2h interval.

When the `IntervalIndex.closed` property is `both` it is possible that two samples theoretically overlap at their endpoints even when `overlap=False`.
