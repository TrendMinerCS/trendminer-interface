# `client_with_bearer_auth`

## trendminer_interface.client_with_bearer_auth

```
client_with_bearer_auth(
    access_token_provider: Callable[[], str],
    server_url: str,
    tz: ZoneInfo | str = ZoneInfo("UTC"),
    verify: bool = True,
    timeout: float | tuple[float, float] = (10, 120),
    transport: BaseTransport | None = None,
) -> TrendMinerClient
```

Create a TrendMinerClient authenticated with a bearer token.

Use this when embedding the SDK into an application that manages its own authentication. The SDK does not cache, refresh, or track the expiry of the token — `access_token_provider` is called on every request and is fully responsible for returning a currently-valid token (for example by caching and refreshing internally). Because no token exchange happens up front, an invalid token surfaces only on the first request, as an `AuthenticationError`.

Parameters:

| Name                    | Type                | Description                                                                                                                                   | Default     |
| ----------------------- | ------------------- | --------------------------------------------------------------------------------------------------------------------------------------------- | ----------- |
| `access_token_provider` | `Callable[[], str]` | Zero-argument callable that returns a currently-valid access token string. Called on every request, so it should be cheap and thread-safe.    | *required*  |
| `server_url`            | `str`               | Base URL of the TrendMiner appliance.                                                                                                         | *required*  |
| `tz`                    | `str or ZoneInfo`   | Client timezone. All time outputs given in client timezone. All inputs without explicit timezone are considered to be in the client timezone. | `UTC`       |
| `verify`                | `bool`              | Sets verify parameter for the requests to appliance. Setting to False prevents SSLError in case appliance SSL certificates are not valid.     | `True`      |
| `timeout`               | `float or tuple`    | Timeout settings for requests.                                                                                                                | `(10, 120)` |
| `transport`             | `BaseTransport`     | Custom httpx transport for the underlying httpx.Client.                                                                                       | `None`      |

Returns:

| Type               | Description |
| ------------------ | ----------- |
| `TrendMinerClient` |             |

See Also

client_from_env : Read the token from the environment instead of a callable. client_from_refresh_token : Let the SDK manage token refresh from a refresh token.
