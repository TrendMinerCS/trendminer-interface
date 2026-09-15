## trendminer_interface.\_services.PagedDataFrame

Paginated DataFrame of search results

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
data: DataFrame
```

The content of the current result page.

### total_elements

```
total_elements: int | None
```

The total number of elements across all pages

Not available for context items.

### total_pages

```
total_pages: int | None
```

The total number of pages

Not available for context items.

### next_page

```
next_page() -> PagedDataFrame
```

Perform a request to get the next page of results

### collect

```
collect(max_pages: int | None = 10) -> DataFrame
```

Collects all pages of results into a single DataFrame

Parameters:

| Name        | Type  | Description | Default                                                                                                                                                                                                               |
| ----------- | ----- | ----------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `max_pages` | \`int | None\`      | Maximum number of pages to collect. Default is set to 10 to prevent accidental excessive API calls. Can be set to None to collect all pages regardless of number. Must be 1 (only the current page) or higher if set. |

Returns:

| Type        | Description                                                                    |
| ----------- | ------------------------------------------------------------------------------ |
| `DataFrame` | A single DataFrame containing the concatenated results of all collected pages. |
