# Objects & Types

The interface exposes several kinds of classes. You rarely construct them yourself — you reach them by navigating the client and calling its methods.

- **Interfaces** — the facade classes reached as namespaces on the client (for example `client.tag_builder.aggregation`). Each groups related methods and sub-namespaces. See the **[Interface tree](https://trendminercs.github.io/trendminer-interface/reference/interface-tree/index.md)** for the full hierarchy.
- **Objects** — the resources returned by interface methods (for example `Aggregation`, `Asset`, `Dashboard`). These carry the data and behaviour of a single TrendMiner entity.
- **Definitions** — the `*Definition` classes you build to create new resources, typically via a `define` call, before saving them back to TrendMiner.
- **Containers** — the collection types returned by search-style methods, such as `PagedList`, `PagedDataFrame` and `PagedDict`, which stream results a page at a time.
- **Exceptions** — the errors the interface may raise, all derived from `TrendMinerError`.

Browse the sections for the full reference of each type.

## Retrieving items

Search and list methods usually return a **container** — `PagedList`, `PagedDataFrame`, or `PagedDict` — rather than a plain Python collection. A container holds only the first page of results and fetches further pages from the appliance on demand, so large result sets are never loaded all at once.

You don't iterate or index a container directly; you consume it in one of two ways:

- **Stream** — `stream()` yields items one at a time (key–value pairs for `PagedDict`), fetching the next page only once the current one is exhausted. Use it to process results without holding them all in memory.
- **Collect** — `collect()` materialises the results into a concrete `list`, `pandas.DataFrame`, or `dict`. Use it when you want the whole result set in hand.

Both default to `max_pages=10`, a guardrail against accidentally making a large number of API calls; pass `max_pages=None` to retrieve every page. The current page is always available directly as `.data`, alongside `.has_next` and `.next_page()` for manual paging.

```
tags = client.tag.search(name="Reactor*")   # -> PagedList[Tag]

# Stream: process one tag at a time, paging lazily
for tag in tags.stream():
    print(tag.name)

# Collect: materialise into a list (pass max_pages=None for every page)
all_tags = tags.collect(max_pages=None)
```

`PagedDataFrame` is the exception: it offers only `collect()` (returning a single concatenated `DataFrame`), while `stream()` is available on `PagedList` and `PagedDict`.

## Creating items

Creating something in TrendMiner typically involves three kinds of methods that build on one another:

- **`new(...)`** — constructs an in-memory building block that has no independent existence on the server, such as a context filter or a trend layer. These are the pieces you assemble into a larger object, and are found on the small builder facades (for example `client.context.filter.*`).
- **`define(...)`** — assembles those pieces into a local **definition** (a `*Definition` object): a complete, in-memory specification of a work organizer item that has not yet been saved.
- **`create(...)`** — persists a definition on the server and returns the live, saved work organizer item.

The example below builds and saves a ContextHub view, using all three:

```
# A context type to filter on (retrieved from the server)
anomaly = client.context.type.from_name("Anomaly")

# 1. new(...) — in-memory filter building blocks, not saved anywhere yet
type_filter = client.context.filter.context_types.new(types=[anomaly])
keyword_filter = client.context.filter.keyword.new(keywords=["shutdown"])

# 2. define(...) — assemble the pieces into a local ContextHubViewDefinition
definition = client.context.view.define(
    filters=[type_filter, keyword_filter],
    view_type="grid",              # "grid", "gantt" or "scatter"
)

# 3. create(...) — persist on the server, returning a live ContextHubView
view = client.context.view.create(
    definition=definition,
    name="Shutdown events",
    description="Grid view of shutdown context items",
)
```

Splitting creation this way keeps the intermediate objects reusable: the same definition can be created more than once (for instance into different folders), and the `new(...)` building blocks can be combined into different definitions.
