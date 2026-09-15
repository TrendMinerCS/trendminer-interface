# `TrendMinerClient`

## trendminer_interface.\_client.TrendMinerClient

Handles authentication to, and interaction with the TrendMiner appliance.

This class is the sole entry point for users of this library. It provides access to the retrieval and instantiation of all other objects, and handles authentication and session management.

Attributes:

| Name      | Type       | Description                                                                                                                                                   |
| --------- | ---------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `tz`      | `ZoneInfo` | Client timezone. All time outputs given in client timezone. All inputs without explicit timezone are considered to be in the client timezone.                 |
| `session` | `Client`   | Session object for making requests to the TrendMiner appliance. This session is shared across all objects created by this client, and handles authentication. |

### SUPPORTED_VERSIONS

```
SUPPORTED_VERSIONS: tuple[str, ...] = (
    "2026.R1.0",
    "2026.R2.0",
)
```

### session

```
session: Client = session
```

### tz

```
tz: ZoneInfo = tz
```

### url

```
url: str
```

Base URL of the TrendMiner appliance

### appliance

```
appliance: ApplianceFacade
```

Facade to TrendMiner appliance information

### asset_framework

```
asset_framework: AssetFrameworkFacade
```

Facade to interact with the asset framework

### context

```
context: ContextFacade
```

Facade to interact with context hub

### dashboard

```
dashboard: DashboardFacade
```

Facade to interact with dashboards

### datasource

```
datasource: DatasourceFacade
```

Facade to interact with tag datasources

### filter

```
filter: FilterFacade
```

Facade to interact with filters

### fingerprint

```
fingerprint: FingerprintFacade
```

Facade to interact with fingerprints

### monitor

```
monitor: MonitorFacade
```

Facade to interact with monitors

### notebook

```
notebook: NotebookFacade
```

Facade to interact with notebooks

### search

```
search: SearchFacade
```

Facade to interact with searches

### tag

```
tag: TagFacade
```

Facade to interact with tags

### tag_builder

```
tag_builder: TagBuilderFacade
```

Facade to build tags without instantiating them first

### trend

```
trend: TrendFacade
```

Facade to interact with trend hub

### user

```
user: UserFacade
```

Facade to interact with users

### work

```
work: WorkFacade
```

Facade to interact with the work organizer
