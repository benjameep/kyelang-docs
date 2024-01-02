---
weight: 5
bookToc: true
---

# Type

Capitalized identifier representing a set of similar values. Analogous to a Noun.


## Literals
There are predefined types like `Number`, `String`, `Boolean`

|           | Examples    |
| --------- | ----------- |
| Number    | `1`, `-3.42`    |
| String    | `"foo"`       |
| Boolean   | `true`, `false` |

All other types inherit from these literals, for example:
- a person's `Name` inherits from `String`
- a `Count` inherits from `Number` where the number is a positive whole number.

In this inheritance process the child types are a strict subset of their parent type.

## Aliases
Aliases allow you to inherit from parent types, scoping them down and renaming them for
your convenience.

For example:

    type Name: String
    type Count: Number > 0


## Models
Some types are a combination of multiple types.

For example a `Date` is a combination of `Year`, `Month`, and `Day`. If you change any one of those
3 values then it results in a different `Date`.

To represent these types that are a combination of other types, we use "Models". Models use a syntax
similar to function definitions, where each component of the type is defined within parenthesis. Our `Date`
example would look something like this:

    Date(year: Year, month: Month, day: Number[1..31])

## Formats
Sometimes there are multiple ways to define the same type, for example a `Date` could be defined
as `Date(year,month,day)` or `Date(year,dayOfYear)`. This is resolved with a syntax similar to function overloading,
where you define the type multiple times with the same name, but different arguments.

    Date(year: Year, month: Month, day: Number[1..31])

    Date(year: Year, dayOfYear: Number[1..365])

You'll need to define a way for the formats to convert between one another. (The syntax of which has not been nailed down yet) Which is easy enough with an expression if the formats can be computed from another format. But formats can be used even for types that can't be computed.

For example say an employee can be identified by either their employee id number or their email address.

    Employee(employeeId: Number)

    Employee(email: Email)

There is no function you can write to convert in between their `employeeId` and `email`, the conversion would have to be done through a lookup function. Which means at some point you'll need to define a table that contain's both an employee's id & email.

    Employee(employeeId: Number, email: Email)