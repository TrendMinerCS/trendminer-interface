# Creating a client

Every interaction with TrendMiner starts from an authenticated `TrendMinerClient`. All retrieval and creation of objects branches from this instance — you never construct it directly, but obtain it through one of the factory functions below.

How a client authenticates depends on which factory you use. `client_from_credentials` and `client_from_refresh_token` perform an OAuth token exchange against your appliance and therefore need a **client id** and **client secret** (generated in ConfigHub by an administrator). `client_from_env` and `client_with_bearer_auth` instead receive a ready-made access token from the environment they run in, and perform no exchange of their own. In every case the client refreshes its access token transparently while it is in use.

## Which function should I use?

- **[`client_from_credentials`](https://trendminercs.github.io/trendminer-interface/creating-a-client/client_from_credentials/index.md)** — authenticate directly from credentials, and the most common starting point. With only a client id and secret you authenticate as the *client user*; add a `username` and `password` and you authenticate as that (local) user, taking on their permissions. Credentials are verified immediately, so a mistake surfaces the moment you create the client.
- **[`client_from_refresh_token`](https://trendminercs.github.io/trendminer-interface/creating-a-client/client_from_refresh_token/index.md)** — reuse an existing OAuth refresh token instead of a username and password. This is the way to run automations for SSO users, who cannot use the password grant. A client id and secret are still required; the appliance URL is read from the token itself.
- **[`client_from_env`](https://trendminercs.github.io/trendminer-interface/creating-a-client/client_from_env/index.md)** — read the access token directly from environment variables. The intended use case is embedded Python applications such as MLHub notebooks (`KERNEL_USER_TOKEN`) and Custom Calculations (`ACCESS_TOKEN`), where the host provides the token for you.
- **[`client_with_bearer_auth`](https://trendminercs.github.io/trendminer-interface/creating-a-client/client_with_bearer_auth/index.md)** — supply a callable that returns a bearer token. Use this when embedding the SDK into a custom application that implements its own authentication and already manages token retrieval and refresh.

## User types

Which factory you reach for is largely determined by *what kind of user* you are authenticating as.

### Client User

A client user is the service account behind an OAuth client (its username has the form `service-account-{client id}`). It is reachable only through the API — you cannot log in as a client user in the TrendMiner UI — and it cannot hold admin permissions. Like any user, it must be granted access to the relevant data sources in ConfigHub. A client user does have a work organizer, but because that work organizer is never accessible from the UI, a client user is best suited to retrieving data rather than saving work organizer items.

Authenticate as a client user with `client_from_credentials`, passing only the client id and secret.

### Local User

A local user is a user account created directly in TrendMiner, as opposed to one coming from an external identity provider. You authenticate as a local user with `client_from_credentials` by supplying a `username` and `password` **in addition to** the client id and secret. The resulting client carries that user's permissions — including admin permissions, which only real users can hold — regardless of the permissions attached to the client id.

Note that the password grant works for local users only: LDAP or SAML credentials cannot be used this way.

### OAuth User

An OAuth user signs in through an external identity provider (SSO / LDAP / SAML). Because only local users can log in with a username and password, an OAuth user cannot be authenticated with `client_from_credentials`. The only way to authenticate as an OAuth user is to log in through the browser and inject the resulting refresh token into your script with `client_from_refresh_token`. Treat this token as you would a password — keep it in a `.env` file rather than pasting it directly into the script.

## Robustness

An authenticated client refreshes its access token automatically while you use it. Through inactivity or prolonged use (on the order of a few hours), the underlying session will nonetheless eventually expire, at which point you need to authenticate again. The client never keeps sensitive information such as your password in memory.

For long-running scripts it is worth adding **automated retries**, so that a transient network hiccup or a momentarily overloaded appliance does not abort the whole run. Every factory accepts a `transport` argument, which is the injection point for a retry policy. The example below uses the third-party [`httpx-retries`](https://pypi.org/project/httpx-retries/) package (install it alongside the SDK):

```
from httpx_retries import Retry, RetryTransport
from trendminer_interface import client_from_credentials

retry = Retry(
    total=5,                                   # up to 5 retries per request
    backoff_factor=1,                          # exponential backoff between attempts
    status_forcelist=[429, 502, 503, 504],     # retry on rate-limit / gateway errors
    allowed_methods=["GET", "PUT", "DELETE", "POST"],
)

client = client_from_credentials(
    url="https://your.trendminer.cloud",
    client_id="your-client",
    client_secret="...",                       # load from a .env file or keyring
    transport=RetryTransport(retry=retry),
)
```

`status_forcelist` limits retries to transient responses — 429 (too many requests) and the 502/503/504 gateway errors — while `allowed_methods` opts even non-idempotent `POST` requests into the policy. Tune these to taste; the same `transport` argument works with every factory function.
