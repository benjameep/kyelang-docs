---
weight: 10
---

# Lookup
Use `()` to get a specific value within a type, using the type's index, throwing an error if it does not exist.

```
# Get the user with the email `bob@email.com`
User(email="bob@email.com")

# Gets the string "4"?
String(4)
```

Also used to define arguments on an edge, which I guess is getting a specific edge in a sense...
```
String.slice(0..5)
```