# `client.context.workflow`

## trendminer_interface.\_client.context.workflow.ContextWorkflowFacade

Facade for retrieving and creating context workflows

### create

```
create(name: str, states: list[str]) -> ContextWorkflow
```

Create a new context workflow

Parameters:

| Name     | Type        | Description                                                                                                                                                 | Default    |
| -------- | ----------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------- |
| `name`   | `str`       | Name of the context workflow. Does not have to be unique.                                                                                                   | *required* |
| `states` | `list[str]` | Possible states of the workflow; the first and last items are considered the start and end states, respectively, and can occur only once in a context item. | *required* |

Returns:

| Type              | Description                   |
| ----------------- | ----------------------------- |
| `ContextWorkflow` | The created context workflow. |

### from_identifier

```
from_identifier(identifier: str) -> ContextWorkflow
```

Get a context workflow by its identifier

Parameters:

| Name         | Type  | Description                              | Default    |
| ------------ | ----- | ---------------------------------------- | ---------- |
| `identifier` | `str` | UUID of the context workflow to retrieve | *required* |

Returns:

| Type              | Description                                |
| ----------------- | ------------------------------------------ |
| `ContextWorkflow` | Context workflow with the given identifier |

Raises:

| Type               | Description                                              |
| ------------------ | -------------------------------------------------------- |
| `ResourceNotFound` | If no context workflow with the given identifier exists. |

### from_name

```
from_name(name: str) -> ContextWorkflow
```

Get a context workflow by its name

Parameters:

| Name   | Type  | Description                              | Default    |
| ------ | ----- | ---------------------------------------- | ---------- |
| `name` | `str` | Name of the context workflow to retrieve | *required* |

Returns:

| Type              | Description                          |
| ----------------- | ------------------------------------ |
| `ContextWorkflow` | Context workflow with the given name |

Raises:

| Type                | Description                                         |
| ------------------- | --------------------------------------------------- |
| `ResourceNotFound`  | If no context workflow with the given name exists.  |
| `AmbiguousResource` | If multiple context workflows match the given name. |

### search

```
search(
    name: str | None = None, page=0, size=2000
) -> PagedList[ContextWorkflow]
```

Search for context workflows

Parameters:

| Name   | Type  | Description                                                                                       | Default |
| ------ | ----- | ------------------------------------------------------------------------------------------------- | ------- |
| `name` | `str` | Search for context workflows with names matching this query. Can use the '\*' symbol as wildcard. | `None`  |
| `page` | `int` | Page number to start the search from (0-indexed). Default is 0.                                   | `0`     |
| `size` | `int` | Number of results to return per page. Default is 2000 (the maximum supported by the backend).     | `2000`  |

Returns:

| Type                         | Description                                               |
| ---------------------------- | --------------------------------------------------------- |
| `PagedList[ContextWorkflow]` | Page with context workflows matching the search criteria. |
