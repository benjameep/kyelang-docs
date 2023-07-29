---
weight: 10
---

# Edge
Lowercase identifier representing the relationship between a source type and a target type. Analogous to properties and methods on a class.

Edges are directed from a source type to a target type, because that is how language works. A person's dog is their "pet", but a dog's person is their "owner"

Edges are local to their source type. So a person's "name" is a different edge than a dog's "name", even though both of the edges are called "name"

Edges can also have arguments, each unique combination of arguments will be considered a separate edge, because it is assumed that every unique combination of arguments will lead to a separate range of [Types]({{< ref "type" >}}) But this is especially useful for computed edges.
```
# Edge to first character in a string
String.char(0)

# Edge to string with given date format
Date.format("YYYY-MM-DD")
```
