# `client_from_credentials`

## trendminer_interface.client_from_credentials

```
client_from_credentials(
    url: str,
    client_id: str,
    client_secret: str,
    username: str | None = None,
    password: str | None = None,
    tz: ZoneInfo | str = ZoneInfo("UTC"),
    verify: bool = True,
    timeout: float | tuple[float, float] = (10, 120),
    transport: BaseTransport | None = None,
    check_version: bool = True,
) -> TrendMinerClient
```

Create a TrendMinerClient from credentials

Providing client id and client secret leads to client authentication. The resulting client will have the permissions of that client user. To authenticate as a specific user, username and password need to be provided. The resulting permissions will be of that user, ignoring any permissions linked to the client id.

Some functions may require admin permissions. Only actual users can have these permissions.

Credentials are validated immediately: the client authenticates with the appliance as it is created, so invalid credentials raise straight away rather than on first use. When `username` is given, `password` must be given as well.

Parameters:

| Name            | Type              | Description                                                                                                                                                                         | Default     |
| --------------- | ----------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------- |
| `url`           | `str`             | TrendMiner appliance url                                                                                                                                                            | *required*  |
| `client_id`     | `str`             | Valid client id for the given appliance.                                                                                                                                            | *required*  |
| `client_secret` | `str`             | Client secret matching the given client id.                                                                                                                                         | *required*  |
| `username`      | `str`             | Setting username provides access to the resources of this user (e.g., saved items). Requires password to be set as well. Only works for local users, not for SSO (LDAP/SAML) users. | `None`      |
| `password`      | `str`             | Password matching the given username.                                                                                                                                               | `None`      |
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

| Type              | Description                                                                                                            |
| ----------------- | ---------------------------------------------------------------------------------------------------------------------- |
| `HTTPStatusError` | If the appliance rejects the credentials during the initial token request performed while the client is being created. |

See Also

client_from_refresh_token : Authenticate an SSO user from a browser-obtained refresh token. client_from_env : Authenticate from a host-provided token (MLHub notebooks, Custom Calculations). client_with_bearer_auth : Authenticate with a caller-supplied token provider.

Examples:

Authenticating as a client user:

```
>>> from trendminer_interface import client_from_credentials
>>> client = client_from_credentials(
...     url="https://your.trendminer.cloud",
...     client_id="your-client",
...     client_secret="...",  # load from a .env file or keyring, never hard-code
... )
```

Authenticating as a local user with custom timezone:

```
>>> client = client_from_credentials(
...     url="https://your.trendminer.cloud",
...     client_id="your-client",
...     client_secret="...",  # load from a .env file or keyring, never hard-code
...     username="jane.doe",
...     password="...",       # load from a .env file or keyring, never hard-code
...     tz="Europe/Brussels",
... )
```
