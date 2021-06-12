---
title: Refactoring - permissions
date: "2021-06-12T07:00:00.000Z"
description: "Refactoring simple frontend permissions handling."
---

# Example 

Let's say you have a function that checks the users permissions. One way to achive this is by assigning the user to groups and then checking if the user is a member of them.
If you were really verbose you could assign a user to groups that have READ permissions, CREATE permissions, ADMIN permission etc. This is all fine, but a bit wastefull, because 
there is some logic in CRUD operations. For example a user who has CREATE permissions, usually has READ permissions, and a user that is part of an _admin_ group certianly has
permission to view a resource, so assigning a admin user to all CRUD related groups makes no sense.

Here the logic get's a bit complicated.

...

Imagine we have a mapping somewhere where we mapp user groups to permissions. This mapping can be in the code, in a config file or in the database, but for the purpose of 
this example, let it be a mapping we just happen to have.

```javascript
functon hasPermission(groups, permission, permission):
  ....
```

```javascript
if (permission == "admin") {
  return permisssions.include("admin");
} else {
  return permissions.includes(permission) || permisssions.include("admin");
}
```

