---
layout:
  title:
    visible: true
  description:
    visible: false
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: true
---

# Welcome

Kye stands for “Know Your Edges”. It is intended to be a very simple language with punctuation similar to JSON.

It is similar in purpose to GraphQL where it tries to serve as an universal place for data models to be defined. When those data models are attached to an engine, the engine can validate whether or not given data matches the defined data models.

I also envision extraction and transformation functions to be attached to data models so that a Kye query can extract and serve the data as requested. Enabling a Kye platform to be a one-stop shop for managing all data across many sources.

```
User(id)(username) {
  id: Number
  username: String
  name: String
  age?: Number

  assert age > 0 & age <= 120
}
```
