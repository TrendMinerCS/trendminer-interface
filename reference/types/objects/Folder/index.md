## trendminer_interface.objects.Folder

Bases: `SavedItemBase`

Work organizer folder

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

### definition

```
definition: Any = definition
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

### update

```
update() -> Folder
```

Update the folder in the TrendMiner work organizer to match the current instance state

### search_contents

```
search_contents(
    content_type: type[SavedItem] | None = None,
    page: int = 0,
    size: int = 2000,
) -> PagedList[SavedItem]
```

Search items saved in this folder

Parameters:

| Name           | Type              | Description                                                                                   | Default |
| -------------- | ----------------- | --------------------------------------------------------------------------------------------- | ------- |
| `content_type` | `type[SavedItem]` | Type of items to get. If None, items of all types are returned.                               | `None`  |
| `page`         | `int`             | Page number of results to return. By default, start at the first page of results (0-indexed). | `0`     |
| `size`         | `int`             | Number of results to return per page.                                                         | `2000`  |

Returns:

| Type                   | Description                                                    |
| ---------------------- | -------------------------------------------------------------- |
| `PagedList[SavedItem]` | Paginated list of items of the given type saved in this folder |

### get_item

```
get_item(
    name: str, content_type: type[SavedItem]
) -> SavedItem
```

Get item with the given name and type saved in this folder

Parameters:

| Name           | Type              | Description              | Default    |
| -------------- | ----------------- | ------------------------ | ---------- |
| `name`         | `str`             | Name of the item to get  | *required* |
| `content_type` | `type[SavedItem]` | Type of the item to get. | *required* |

Returns:

| Name   | Type        | Description                                                |
| ------ | ----------- | ---------------------------------------------------------- |
| `item` | `SavedItem` | The item with the given name and type saved in this folder |

Raises:

| Type                | Description                                                    |
| ------------------- | -------------------------------------------------------------- |
| `ResourceNotFound`  | If no item with the given name and type exists in this folder. |
| `AmbiguousResource` | If multiple items match.                                       |
