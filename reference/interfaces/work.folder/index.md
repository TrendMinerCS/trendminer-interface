# `client.work.folder`

## trendminer_interface.\_client.work.folder.FolderFacade

Facade for getting saved folders in the work organizer

### create

```
create(name: str, folder: Folder | None = None) -> Folder
```

Create a folder in the work organizer

Parameters:

| Name     | Type     | Description                                                                                                                          | Default    |
| -------- | -------- | ------------------------------------------------------------------------------------------------------------------------------------ | ---------- |
| `name`   | `str`    | The name of the folder to create                                                                                                     | *required* |
| `folder` | `Folder` | The parent folder in which to create the new folder. If None (default), the new folder is created in the root of the work organizer. | `None`     |

Returns:

| Type     | Description        |
| -------- | ------------------ |
| `Folder` | The created folder |

### from_identifier

```
from_identifier(identifier: str) -> Folder
```

Get a folder by its unique identifier

Parameters:

| Name         | Type  | Description                                | Default    |
| ------------ | ----- | ------------------------------------------ | ---------- |
| `identifier` | `str` | The unique identifier of the folder to get | *required* |

Returns:

| Type     | Description                          |
| -------- | ------------------------------------ |
| `Folder` | The folder with the given identifier |

Raises:

| Type               | Description                                    |
| ------------------ | ---------------------------------------------- |
| `ResourceNotFound` | If no folder with the given identifier exists. |

### from_path

```
from_path(
    names: list[str], user: User | None = None
) -> Folder
```

Get a folder by its path in the work organizer, starting from a user home folder

Parameters:

| Name    | Type        | Description                                                                                                                                                                                                                                   | Default    |
| ------- | ----------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------- |
| `names` | `List[str]` | The path of folder names to the target folder, e.g.['MyFolder', 'MySubfolder', 'MyTargetFolder']                                                                                                                                              | *required* |
| `user`  | `User`      | The owner of the folder to retrieve. Path browsing will start from this user's work organizer. By default, the authenticated user's work organizer is parsed. Parsing another user's work organizer requires system administrator privileges. | `None`     |

Returns:

| Type     | Description                    |
| -------- | ------------------------------ |
| `Folder` | The folder with the given path |

Raises:

| Type                | Description                                 |
| ------------------- | ------------------------------------------- |
| `ResourceNotFound`  | If a folder in the path does not exist.     |
| `AmbiguousResource` | If a path segment matches multiple folders. |

Examples:

```
>>> client.work.folder.from_path(["MyFolder", "MySubfolder"])
```

### from_name

```
from_name(
    name: str, scope: WorkScope = "my work"
) -> Folder
```

Get a folder from its name

Parameters:

| Name    | Type        | Description                                                                                                                                                                                                                                                                                                                                         | Default     |
| ------- | ----------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------- |
| `name`  | `str`       | The name of the folder to get                                                                                                                                                                                                                                                                                                                       | *required*  |
| `scope` | `WorkScope` | Searching scope for getting the folder. - 'my work': The authenticated work organizer (default) - 'shared': Another user's work shared to the authenticated user - 'favorites': The authenticated user's favorites, which can include items from own work and shared items. - 'system': Any user's work. Only accessible for system administrators. | `'my work'` |

Returns:

| Type     | Description                    |
| -------- | ------------------------------ |
| `Folder` | The folder with the given name |

Raises:

| Type                | Description                                           |
| ------------------- | ----------------------------------------------------- |
| `ResourceNotFound`  | If no folder with the given name exists in the scope. |
| `AmbiguousResource` | If multiple folders match the given name.             |

### search

```
search(
    query: str | None = None,
    scope: WorkScope = "my work",
    page: int = 0,
    size: int = 2000,
) -> PagedList[Folder]
```

Search folders by name or description

Parameters:

| Name    | Type        | Description                                                                                                                                                                                                                                                                                                                  | Default     |
| ------- | ----------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------- |
| `query` | `str`       | The search query. The '\*' can be used as a wildcard. Returns all folders if query is None (default).                                                                                                                                                                                                                        | `None`      |
| `scope` | `WorkScope` | Searching scope. - 'my work': The authenticated work organizer (default) - 'shared': Another user's work shared to the authenticated user - 'favorites': The authenticated user's favorites, which can include items from own work and shared items. - 'system': Any user's work. Only accessible for system administrators. | `'my work'` |
| `page`  | `int`       | Page number of results to return. By default, start at the first page of results (0-indexed).                                                                                                                                                                                                                                | `0`         |
| `size`  | `int`       | Number of results to return per page.                                                                                                                                                                                                                                                                                        | `2000`      |

Returns:

| Name      | Type                | Description                                         |
| --------- | ------------------- | --------------------------------------------------- |
| `folders` | `PagedList[Folder]` | Paginated list of folders matching the search query |

### get_user_home

```
get_user_home(user: User) -> Folder
```

System administrator method to get the home folder of a given user

Parameters:

| Name   | Type   | Description                                                                                                              | Default    |
| ------ | ------ | ------------------------------------------------------------------------------------------------------------------------ | ---------- |
| `user` | `User` | The user for whom to get the home folder. Accessing another user's home folder requires system administrator privileges. | *required* |

Returns:

| Type     | Description                       |
| -------- | --------------------------------- |
| `Folder` | The home folder of the given user |

### get_users_root

```
get_users_root() -> Folder
```

System administrator method to get the `Users` root folder which contains all user home folders

Returns:

| Type     | Description           |
| -------- | --------------------- |
| `Folder` | The Users root folder |
