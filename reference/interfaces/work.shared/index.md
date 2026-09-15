# `client.work.shared`

## trendminer_interface.\_client.work.shared.SharedWorkFacade

Facade for getting items from the top level of the 'shared with me' directory

### search_contents

```
search_contents(
    query: str | None = None,
    content_type: type[SavedItem] | None = None,
    direct_only: bool = True,
    page: int = 0,
    size: int = 2000,
) -> PagedList[SavedItem]
```

Search items saved directly in the 'shared with me' root directory.

Parameters:

| Name           | Type      | Description                                                                                                          | Default                                                                                |
| -------------- | --------- | -------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------- |
| `query`        | \`str     | None\`                                                                                                               | Search query to filter items by name or description. If None, no filtering is applied. |
| `content_type` | `type[T]` | List of types of items to get. If None, items of all types are returned.                                             | `None`                                                                                 |
| `direct_only`  | `bool`    | If True, only items directly shared with the user are returned. If False, also items in shared folders are returned. | `True`                                                                                 |
| `page`         | `int`     | Page number of results to return. By default, start at the first page of results (0-indexed).                        | `0`                                                                                    |
| `size`         | `int`     | Number of results to return per page.                                                                                | `2000`                                                                                 |

Returns:

| Name   | Type           | Description                                                 |
| ------ | -------------- | ----------------------------------------------------------- |
| `item` | `PagedList[T]` | Paginated list of shared items matching the search criteria |

### get_item

```
get_item(
    name: str, content_type: type[SavedItem]
) -> SavedItem
```

Get item with the given name and type saved in the 'shared with me' root directory

Parameters:

| Name           | Type              | Description              | Default    |
| -------------- | ----------------- | ------------------------ | ---------- |
| `name`         | `str`             | Name of the item to get  | *required* |
| `content_type` | `type[SavedItem]` | Type of the item to get. | *required* |

Raises:

| Type                | Description                                                        |
| ------------------- | ------------------------------------------------------------------ |
| `ResourceNotFound`  | If no item with the given name and type exists in the shared work. |
| `AmbiguousResource` | If multiple items match the given name and type.                   |
