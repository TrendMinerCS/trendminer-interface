## trendminer_interface.objects.ContextField

Configuration of a context field

Attributes:

| Name          | Type          | Description                                                                                                                                        |
| ------------- | ------------- | -------------------------------------------------------------------------------------------------------------------------------------------------- |
| `name`        | `str`         | Name that is visible to the users in the appliance                                                                                                 |
| `placeholder` | `str`         | Field placeholder that is displayed to the user if the field is blank. This is NOT a default value, it is a visual aid to the user; "" if not set. |
| `options`     | `list of str` | Options for enumeration fields; [] for non-enumeration fields.                                                                                     |

### name

```
name: str = name
```

### placeholder

```
placeholder: str = placeholder
```

### options

```
options: list[str] = options
```

### identifier

```
identifier: str
```

UUID of the context field

### key

```
key: str
```

Unique key that is used as the main identifier of the field

### field_type

```
field_type: ContextFieldType
```

Context field type. Determines what type of values the field can take.

### update

```
update() -> ContextField
```

Update the appliance context field to the current instance configuration

Returns:

| Type           | Description           |
| -------------- | --------------------- |
| `ContextField` | Updated context field |

### delete

```
delete() -> None
```

Permanently delete the context field
