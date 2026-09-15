## trendminer_interface.objects.ContextComponentFilter

Filter on components the context items are attached to

Attributes:

| Name      | Type                                                                             | Description                                                                                                                                                                                                          |
| --------- | -------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `queries` | `list of tuple[Tag or Asset or Attribute, {"self", "ancestors", "descendants"}]` | List of components on which to filter, and whether to include ancestors or descendants. For tags, only self is possible. For attributes, only self and ancestors are possible. For assets, all options are possible. |
| `mode`    | \`{'empty', 'not empty'}                                                         | None\`                                                                                                                                                                                                               |

### queries

```
queries: (
    list[tuple[Tag | Asset | Attribute, ComponentInclusion]]
    | None
)
```

### mode

```
mode: EmptyMode | None
```
