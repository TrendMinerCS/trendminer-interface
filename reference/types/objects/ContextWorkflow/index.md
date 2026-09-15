## trendminer_interface.objects.ContextWorkflow

Configuration of a context workflow

Attributes:

| Name     | Type          | Description                                                                                                                                                 |
| -------- | ------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `name`   | `str`         | Name that is visible to the users in the appliance                                                                                                          |
| `states` | `list of str` | Possible states of the workflow; the first and last items are considered the start and end states, respectively, and can occur only once in a context item. |

### name

```
name: str = name
```

### states

```
states: list[str] = states
```

### identifier

```
identifier: str
```

UUID of the context workflow

### update

```
update() -> ContextWorkflow
```

Update the appliance context workflow to the current instance configuration

Returns:

| Type              | Description              |
| ----------------- | ------------------------ |
| `ContextWorkflow` | Updated context workflow |

### delete

```
delete() -> None
```

Permanently delete the context workflow
