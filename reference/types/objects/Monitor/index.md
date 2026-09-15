## trendminer_interface.objects.Monitor

TrendMiner monitor

Attributes:

| Name                    | Type                             | Description                                                 |
| ----------------------- | -------------------------------- | ----------------------------------------------------------- |
| `fingerprint_trigger`   | `(ValueBasedSearch, optional)`   | Optional search that triggers fingerprint-based monitoring. |
| `fingerprint_threshold` | `(float, optional)`              | Threshold value for fingerprint deviation monitoring.       |
| `webhook`               | `WebhookMonitorNotification`     | Webhook notification configuration for this monitor.        |
| `email`                 | `EmailMonitorNotification`       | Email notification configuration for this monitor.          |
| `context`               | `ContextItemMonitorNotification` | Context item notification configuration for this monitor.   |

### fingerprint_trigger

```
fingerprint_trigger: (
    ValueBasedSearch
    | SimilaritySearch
    | AreaSearch
    | DigitalStepSearch
    | Fingerprint
    | None
) = fingerprint_trigger
```

### fingerprint_threshold

```
fingerprint_threshold: float | None = fingerprint_threshold
```

### webhook

```
webhook: WebhookMonitorNotification = webhook
```

### email

```
email: EmailMonitorNotification = email
```

### context

```
context: ContextItemMonitorNotification = context
```

### identifier

```
identifier: int
```

Monitor identifier. Not a UUID, just simple sequential numbering.

### name

```
name: str
```

Name of the monitor.

### parent

```
parent: (
    ValueBasedSearch
    | SimilaritySearch
    | AreaSearch
    | DigitalStepSearch
    | Fingerprint
)
```

The search or fingerprint object that this monitor is based on.

### state

```
state: Literal['enabled', 'disabled', 'system disabled']
```

Current state of the monitor.

### created_at

```
created_at: Timestamp | None
```

Timestamp when the monitor was created.

### last_modified

```
last_modified: Timestamp | None
```

Timestamp when the monitor was last modified.

### update

```
update() -> None
```

Update the monitor configuration on the server

Notes

Does not return the updated monitor object. To get the updated monitor, retrieve it again from its parent or its identifier.

### enable

```
enable() -> None
```

Enable the monitor

Notes

Does not return an updated monitor object nor are any attributes updated in place. To get the updated monitor, retrieve it again from its parent or its identifier.

### disable

```
disable() -> None
```

Disable the monitor

Notes

Does not return an updated monitor object nor are any attributes updated in place. To get the updated monitor, retrieve it again from its parent or its identifier.

### get_results

```
get_results(limit: int = 2000) -> DataFrame
```

Get most recent monitor results

Parameters:

| Name    | Type  | Description                                                                    | Default |
| ------- | ----- | ------------------------------------------------------------------------------ | ------- |
| `limit` | `int` | The maximum number of results to retrieve. Defaults to the max allowed number. | `2000`  |

Returns:

| Name      | Type        | Description                                                                                                                                                                                         |
| --------- | ----------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `results` | `DataFrame` | Result DataFrame with IntervalIndex, and open and score columns. Note that the match score (0 - 100) column will be NaN for all monitors that do not have a SimilaritySearch or Fingerprint parent. |
