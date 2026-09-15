## trendminer_interface.objects.TagImport

Wrapper around an imported tag

### identifier

```
identifier: str
```

The identifier of the import itself (not the imported tag)

### tag

```
tag: Tag
```

The imported tag

### created_at

```
created_at: Timestamp
```

Timestamp on which the tag was imported

### delete

```
delete() -> None
```

Permanently remove the imported tag (blocking the tag name for future imports)

Notes

Deleting an imported tag is typically not desirable as you will not be able to use this tag name for future imports. A non-deleted imported tag can simply be overwritten by performing a new import with the same tag name.
