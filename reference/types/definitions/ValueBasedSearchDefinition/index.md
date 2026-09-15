## trendminer_interface.objects.search.value_based_search.ValueBasedSearchDefinition

Bases: `BaseSearchDefinition`

Definition for a value based search

Attributes:

| Name       | Type                          | Description                                                                |
| ---------- | ----------------------------- | -------------------------------------------------------------------------- |
| `queries`  | `list[ValueBasedSearchQuery]` | Search query tuples.                                                       |
| `duration` | `Timedelta`                   | Duration of the search.                                                    |
| `operator` | `{'and', 'or'}`               | How the queries are combined ("and": all must match; "or": any may match). |

### queries

```
queries: list[ValueBasedSearchQuery] = queries
```

### duration

```
duration: Timedelta = duration
```

### operator

```
operator: ValueBasedSearchMode = mode
```

### calculations

```
calculations: dict[str, SearchCalculation] = calculations
```

### get_results

```
get_results(
    target: Interval[Timestamp] | DataFrame,
    drop: bool = True,
    page: int = 0,
    size: int = 10000,
) -> PagedDataFrame
```

Perform a search based on the definition

Parameters:

| Name     | Type                    | Description                                                                                                                                                                                                                                                                                                                                                                   | Default    |
| -------- | ----------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------- |
| `target` | `Interval or DataFrame` | The input intervals to search for. Can be either a single pandas Interval or a DataFrame with IntervalIndex containing non-overlapping intervals. The closed property of the target will be retained in the search results.                                                                                                                                                   | *required* |
| `drop`   | `bool`                  | Whether to drop the original interval columns from the resulting DataFrame, by default True. If False, the original interval in which each search result was found will be kept as a column in the resulting DataFrame. For a pd.Interval input, the name of this column will be search_interval. For a DataFrame input, the name of the original IntervalIndex will be kept. | `True`     |
| `page`   | `int`                   | The page number of results to retrieve. Default is 0 (the first page).                                                                                                                                                                                                                                                                                                        | `0`        |
| `size`   | `int`                   | The number of results to include in each page. Default is 10000.                                                                                                                                                                                                                                                                                                              | `10000`    |

Returns:

| Type             | Description                                                                                           |
| ---------------- | ----------------------------------------------------------------------------------------------------- |
| `PagedDataFrame` | Page containing DataFrame with IntervalIndex and columns corresponding to the calculations specified. |

Raises:

| Type         | Description                                                                                       |
| ------------ | ------------------------------------------------------------------------------------------------- |
| `ValueError` | If target is neither a pandas Interval nor a pandas DataFrame, or if the input intervals overlap. |

Notes

Any columns already present in an input DataFrame will be kept. Their values will be mapped to the search results based on the intervals in which the search results were found.
