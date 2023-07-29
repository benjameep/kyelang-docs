---
weight: 5
---

# Filtering
Use `[]` to filter types to a subset of that type
```
# Numbers 0 through 100
Number[0..100]

# Strings with a length longer than 5
String[.length > 5]

# 
Car[.make == "Toyota" & .year > 2000]
```

Can either use edges on the type, or a range of instances
