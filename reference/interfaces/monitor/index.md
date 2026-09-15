# `client.monitor`

## trendminer_interface.\_client.monitor.MonitorFacade

Facade for retrieving monitors

Notes

Retrieving a monitor by name is not supported. You must first retrieve the search or fingerprint by its name, and then call `get_monitor` on that object.

### from_identifier

```
from_identifier(identifier: int) -> Monitor
```

Retrieve monitor from identifier

Parameters:

| Name         | Type  | Description        | Default    |
| ------------ | ----- | ------------------ | ---------- |
| `identifier` | `int` | Monitor identifier | *required* |

Returns:

| Type      | Description                           |
| --------- | ------------------------------------- |
| `Monitor` | The monitor with the given identifier |

Raises:

| Type               | Description                                     |
| ------------------ | ----------------------------------------------- |
| `ResourceNotFound` | If no monitor with the given identifier exists. |

### get_overview

```
get_overview(
    since: Timestamp | str | None = None,
) -> DataFrame
```

Get an overview of the number of hits for all active monitors

Parameters:

| Name    | Type               | Description                                                                               | Default |
| ------- | ------------------ | ----------------------------------------------------------------------------------------- | ------- |
| `since` | `Timestamp or str` | The start date from when to count the number of monitor results (up to the current date). | `None`  |

Returns:

| Type        | Description                                              |
| ----------- | -------------------------------------------------------- |
| `DataFrame` | DataFrame with columns 'monitor' and 'number_of_results' |

### search

```
search(
    user: User | None = None, active_only: bool = True
) -> list[Monitor]
```

Search for monitors

Parameters:

| Name          | Type   | Description                                                                                                                                        | Default |
| ------------- | ------ | -------------------------------------------------------------------------------------------------------------------------------------------------- | ------- |
| `user`        | `User` | User for which to retrieve the monitors. If not provided, monitors for the currently authenticated user are retrieved.                             | `None`  |
| `active_only` | `bool` | Whether only the currently active monitors need to be retrieved, otherwise a monitor is retrieved for every search that is implemented in the SDK. | `True`  |

Returns:

| Type              | Description               |
| ----------------- | ------------------------- |
| `list of Monitor` | List of Monitor instances |

Notes

Contrary to other search methods, this method does NOT result in a paginated list as the underlying endpoint is not paginated.
