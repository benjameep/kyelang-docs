---
weight: 15
---

# Define Edges
Edges are always attached to a type, because they are a function of the type's index. Use `{}` to define edges on a Type

```
User(user_id: String) {
  name: String
  status: "active" | "inactive" | "deleted"
  lastLogin: DateTime?
}
```

# Define an Edge
Use `:` to define an edge

Before the `:` is the column name, after the `:` is what Type you are expecting to be found in that column.
```kye
name: String*
```