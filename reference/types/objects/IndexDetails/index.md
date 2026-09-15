## trendminer_interface.objects.IndexDetails

Tag indexing details

### tag

```
tag: Tag
```

The tag for which these index details apply.

### status

```
status: IndexStatus
```

The current status of the index.

Returns:

| Name     | Type  | Description                                                             |
| -------- | ----- | ----------------------------------------------------------------------- |
| `status` | `str` | "ok", "in progress", "out of date", "stale", "incomplete", or "dormant" |

### progress

```
progress: float
```

Tag historic indexing progress percentage (0-100).

### created_at

```
created_at: Timestamp
```

Timestamp the index was created at.

### last_modified

```
last_modified: Timestamp
```

Timestamp the index details were modified.

### last_updated

```
last_updated: Timestamp | None
```

Timestamp the index data was last updated.

### coverage_interval

```
coverage_interval: Interval
```

The time interval for which index requests have been sent to the datasource.

This does not mean that data is available for the entire interval. If the index status is 'ok', the interval left value should equal the index horizon, and the right value should be close to the current time.

### data_interval

```
data_interval: Interval
```

The time interval for which actual data is available in the index.

The left and right values of the returned interval are the timestamps of the earliest and latest data points in the index.

### index_frequency

```
index_frequency: Timedelta
```

The frequency at which the index is generally updated with new data.

### update

```
update() -> IndexDetails
```

Send a request to update the index with the latest data

Returns:

| Type           | Description                                                            |
| -------------- | ---------------------------------------------------------------------- |
| `IndexDetails` | The updated index details after the update request has been processed. |

### refresh

```
refresh() -> None
```

Refresh the tag index

### delete

```
delete() -> None
```

Delete the tag index.
