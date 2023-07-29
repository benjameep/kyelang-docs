---
weight: 25
# bookHidden: true
---

# Nominal, Ordinal, Interval, or Ratio (to be determined)

> skip for first version (no major transformation methods)

I would like a way for Types to identify themselves as Nominal, Ordinal, Interval, or Ratio. This will be especially useful for tools that automatically generate charts from data. For example knowing that Poor~Excellent is Ordinal and it's specific order will help the tool choose a gradient color scale instead of a discrete color scale.

This will likely be done with operator overloading, as each level of measurement is defined by what set of operators are allowed to work with it (each level needs to be able to use all previous levels of operators)

- Nominal: `==`, `!=`
- Ordinal: `>`, `<`, `>=`, `<=`, `~`
- Interval: `+`, `-`
- Ratio: `*`, `/`, `== Null` (true zero)

Note that interval measurements sometimes need a secondary interval/delta type. For example DateTimes:
- `DateTime - DateTime` is `TimeDelta`
- `DateTime + DateTime` is not valid
- `DateTime + TimeDelta` is `DateTime`

I might also want to include an "invert" operator that transforms:
- `True` to `False`
- `34` to `-34`
- `Poor` to `Excellent` and `Fair` to `Good` (inverses the order of Ordinals)
- Does not apply to unsigned integers (counts)