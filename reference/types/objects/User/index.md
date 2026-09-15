## trendminer_interface.objects.User

A natural user or a service account

### identifier

```
identifier: str
```

Identifier of the user

### name

```
name: str
```

Username

### first_name

```
first_name: str | None
```

First name of the user

None for service accounts

### last_name

```
last_name: str | None
```

Last name of the user

None for service accounts

### mail

```
mail: str | None
```

Email address of the user

None for service accounts

### groups

```
groups: list[UserGroup]
```

User groups the user belongs to

### created_at

```
created_at: Timestamp
```

User creation timestamp

### roles

```
roles: list[str]
```

List of user roles
