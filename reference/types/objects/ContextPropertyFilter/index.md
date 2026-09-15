## trendminer_interface.objects.ContextPropertyFilter

Filter on other properties of context items

The values assigned context items for which the key does not match that of a context field defined on the context type are considered 'other properties'. Only string-based searches are possible for other properties.

Attributes:

| Name     | Type          | Description                       |
| -------- | ------------- | --------------------------------- |
| `key`    | `str`         | Other property key to filter on   |
| `values` | `list of str` | List of values on which to filter |

### key

```
key: str
```

### values

```
values: list[str]
```
