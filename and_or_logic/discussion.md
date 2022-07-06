# Signpost - logic using `and`/`all()` and/or `or`/`any()`

We need a signpost to link to the various existing canonicals explaining logical errors wherein OP expects these operators and builtin functions to work like the corresponding English words.

## Setup

You know the drill.
```
'a' == 'b' or 'c' # why true?
'a' or 'b' == 'c' # why true?
('a' or 'b') == 'b' # why false?
```
Similar issues with `and`; similar issues with the functions `any()` (parallel to `or`) and `all()` (parallel to `and`); similar issues with other relational operators (especially `in`)


## Standard solutions

Either the conditions have to be separately tested explicitly; or `in` can be used for the case of multiple values on on

The signpost would also serve to answer anyone who actually does ask the questions on a theoretical level; it should cover:

* Why does it do what it does?
* * truthy and falsy values
* * Structure of expressions; each operation is evaluated in order, according to (ahem) the order of operations
* * But that doesn't actually cause the problem
* * Short-circuiting; rhs is only evaluated if needed, unlike most binary operators
* * But that doesn't actually cause the problem either

* How should I write the code instead?
* * separate conditions are needed to do it in the basic way
* * show how any() and all() synergize with generators
* * multiple equality checks can be converted to set membership
* * * performance considerations for set construction
* * for multiple numeric inequality checks, figure out the most challenging test case
* * for multiple "not equals", convert to equals following de Morgan's law
* * for multiple values `in` one, check the set intersection
* * for one value `in` multiple possibilities, intersecting or unioning the possibilities first might be better
* * * but be careful of `str.__contains__`

* Can it be changed?
* * (A working implementation should really be in a separate question)
* * Short-circuiting means that at most two operands could be considered, and the behaviour can't be overloaded anyway. You would have to look at `|` and `&`
* * You can only define the operator for a type that you control; this means at least one operand has to be of that type
* * This has to *result in a value* that can be used with the relational operator to get the right result - i.e., more operator overloading
* * * `(foo(a) | b) in c` can't be overloaded for this; it depends on `__contains__`, but only the right-hand side can overload that. It would need the RHS to also be a type under your control
* * all of this is still an extremely bad idea


## Existing candidates

Parts of the material are covered by:
https://stackoverflow.com/questions/15112125 for `'a' or 'b' == 'c'` (why/how)
https://stackoverflow.com/questions/6838238 for `'a' == 'b' or 'c'` (how)
https://stackoverflow.com/questions/20002503 for `'a' == 'b' or 'c'` (why)
https://stackoverflow.com/questions/62361656 for `or` has no dunder, and `__or__` implements `|`
https://stackoverflow.com/questions/4843158 for substring of any element of a list
https://stackoverflow.com/questions/19211828 `any` vs. set membership
https://stackoverflow.com/questions/15147751/ all of list `in` another list (but not this one, because of the repetition issue)
https://stackoverflow.com/questions/3931541 all of list `in` another list
https://stackoverflow.com/questions/740287 any of list `in` another list
https://stackoverflow.com/questions/72877675 doing it anyway

