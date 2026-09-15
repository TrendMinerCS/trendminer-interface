## trendminer_interface.objects.ContextEnumerationFieldFilter

Filter on context enumeration field values

Attributes:

| Name     | Type                     | Description                                                          |
| -------- | ------------------------ | -------------------------------------------------------------------- |
| `field`  | `ContextField`           | The context field on which to filter. Must be of 'enumeration' type. |
| `values` | \`list[str]              | None\`                                                               |
| `mode`   | \`{'empty', 'not empty'} | None\`                                                               |

### field

```
field: ContextField
```

### values

```
values: list[str] | None
```

### mode

```
mode: EmptyMode | None
```
