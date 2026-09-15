# `client.work.my_work`

## trendminer_interface.\_client.work.my_work.MyWorkFacade

Facade for getting items saved directly in the 'my work' root directory

### search_contents

```
search_contents(
    content_type: type[SavedItem] | None = None,
    page: int = 0,
    size: int = 2000,
) -> PagedList[SavedItem]
```

Search items saved directly in the 'my work' root directory.

Parameters:

| Name           | Type      | Description                                                                                   | Default |
| -------------- | --------- | --------------------------------------------------------------------------------------------- | ------- |
| `content_type` | `type[T]` | List of types of items to get. If None, items of all types are returned.                      | `None`  |
| `page`         | `int`     | Page number of results to return. By default, start at the first page of results (0-indexed). | `0`     |
| `size`         | `int`     | Number of results to return per page.                                                         | `2000`  |

Returns:

| Name    | Type           | Description                                                                             |
| ------- | -------------- | --------------------------------------------------------------------------------------- |
| `items` | `PagedList[T]` | Paginated list of items of the given type saved in the authenticated user's home folder |

### get_item

```
get_item(
    name: str, content_type: type[SavedItem]
) -> SavedItem
```

Get item with the given name and type saved in the 'my work' root directory

Parameters:

| Name           | Type              | Description              | Default    |
| -------------- | ----------------- | ------------------------ | ---------- |
| `name`         | `str`             | Name of the item to get  | *required* |
| `content_type` | `type[SavedItem]` | Type of the item to get. | *required* |

Raises:

| Type                | Description                                                  |
| ------------------- | ------------------------------------------------------------ |
| `ResourceNotFound`  | If no item with the given name and type exists in 'my work'. |
| `AmbiguousResource` | If multiple items match the given name and type.             |
