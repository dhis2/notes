
## Changes to `user` properties

From 2.35, all endpoints that expose objects that has `user` property will no longer expose the full graph of a `user`, this means that field filters like:

```
?fields=id,displayName,user[id,firstName,surname, userCredentials[*]]
?fields=id,displayName,userGroups[id,firstName,surname, userCredentials[*]]
```

Will no longer expose all available properties and instead only:

- `id`
- `code`
- `name`
- `displayName` (should be preferred over name)
- `username` (previously part of `userCredentials`)

So queries like this should be favored instead:

```
?fields=id,displayName,user[id,displayName]
?fields=id,displayName,userGroups[username]
```

Please note that this also applies to properties that are exposing a user but are not called user, an example would be `lastUpdatedBy`.
