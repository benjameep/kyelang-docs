---
title: Kye Docs
type: docs
---

# Kye Docs

{{< hint danger >}}
**!! Under Active Development !!**  
Kye is in its early stages and is not yet available for public use.

If you would like to be notified when a public release is made, subscribe to [my substack](https://kyelabs.substack.com) 

Thank you! :smiling_face_with_smiling_eyes:
{{< /hint >}}

## What is Kye?

Kye stands for "Know Your Edges". It is intended to be a very simple language with punctuation similar to JSON.

It is similar in purpose to GraphQL where it tries to serve as an universal place
for data models to be defined. When those data models are attached to an engine,
the engine can validate whether or not given data matches the defined data models.

I also envision extraction and transformation functions to be attached to data models
so that a Kye query can extract and serve the data as requested. Enabling a Kye platform
to be a one-stop shop for managing all data across many sources.

## Identifiers are case-sensitive

Capitalized identifiers are [Types]({{< relref "type" >}})
  - `City`
  - `Person`
  - `EmailAddress`

lower-case identifiers are [Edges]({{< relref "edge" >}})
  - `firstName`
  - `home_address`
  - `parent`

ALL_CAPS identifiers are enum constants
  - `TRUE`
  - `BACHELORS_DEGREE`
  - `ACTIVE_STATUS`

## Type Definitions

Custom types are defined with either the `type` or `model` keyword.

Using the `type` keyword basically creates a type alias, extending the parent type.

    type Name: String
    type Count: Number

Using the `enum` keyword creates an enum type, defining constants to be used anywhere

    enum Status {
      INACTIVE
      ACTIVE
      DISABLED
    }

Using the `model` keyword requires you to specify an edge to be used as the index of the type.

    model User(id) {
      id: Number
      name: String
    }

## Edge Definitions

Edges are defined within the curly brackets `{}` of a type, and can either specify a value or
a type.

If a value is specified (using literals or referencing another edges) then it is considered 
a computed edge, and during validation the computed value is checked to make sure it matches
the given value.

    model User(id) {
      id: Number
      name: String
      phone: String

      # ensures that the status value is always equal to the string "active"  
      status: "active"

      # references the phone edge
      masked_phone: phone.slice(0,-4).replace(/\d/,"*") + phone.slice(-4)
    }

## Edge Cardinality

Unlike other programming languages that surround a type in an Array to allow for there to be
multiple definitions of a value, Kye uses a suffix at the end of the edge name similar to regex syntax.

- `+` means you expect one or more definitions.
- `?` means you will allow for a NULL definition.
- `*` means you expect zero to many definitions.

Not specifying a cardinality suffix means you expect one and only one definition.

    model Post(id) {
        id: Number
        authors+: Person
        tags*: Tag
        published?: Date
    }

## Type Queries

Type ranges can be clamped by using comparison operators

    type Count: Number >= 0

Types can be filtered by using an edge expression within square brackets

    type ActiveUser: User[status == ACTIVE]

    type LongString: String[length > 60]

Types can be combined through or `|`, and `&`, xor `^` operators.

    type Name: String[length <= 3] & String[length < 60]

    type Grade: "A" | "B" | "C" | Number