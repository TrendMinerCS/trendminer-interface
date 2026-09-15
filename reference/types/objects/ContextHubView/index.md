## trendminer_interface.objects.ContextHubView

Bases: `SavedItemBase`

ContextHub view work organizer object

### name

```
name: str = name
```

### description

```
description: str = description
```

### folder

```
folder: Folder | None = folder
```

### identifier

```
identifier: str
```

UUID of the saved object

### created_at

```
created_at: Timestamp | None
```

Timestamp the object was created at

Can be None for items created before item creation date tracking was implemented in TrendMiner.

### last_modified

```
last_modified: Timestamp
```

Timestamp the object was last modified

### last_used

```
last_used: Timestamp
```

Timestamp the object was last used

### last_modified_by

```
last_modified_by: User
```

User that last modified the object

### owner

```
owner: User
```

User that owns the object

### shared

```
shared: bool
```

Whether the object is shared with other users

### favorite

```
favorite: bool
```

Whether the object is marked as a favorite by the owner

### version

```
version: int
```

Version number of the object, incremented on each modification

### definition

```
definition: ContextHubViewDefinition
```

### update

```
update() -> Self
```

Update the saved item in TrendMiner to match the current instance state

### delete

```
delete() -> None
```

Permanently delete the saved item in TrendMiner

### move

```
move(folder: Folder) -> None
```

Move the item to a folder

Parameters:

| Name     | Type     | Description                    | Default    |
| -------- | -------- | ------------------------------ | ---------- |
| `folder` | `Folder` | The folder to move the item to | *required* |

Notes

Moving an item to another user's folder will not transfer the ownership and may lead to unexpected behavior. Use the client.work.transfer method instead.

### get_folder_path

```
get_folder_path(include_home=False) -> list[Folder]
```

Get the location in the work organizer

Starts from, but does not include, the user's home folder. Does not include the object itself.

Parameters:

| Name           | Type   | Description                                                                                                                                                           | Default |
| -------------- | ------ | --------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------- |
| `include_home` | `bool` | Whether to include the user's home folder as the first element of the returned list. If False (default), the list starts from the first folder after the home folder. | `False` |

Returns:

| Type           | Description                             |
| -------------- | --------------------------------------- |
| `list[Folder]` | List of folders leading up to this item |

### get_permissions

```
get_permissions() -> list[
    tuple[User | UserGroup, SharePermission]
]
```

Get the sharing settings of the object

Returns:

| Name      | Type                | Description                      |
| --------- | ------------------- | -------------------------------- |
| `sharing` | \`list\[tuple\[User | UserGroup, SharePermission\]\]\` |

### add_permission

```
add_permission(
    subject: User | UserGroup, permission: SharePermission
) -> Self
```

Share the object with a user or user group

Parameters:

| Name         | Type                | Description                                                       | Default    |
| ------------ | ------------------- | ----------------------------------------------------------------- | ---------- |
| `subject`    | `User or UserGroup` | The user or user group to share the object with                   | *required* |
| `permission` | `str`               | The permission to share with. Can be "read", "write", or "manage" | *required* |

Returns:

| Name   | Type            | Description                                                                                                                |
| ------ | --------------- | -------------------------------------------------------------------------------------------------------------------------- |
| `self` | `SavedItemBase` | The object itself, after being shared with the user or user group. Practically, only the shared property may have changed. |

### remove_permission

```
remove_permission(subject: User | UserGroup) -> Self
```

Remove sharing of the object with a user or user group

Parameters:

| Name      | Type                | Description                                   | Default    |
| --------- | ------------------- | --------------------------------------------- | ---------- |
| `subject` | `User or UserGroup` | The user or user group to remove sharing with | *required* |

Returns:

| Name   | Type            | Description                                                                                                                    |
| ------ | --------------- | ------------------------------------------------------------------------------------------------------------------------------ |
| `self` | `SavedItemBase` | The object itself, after removing sharing with the user or user group. Practically, only the shared property may have changed. |

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

| Name     | Type                  | Description                                                                                                                                                                                                                                                                                                                                                                   | Default                                                                                                                                                                                                                     |
| -------- | --------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `target` | \`Interval[Timestamp] | DataFrame\`                                                                                                                                                                                                                                                                                                                                                                   | The input intervals to search for. Can be either a single pandas Interval or a DataFrame with IntervalIndex containing non-overlapping intervals. The closed property of the target will be retained in the search results. |
| `drop`   | `bool`                | Whether to drop the original interval columns from the resulting DataFrame, by default True. If False, the original interval in which each search result was found will be kept as a column in the resulting DataFrame. For a pd.Interval input, the name of this column will be search_interval. For a DataFrame input, the name of the original IntervalIndex will be kept. | `True`                                                                                                                                                                                                                      |
| `page`   | `int`                 | The page number of results to retrieve. Default is 0 (the first page).                                                                                                                                                                                                                                                                                                        | `0`                                                                                                                                                                                                                         |
| `size`   | `int`                 | The number of results to include in each page. Default is 10000.                                                                                                                                                                                                                                                                                                              | `10000`                                                                                                                                                                                                                     |

Returns:

| Type             | Description                                                                                           |
| ---------------- | ----------------------------------------------------------------------------------------------------- |
| `PagedDataFrame` | Page containing DataFrame with IntervalIndex and columns corresponding to the calculations specified. |

Notes

Any columns already present in an input DataFrame will be kept. Their values will be mapped to the search results based on the intervals in which the search results were found.

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

Delete context items based on the view definition filters
