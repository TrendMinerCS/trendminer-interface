# `client.work`

## trendminer_interface.\_client.work.WorkFacade

Facade for work organizer management

### folder

```
folder: FolderFacade
```

Facade for getting and creating folders in the work organizer

### my_work

```
my_work: MyWorkFacade
```

Facade for getting items saved directly in the 'my work' root directory

### shared

```
shared: SharedWorkFacade
```

Facade for getting items saved directly in the 'shared with me' root directory

### favorites

```
favorites: FavoriteWorkFacade
```

Facade for getting items saved directly in the 'favorites' root directory

### transfer

```
transfer(
    items: list[SavedItem],
    user: User,
    folder_name: str,
    retain_write_access: bool = True,
) -> None
```

Transfer items to another user

Parameters:

| Name                  | Type              | Description                                                                                                      | Default    |
| --------------------- | ----------------- | ---------------------------------------------------------------------------------------------------------------- | ---------- |
| `items`               | `list[SavedItem]` | Saved items to transfer                                                                                          | *required* |
| `user`                | `User`            | New owner of the saved items                                                                                     | *required* |
| `folder_name`         | `str`             | Name of the folder that will be created in the new user's home folder, which will contain the transferred items. | *required* |
| `retain_write_access` | `bool`            | Whether the current user should retain write access to the transferred items                                     | `True`     |
