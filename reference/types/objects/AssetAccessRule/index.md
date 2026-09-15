## trendminer_interface.objects.AssetAccessRule

Access rule giving a user certain permissions to a certain Asset or Attribute

Attributes:

| Name         | Type                | Description                                                                                                                                                                                                                                                                 |
| ------------ | ------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `subject`    | `User or UserGroup` | The subject to which the access rule relates                                                                                                                                                                                                                                |
| `permission` | `str`               | The permission granted to the user - "read": allows reading context items of the asset/attribute, and thus also browsing. - "browse": allows browsing the asset/attribute, but not reading context items. - "none": explicit denial of permissions for the asset/attribute. |

### subject

```
subject: User | UserGroup = subject
```

### permission

```
permission: AssetAccessPermission = permission
```

### identifier

```
identifier: str
```

Unique UUID of the access rule

### node

```
node: Asset | Attribute
```

The asset framework node to which the access rule relates

### delete

```
delete() -> None
```

Delete the access rule

Notes

When a rule is retrieved as an inherited access rule, it will be removed from the asset on which it is defined.
