# Getting started

## Authentication

All interactions with your TrendMiner server will run through an authenticated [`TrendMinerClient`](https://trendminercs.github.io/trendminer-interface/reference/types/TrendMinerClient/index.md) instance. All methods for retrieval of objects and creation of new objects will branch from this instance.

Typically, you will authenticate a client instance directly from credentials. The following will authenticate you as a client user. For more details on authentication and client creation, refer to [creating a client](https://trendminercs.github.io/trendminer-interface/creating-a-client/index.md).

```
from trendminer_interface import client_from_credentials

client = client_from_credentials(
    url="https://training.trendminer.cloud",
    client_id="clientuser",
    client_secret="GdYDrRef3hwdshIJwj3e3IsiUJqigVxZ",
)
```

Note that the credentials above are only for illustration, and that it is insecure to hard-code secrets and passwords directly in your code. Use a `.env` file or a [keyring service](https://pypi.org/project/keyring/) instead.

## The client as entry point

Once we have our authenticated [`TrendMinerClient`](https://trendminercs.github.io/trendminer-interface/reference/types/TrendMinerClient/index.md) instance, we can start interacting with TrendMiner. For example, we can search for some tags.

```
import pandas as pd

tag = client.tag.from_name("TM_Hour_UTC")
print(tag)
```

Output

```
2026-01-01 00:00:00+00:00    0.0
2026-01-01 01:00:00+00:00    1.0
2026-01-01 02:00:00+00:00    2.0
2026-01-01 03:00:00+00:00    3.0
2026-01-01 04:00:00+00:00    4.0
Freq: h, Name: value, dtype: float64
```

Once authenticated, you can retrieve and create tags, work organizer items, context items, ... all from your `client`. For a full overview of methods available from the client, refer to [Interface tree](https://trendminercs.github.io/trendminer-interface/reference/interface-tree/index.md).

## Getting to work

After exploring how to [create the correct type of client](https://trendminercs.github.io/trendminer-interface/creating-a-client/index.md), the easiest way to get started is to check the [Examples](https://trendminercs.github.io/trendminer-interface/examples/index.md) section for snippets similar to your use cases. The [Interface tree](https://trendminercs.github.io/trendminer-interface/reference/interface-tree/index.md) overview should give you an idea on what functionalities are available in the SDK. You can dive into class details from this page, or navigate through the [Objects & Types](https://trendminercs.github.io/trendminer-interface/objects-and-types/index.md) section directly.

For examples of fully fleshed-out use cases, you can check the [Use cases](https://trendminercs.github.io/trendminer-interface/use-cases/index.md) section.
