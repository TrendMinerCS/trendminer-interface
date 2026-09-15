## trendminer_interface.objects.ContextKeywordFilter

Filter on context item keywords

Attributes:

| Name       | Type                                 | Description                                                                                                 |
| ---------- | ------------------------------------ | ----------------------------------------------------------------------------------------------------------- |
| `keywords` | `list of str, optional`              | Keywords which must be present on the context items. Ignored when using mode.                               |
| `mode`     | `({'empty', 'not empty'}, optional)` | When not None, filter for context items without or with keywords. Ignores the keywords attribute when used. |

### keywords

```
keywords: list[str] | None
```

### mode

```
mode: EmptyMode | None
```
