# `client.context.item`

## trendminer_interface.\_client.context.item.ContextItemFacade

Facade for managing context items in TrendMiner

Context items are always represented as a pandas DataFrame, where each row corresponds to a context item.

### create

```
create(items: DataFrame) -> None
```

Create new context items from a valid DataFrame.

Parameters:

| Name    | Type        | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     | Default    |
| ------- | ----------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------- |
| `items` | `DataFrame` | Input DataFrame with a pandas.IntervalIndex and the following structure: Index: The index will be a pandas.IntervalIndex, with index.left and index.right the timestamps of the context item start and end events, respectively. Required columns: - type (ContextType): context type of each item - component (Tag or Asset or Attribute): component to which the item will be attached Optional columns: - open (bool): whether the context item is open-ended (no end state). Default behavior is closed. - keywords (list[str]): the keywords to attach to the context item - description (str): the context item description Event columns: Additional pandas.Timestamp values will be considered additional states (events) with the column name as the state name. Field columns: Any remaining numeric or string values will be considered context fields with the column name as the key. The following metadata columns will be ignored: key, identifier, identifier_external, created_by, created_at, last_modified. | *required* |

Returns:

| Type   | Description                                                                                                                                                               |
| ------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `None` | No output is returned. To load the created context items (with their metadata such as identifiers), use get_items on a ContextHubViewDefinition with appropriate filters. |

Notes

If a DataFrame of existing context items is passed, copies of these context items will be created.

### update

```
update(items: DataFrame) -> None
```

Update existing context items to a new state

Parameters:

| Name    | Type        | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     | Default    |
| ------- | ----------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------- |
| `items` | `DataFrame` | Input DataFrame with a pandas.IntervalIndex and the following structure: Index: The index will be a pandas.IntervalIndex, with index.left and index.right the timestamps of the context item start and end events, respectively. Required columns: - identifier (str): identifier of the existing context item - type (ContextType): context type of each item - component (Tag or Asset or Attribute): component to which the item will be attached Optional columns: - open (bool): whether the context item is open-ended (no end state). Default behavior is closed. - keywords (list[str]): the keywords to attach to the context item - description (str): the context item description Event columns: Additional pandas.Timestamp values will be considered additional states (events) with the column name as the state name. Field columns: Any remaining numeric or string values will be considered context fields with the column name as the key. The following metadata columns will be ignored: key, identifier_external, created_by, created_at, last_modified. | *required* |

Returns:

| Type   | Description |
| ------ | ----------- |
| `None` |             |

### delete

```
delete(items: DataFrame) -> None
```

Permanently delete all context items in the DataFrame
