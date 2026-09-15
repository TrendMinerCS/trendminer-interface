# `client_from_refresh_token`

## trendminer_interface.client_from_refresh_token

```
client_from_refresh_token(
    refresh_token: str,
    client_id: str,
    client_secret: str,
    tz: ZoneInfo | str = ZoneInfo("UTC"),
    verify: bool = True,
    timeout: float | tuple[float, float] = (10, 120),
    transport: BaseTransport | None = None,
    check_version: bool = True,
) -> TrendMinerClient
```

Create a TrendMinerClient from a refresh token

Intended use case is to run automations for SSO-based users, who cannot use the password grant type. The refresh token can be obtained by logging in to the TrendMiner appliance via the browser, opening the developer tools, and copying the refresh token.

A client ID and client secret are still required, but the resulting client will have the permissions of the user linked to the refresh token. The appliance URL is taken from the token itself, so no `url` argument is needed.

Parameters:

| Name            | Type              | Description                                                                                                                                                                         | Default     |
| --------------- | ----------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------- |
| `refresh_token` | `str`             | Refresh token obtained from the TrendMiner appliance.                                                                                                                               | *required*  |
| `client_id`     | `str`             | Valid client id for the given appliance.                                                                                                                                            | *required*  |
| `client_secret` | `str`             | Client secret matching the given client id.                                                                                                                                         | *required*  |
| `tz`            | `str or ZoneInfo` | Client timezone. All time outputs given in client timezone. All inputs without explicit timezone are considered to be in the client timezone.                                       | `UTC`       |
| `verify`        | `bool`            | Sets verify parameter for the requests to appliance. Setting to False prevents SSLError in case appliance SSL certificates are not valid.                                           | `True`      |
| `timeout`       | `float or tuple`  | Timeout settings for requests.                                                                                                                                                      | `(10, 120)` |
| `transport`     | `BaseTransport`   | Custom httpx transport for the underlying httpx.Client.                                                                                                                             | `None`      |
| `check_version` | `bool`            | Whether to check if the TrendMiner appliance version is supported by this SDK version. If True, a warning is raised if the appliance version does not match the supported versions. | `True`      |

Returns:

| Type               | Description |
| ------------------ | ----------- |
| `TrendMinerClient` |             |

Raises:

| Type              | Description                                                                                                              |
| ----------------- | ------------------------------------------------------------------------------------------------------------------------ |
| `HTTPStatusError` | If the appliance rejects the refresh token during the initial token request performed while the client is being created. |

See Also

client_from_credentials : Authenticate a client user or local user from credentials.

Notes

The refresh token is rotated on every refresh: once the client refreshes, the token you originally copied from the browser is no longer valid. For long-running automations keep the client alive rather than recreating it from the same copied token.
