## trendminer_interface.objects.Datasource

Tag datasource

### identifier

```
identifier: str
```

Datasource identifier

### name

```
name: str
```

Datasource name

### description

```
description: str
```

Datasource description

### capabilities

```
capabilities: list[str]
```

Capability types, e.g. TIME_SERIES

### raw

```
raw: bool
```

Whether the datasource only supports raw values (plots index points only, even when zooming in).

### granularity

```
granularity: Timedelta
```

Chunk size for historic indexing

### source_type

```
source_type: str
```

Datasource type

### created_at

```
created_at: Timestamp
```

Date the datasource was created

### synced_at

```
synced_at: Timestamp
```

Last synced date for the datasource

### builtin

```
builtin: bool
```

Whether the datasource is one of the fixed appliance datasources (e.g., Formula tags)
