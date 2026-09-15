## trendminer_interface.objects.EmailMonitorNotification

Monitor email notification

Attributes:

| Name      | Type          | Description                         |
| --------- | ------------- | ----------------------------------- |
| `enabled` | `bool`        | Whether the notification is enabled |
| `subject` | `str`         | The email subject                   |
| `message` | `str`         | The email message body              |
| `to`      | `list of str` | The email recipients                |

### enabled

```
enabled: bool = enabled
```

### subject

```
subject: str = subject
```

### message

```
message: str = message
```

### to

```
to: list[str] = to
```

### enabled_at

```
enabled_at: Timestamp | None
```

The timestamp the notification was enabled
