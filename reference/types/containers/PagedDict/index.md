## trendminer_interface.\_services.PagedDict

Bases: `Generic[K, V]`

Paginated dict of search results

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
data: dict[K, V]
```

The content of the current result page.

### total_elements

```
total_elements: int
```

The total number of elements across all pages

### next_page

```
next_page() -> PagedDict[K, V]
```

Perform a request to get the next page of results

### collect

```
collect(max_pages: int | None = 10) -> dict[K, V]
```

Collects all pages of results into a single dict

Parameters:

| Name        | Type  | Description | Default                                                                                                                                                                                                               |
| ----------- | ----- | ----------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `max_pages` | \`int | None\`      | Maximum number of pages to collect. Default is set to 10 to prevent accidental excessive API calls. Can be set to None to collect all pages regardless of number. Must be 1 (only the current page) or higher if set. |

Returns:

| Type      | Description                                                          |
| --------- | -------------------------------------------------------------------- |
| `content` | A dictionary containing the combined content of all collected pages. |

### stream

```
stream(
    max_pages: int | None = 10,
) -> Iterator[tuple[K, V]]
```

Stream dict items one by one, loading new pages as needed

Parameters:

| Name        | Type  | Description | Default                                                                                                                                                                                                             |
| ----------- | ----- | ----------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `max_pages` | \`int | None\`      | Maximum number of pages to stream. Default is set to 10 to prevent accidental excessive API calls. Can be set to None to stream all pages regardless of number. Must be 1 (only the current page) or higher if set. |

Yields:

| Name   | Type          | Description                                             |
| ------ | ------------- | ------------------------------------------------------- |
| `item` | `tuple[K, V]` | Each individual key-value pair from all streamed pages. |
