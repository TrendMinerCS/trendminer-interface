# `client_from_env`

## trendminer_interface.client_from_env

```
client_from_env(
    tz: ZoneInfo | str = ZoneInfo("UTC"),
    verify: bool = True,
    timeout: float | tuple[float, float] = (10, 120),
    transport: BaseTransport | None = None,
) -> TrendMinerClient
```

Create a TrendMinerClient from environmental variables

Reads an access token from `KERNEL_USER_TOKEN` (set inside MLHub notebooks) or, if that is not set, `ACCESS_TOKEN` (set for Custom Calculations). The token is re-read from the environment on every request, so a token rotated by the host is picked up automatically. The appliance URL is derived from the token itself.

Unlike the other factories, no appliance version check is performed — that responsibility is left to the embedding application, whose SDK and appliance versions are expected to match.

Parameters:

| Name        | Type              | Description                                                                                                                                   | Default     |
| ----------- | ----------------- | --------------------------------------------------------------------------------------------------------------------------------------------- | ----------- |
| `tz`        | `str or ZoneInfo` | Client timezone. All time outputs given in client timezone. All inputs without explicit timezone are considered to be in the client timezone. | `UTC`       |
| `verify`    | `bool`            | Sets verify parameter for the requests to appliance. Setting to False prevents SSLError in case appliance SSL certificates are not valid.     | `True`      |
| `timeout`   | `float or tuple`  | Timeout settings for requests.                                                                                                                | `(10, 120)` |
| `transport` | `BaseTransport`   | Custom httpx transport for the underlying httpx.Client.                                                                                       | `None`      |

Returns:

| Type               | Description |
| ------------------ | ----------- |
| `TrendMinerClient` |             |

Raises:

| Type         | Description                                                              |
| ------------ | ------------------------------------------------------------------------ |
| `ValueError` | If neither KERNEL_USER_TOKEN nor ACCESS_TOKEN is set in the environment. |

See Also

client_with_bearer_auth : Supply the token through a callable instead of the environment.

Examples:

```
>>> from trendminer_interface import client_from_env
>>> client = client_from_env()  # inside an MLHub notebook or Custom Calculation
```
