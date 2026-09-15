# `client.user`

## trendminer_interface.\_client.user.UserFacade

Facade for user related operations in TrendMiner.

### group

```
group: UserGroupFacade
```

Facade for user group related operations in TrendMiner.

### self

```
self: User
```

Get the currently authenticated user

Returns:

| Name   | Type   | Description                      |
| ------ | ------ | -------------------------------- |
| `self` | `User` | The currently authenticated user |

### from_identifier

```
from_identifier(identifier: str) -> User
```

Get a user by their identifier

Parameters:

| Name         | Type  | Description      | Default    |
| ------------ | ----- | ---------------- | ---------- |
| `identifier` | `str` | UUID of the user | *required* |

Returns:

| Type   | Description                                   |
| ------ | --------------------------------------------- |
| `User` | User corresponding to the provided identifier |

Raises:

| Type               | Description                                  |
| ------------------ | -------------------------------------------- |
| `ResourceNotFound` | If no user with the given identifier exists. |

### from_name

```
from_name(name: str) -> User
```

Get a user by their name

Parameters:

| Name   | Type  | Description      | Default    |
| ------ | ----- | ---------------- | ---------- |
| `name` | `str` | Name of the user | *required* |

Returns:

| Type   | Description                             |
| ------ | --------------------------------------- |
| `User` | User corresponding to the provided name |

Raises:

| Type                | Description                             |
| ------------------- | --------------------------------------- |
| `ResourceNotFound`  | If no user with the given name exists.  |
| `AmbiguousResource` | If multiple users match the given name. |

### all_client_users

```
all_client_users(page=0, size=10000) -> PagedList[User]
```

Get all client users

Client users are service accounts for OAuth clients. They have a username of the form `service-account-{client id}`

Parameters:

| Name   | Type  | Description                                                                                   | Default |
| ------ | ----- | --------------------------------------------------------------------------------------------- | ------- |
| `page` | `int` | Page number of results to return. By default, start at the first page of results (0-indexed). | `0`     |
| `size` | `int` | Number of results to return per page.                                                         | `10000` |

Returns:

| Type              | Description                        |
| ----------------- | ---------------------------------- |
| `PagedList[User]` | Paginated list of all client users |

### search

```
search(
    query: str, page: int = 0, size: int = 10000
) -> PagedList[User]
```

Search users by a query string

Parameters:

| Name    | Type  | Description                                                                                               | Default    |
| ------- | ----- | --------------------------------------------------------------------------------------------------------- | ---------- |
| `query` | `str` | Query string to search for in username, first name, last name, and email. Supports wildcard character \*. | *required* |
| `page`  | `int` | Page number of results to return. By default, start at the first page of results (0-indexed).             | `0`        |
| `size`  | `int` | Number of results to return per page.                                                                     | `10000`    |

Returns:

| Type              | Description                                |
| ----------------- | ------------------------------------------ |
| `PagedList[User]` | Paginated list of users matching the query |

Notes

There is no endpoint for searching users by a specific property (e.g. username)

Client users cannot be retrieved by this method. They can be retrieved by their exact name (`service-account-{client id}`) using the `.from_name` method.

Searching for a first or last name with a string that includes spaces does not work.
