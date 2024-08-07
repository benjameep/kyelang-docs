# Querying Models

Queries are expressions that are used in a variety of places; selecting & filtering models, defining edge types & assertions.

Expressions used in the global scope return tables. For example, the following commands will display different views of the `User` table

```
> User

> User[name == "Ben"]

> User{ id, name }
```

Expressions used within the scope of a table generate a column. For example, a filter expression, an assertion expression, or computed column expression.

<pre><code><strong>> User{ full_name: first_name + ' ' + last_name }
</strong></code></pre>

## Expressions

Expressions support the basic operations:

* `+ - * / %` math
* `== != >= > < <=` comparison
* `! & | ^` logical (not, and, or, xor)
* `()` parenthesis

## Selecting

Use the curly brackets after a table expression to create a new view of that type, showing only the listed columns, able to define new computed columns, or define additional assertions for that view.

```
> User {
    id,
    full_name: first_name + ' ' + last_name
    assert id > 0
  }
```

## Filtering

Use square brackets after a table expression with a list of expressions that all must be true in order to be included in the resulting table.

```
> User[
    name == "Ben"
    country == "US"
  ]
```
