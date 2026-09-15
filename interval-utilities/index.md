# Interval utilities

Importing `trendminer_interface` automatically imports `interval_utilities`, which registers a pandas DataFrame accessor under the `inu` namespace — you never need to import it yourself. From that point on, any DataFrame whose index is a [`pandas.IntervalIndex`](https://pandas.pydata.org/docs/reference/api/pandas.IntervalIndex.html) of timezone-aware timestamps gains a family of interval operations under `df.inu`: shifting, growing, shrinking and rounding interval edges, deriving new intervals relative to existing ones, inverting an index to its gaps, grouping overlapping intervals, and drawing random samples. The SDK uses these same utilities internally.

Every method returns a **new** DataFrame; nothing is edited in place. That makes the operations composable — you can chain them to shape interval data into exactly the form your analysis needs.

## Intervals, interval indices, and events

Intervals are a key concept throughout this library — they appear all over as both parameters and return types — so it is worth familiarizing yourself with pandas' own interval types before reaching for these utilities. The accessor operates directly on them, and their `closed` semantics, edge attributes and timedelta arguments all follow pandas' conventions:

- an **interval** is a single [`pandas.Interval`](https://pandas.pydata.org/docs/reference/api/pandas.Interval.html) — a span with a `left` edge, a `right` edge, and a `closed` attribute.
- **intervals** are a [`pandas.IntervalIndex`](https://pandas.pydata.org/docs/reference/api/pandas.IntervalIndex.html) — an index made up of many such intervals.
- **events** are a `pandas.DataFrame` indexed by an `IntervalIndex`, pairing each interval with the data recorded over it.

This is the vocabulary used throughout the documentation. The `inu` namespace only exists on events — a DataFrame with an `IntervalIndex`; accessing it on a DataFrame with any other index raises `AttributeError`.

## Examples

Widen every interval by an hour on each side:

```
widened = df.inu.grow(left="1h", right="1h")
```

Shift every interval an hour later in time:

```
shifted = df.inu.shift(pd.Timedelta("1h"))
```

Round interval edges to a whole hour, growing outwards so nothing is lost:

```
rounded = df.inu.round("1h", left="grow", right="grow")
```

Take the overall span of the index as a single `pandas.Interval`:

```
span = df.inu.get_span()
```

Invert the index to get the gaps between the intervals as a new set of events:

```
gaps = df.inu.invert(name="gaps")
```

Group overlapping intervals together and aggregate within each group:

```
merged = df.inu.group_overlapping().first()
```

Draw three random five-minute sub-intervals in total, spread across all the intervals:

```
samples = df.inu.sample(duration=pd.Timedelta("5m"), n=3)
```

## Reference

- **[The `inu` accessor](https://trendminercs.github.io/trendminer-interface/interval-utilities/DataFrameIntervalUtilitiesAccessor/index.md)** — full reference for every method on the accessor, with signatures and parameter descriptions.
