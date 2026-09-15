# `client.user.group`

## trendminer_interface.\_client.user.group.UserGroupFacade

Facade for user group related operations in TrendMiner.

### everyone

```
everyone: UserGroup
```

Group representing all TrendMiner users

This group is always present. It has a fixed identifier and name.

Returns:

| Name       | Type        | Description                                                                                                      |
| ---------- | ----------- | ---------------------------------------------------------------------------------------------------------------- |
| `everyone` | `UserGroup` | Group representing all TrendMiner users, with: - identifier: "99999999-9999-9999-9999-999999999999" - name: "\*" |

Notes

This group is not retrievable from its identifier or name.

### from_identifier

```
from_identifier(identifier: str) -> UserGroup
```

Get a user group by its identifier

Parameters:

| Name         | Type  | Description            | Default    |
| ------------ | ----- | ---------------------- | ---------- |
| `identifier` | `str` | UUID of the user group | *required* |

Returns:

| Type        | Description                                         |
| ----------- | --------------------------------------------------- |
| `UserGroup` | User group corresponding to the provided identifier |

Raises:

| Type               | Description                                        |
| ------------------ | -------------------------------------------------- |
| `ResourceNotFound` | If no user group with the given identifier exists. |

### from_name

```
from_name(name: str) -> UserGroup
```

Get a user group by its name

Parameters:

| Name   | Type  | Description            | Default    |
| ------ | ----- | ---------------------- | ---------- |
| `name` | `str` | Name of the user group | *required* |

Returns:

| Type        | Description                                   |
| ----------- | --------------------------------------------- |
| `UserGroup` | User group corresponding to the provided name |

Raises:

| Type                | Description                                   |
| ------------------- | --------------------------------------------- |
| `ResourceNotFound`  | If no user group with the given name exists.  |
| `AmbiguousResource` | If multiple user groups match the given name. |

### search

```
search(
    name: str, page: int = 0, size: int = 10000
) -> PagedList[UserGroup]
```

Search for user groups by name

Parameters:

| Name   | Type  | Description                                                                                   | Default    |
| ------ | ----- | --------------------------------------------------------------------------------------------- | ---------- |
| `name` | `str` | Partial name to search for. Wildcard character (\*) is not supported.                         | *required* |
| `page` | `int` | Page number of results to return. By default, start at the first page of results (0-indexed). | `0`        |
| `size` | `int` | Number of results to return per page.                                                         | `10000`    |

Returns:

| Type                   | Description                                                |
| ---------------------- | ---------------------------------------------------------- |
| `PagedList[UserGroup]` | Paginated list of user groups matching the search criteria |
