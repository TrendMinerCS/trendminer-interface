## trendminer_interface.objects.ValueBasedSearch

Bases: `BaseSearch`

Value based search work organizer object

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
definition: ValueBasedSearchDefinition
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
    tuple[User | UserGroup, WorkSharePermission]
]
```

Get the sharing settings of the object

Returns:

| Name      | Type                | Description                          |
| --------- | ------------------- | ------------------------------------ |
| `sharing` | \`list\[tuple\[User | UserGroup, WorkSharePermission\]\]\` |

### add_permission

```
add_permission(
    subject: User | UserGroup,
    permission: WorkSharePermission,
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

### get_monitor

```
get_monitor() -> Monitor
```

Get the monitor corresponding to the item

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
