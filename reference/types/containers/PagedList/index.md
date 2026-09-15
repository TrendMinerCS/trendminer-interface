## trendminer_interface.\_services.PagedList

Bases: `Generic[T]`

Paginated list of search results

### has_next

```
has_next: bool
```

Whether there is a next page of results available

### page_number

```
page_number: int
```

The current page number (0-indexed)

### size

```
size: int
```

The requested number of items per page. Not necessarily the same as the actual number of items on the page

### data

```
data: list[T]
```

The content of the current result page.

### total_pages

```
total_pages: int | None
```

The total number of pages

Not available for user groups

### total_elements

```
total_elements: int | None
```

The total number of elements across all pages

Not available for user groups

### next_page

```
next_page() -> PagedList[T]
```

Perform a request to get the next page of results

### collect

```
collect(max_pages: int | None = 10) -> list[T]
```

Collects all pages of results into a single list

Parameters:

| Name        | Type  | Description | Default                                                                                                                                                                                                               |
| ----------- | ----- | ----------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `max_pages` | \`int | None\`      | Maximum number of pages to collect. Default is set to 10 to prevent accidental excessive API calls. Can be set to None to collect all pages regardless of number. Must be 1 (only the current page) or higher if set. |

Returns:

| Type      | Description                                   |
| --------- | --------------------------------------------- |
| `content` | A list with the items of all collected pages. |

### stream

```
stream(max_pages: int | None = 10) -> Iterator[T]
```

Streams items one by one, loading new pages as needed

Parameters:

| Name        | Type  | Description | Default                                                                                                                                                                                                             |
| ----------- | ----- | ----------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `max_pages` | \`int | None\`      | Maximum number of pages to stream. Default is set to 10 to prevent accidental excessive API calls. Can be set to None to stream all pages regardless of number. Must be 1 (only the current page) or higher if set. |

Yields:

| Name      | Type | Description                                                                 |
| --------- | ---- | --------------------------------------------------------------------------- |
| `content` | `T`  | Each individual item from the content of all streamed pages, one at a time. |
