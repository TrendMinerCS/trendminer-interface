## trendminer_interface.types.ValueBasedSearchQuery

```
ValueBasedSearchQuery = (
    tuple[
        Tag, Literal["=", "!=", ">", "<", ">=", "<="], float
    ]
    | tuple[Tag, Literal["="], str]
    | tuple[Tag, Literal["in"], list[str]]
    | tuple[Tag, Literal["constant"]]
)
```
