## trendminer_interface.objects.context.contexthub_view.ContextHubViewDefinition

Bases: `BaseSearchDefinition`

Definition for a context item search

Attributes:

| Name        | Type                  | Description                                 |
| ----------- | --------------------- | ------------------------------------------- |
| `filters`   | `list[ContextFilter]` | Context item filters to apply to the search |
| `view_type` | `ContextHubViewType`  | The type of view (grid, gantt, scatter)     |

### calculations

```
calculations: dict[str, SearchCalculation]
```

### filters

```
filters: list[ContextFilter] = filters
```

### view_type

```
view_type: ContextHubViewType = view_type
```

### get_items

```
get_items(size: int = 10000) -> PagedDataFrame
```

Retrieve all context items matching the ContextHub view definition filters

Parameters:

| Name   | Type  | Description                                              | Default |
| ------ | ----- | -------------------------------------------------------- | ------- |
| `size` | `int` | The number of items to return per page, by default 10000 | `10000` |

Returns:

| Type             | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| ---------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `PagedDataFrame` | PageDataFrame with a DataFrame data attribute with the following structure: Index: The index will be pandas.IntervalIndex, with index.left and index.right timestamps of the context item start and end events, respectively. If a context item only has a single timestamp (i.e., when its type does not have an associated context workflow), index.left and index.right will be identical. For open context item, index.right will be the current time. Metadata columns: - open (bool): whether the context item is still open (i.e., has no end event yet) - key (str): short key - identifier (str): uuid - identifier_external (str): optional identifier by which the item is linked to an external system - description (str): optional description - type (object, ContextType): context item type - component (object, Tag or Asset or Attribute): component the item is linked to - keywords (list[str]): list of keywords linked to the item - created_by (object, User): user that created the item - created_at (datetime64[us, client timezone]): creation date - last_modified: (datetime64[us, client timezone]): last modified date Field columns: There will be a column for every unique field. Values will be float or str. The column name will be the unique field key (not the field name!) If the field is not present on some of the items, the corresponding values will be nan. Note that for context items that were created by monitors, the following metadata fields will be present (but hidden in the TrendMiner UI): - tm_monitor_id (str): Monitor.identifier short ID - tm_search_id (str): SearchBase.identifier UUID - tm_search_type (str): 'valuebased', 'similarity', ... Event columns: All context item events besides of the start and end events will be added as datetime64[ns, client timezone] columns, with the event name as the column name. |

Notes

Context items linked to multiple components are not supported. Only the first component will be returned.

Duplicate column names can occur when a certain event state occurs more than once, or when there is an overlap between field keys, state names and/or metadata column names. It is advised to avoid this situation as this will complicate processing of the resulting DataFrame.

### delete_items

```
delete_items() -> None
```

Delete context items based on the definition filters

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
