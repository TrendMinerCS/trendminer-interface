# `client.context.filter.keyword`

## trendminer_interface.\_client.context.filter.keyword_filter.ContextKeywordFilterFacade

Facade for creating context keyword filters

### new

```
new(
    keywords: list[str] | None = None,
    mode: EmptyMode | None = None,
) -> ContextKeywordFilter
```

Filter on context item keywords

Parameters:

| Name       | Type                     | Description                                                                                                 | Default                                                                       |
| ---------- | ------------------------ | ----------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------- |
| `keywords` | \`list of str            | None\`                                                                                                      | Keywords which must be present on the context items. Ignored when using mode. |
| `mode`     | `('empty', 'not empty')` | When not None, filter for context items without or with keywords. Ignores the keywords parameter when used. | `"empty"`                                                                     |

Returns:

| Type                   | Description |
| ---------------------- | ----------- |
| `ContextKeywordFilter` |             |
