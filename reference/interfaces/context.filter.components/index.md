# `client.context.filter.components`

## trendminer_interface.\_client.context.filter.component_filter.ContextComponentFilterFacade

Facade for creating context component filters

### new

```
new(
    queries: list[
        tuple[
            Tag | Asset | Attribute,
            Literal["self", "ancestors", "descendants"],
        ]
    ]
    | None = None,
    mode: EmptyMode | None = None,
) -> ContextComponentFilter
```

Context filter on components the context items are attached to

Parameters:

| Name      | Type               | Description | Default                                                                                                                     |
| --------- | ------------------ | ----------- | --------------------------------------------------------------------------------------------------------------------------- |
| `queries` | \`list\[tuple\[Tag | Asset       | Attribute, Literal['self', 'ancestors', 'descendants']\]\]                                                                  |
| `mode`    | \`EmptyMode        | None\`      | When not None, filter on whether the context items are attached to any component at all. Ignores the queries when not None. |
