## trendminer_interface.objects.WebhookMonitorNotification

Monitor webhook notification

Attributes:

| Name         | Type                    | Description                            |
| ------------ | ----------------------- | -------------------------------------- |
| `enabled`    | `bool`                  | Whether the notification is enabled    |
| `enabled_at` | `(Timestamp, optional)` | What time the notification was enabled |
| `url`        | `str`                   | The webhook URL                        |

### enabled

```
enabled: bool = enabled
```

### url

```
url: str = url
```

### enabled_at

```
enabled_at: Timestamp | None
```

The timestamp the notification was enabled
