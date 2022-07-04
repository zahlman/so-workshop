# Comprehensive (sorry) Reference for Processing Data with Comprehensions or Generators

I'm tired of handing out fish with questions like https://stackoverflow.com/questions/72850592. I would much rather teach people to fish in a more general way. Essentially, https://treyhunner.com/2015/12/python-list-comprehensions-now-in-color/ but in Stack Overflow form, and focused on designing a comprehension for the specific task.

More random examples of brainteaser that became popular but can't possibly actually be useful in isolation: https://stackoverflow.com/questions/2522503, https://stackoverflow.com/questions/41028547

## Setup

## Standard solutions

This would be more of a signpost than a canonical, but here are some topics to cover:

* Anatomy of a list comprehension e.g. https://stackoverflow.com/questions/25082410/, https://stackoverflow.com/questions/34835951/
* * Why list comprehensions can iterate quickly: https://stackoverflow.com/questions/41519707
* * Filtering comprehensions are commonly used to avoid removing items from a list while iterating over it: https://stackoverflow.com/questions/1207406/, https://stackoverflow.com/questions/5384914/, https://stackoverflow.com/questions/11941817/, https://stackoverflow.com/questions/5447494, https://stackoverflow.com/questions/6777485, https://stackoverflow.com/questions/61213866, https://stackoverflow.com/questions/49646583, https://stackoverflow.com/questions/9023078
* * Special note about *adding* elements? https://stackoverflow.com/questions/3752618
* * Special note about conditional expressions vs. the `else` clause https://stackoverflow.com/questions/4260280 - and the opposite, https://stackoverflow.com/questions/24442091
* Relationship of `map` and `filter` to comprehensions, and performance considerations: https://stackoverflow.com/questions/1247486/, https://stackoverflow.com/questions/6402824, https://stackoverflow.com/questions/11616599, https://stackoverflow.com/questions/22108488, https://stackoverflow.com/questions/24831476, https://stackoverflow.com/questions/3013449/, https://stackoverflow.com/questions/8994319, https://stackoverflow.com/questions/16784162, https://stackoverflow.com/questions/39178715
* * Special note about the "implicit zip" in `map`
* * Special note about the awkwardness of getting a flattened result from `map` https://stackoverflow.com/questions/22091389
* Nested clauses vs. nested comprehensions: https://stackoverflow.com/questions/1077015, https://stackoverflow.com/questions/952914/, https://stackoverflow.com/questions/18072759, https://stackoverflow.com/questions/1198777, https://stackoverflow.com/questions/16568056 (needs work btw), https://stackoverflow.com/questions/33355299
* * Philosophical note not to get carried away
* Special performance consideration for membership-based filtering: https://stackoverflow.com/questions/20056458, https://stackoverflow.com/questions/40639995 BUT also just consider set intersection e.g. https://stackoverflow.com/questions/3852780
* Using a comprehension only for its side effects? https://stackoverflow.com/questions/5766816
* Idiosyncratic performance concerns: https://stackoverflow.com/questions/56288015
* Understanding set and dict comprehensions by comparison, as well as generator expressions: https://stackoverflow.com/questions/9060653
* Performance considerations for generator expressions: https://stackoverflow.com/questions/245792/, https://stackoverflow.com/questions/47789, https://stackoverflow.com/questions/102535
* Generator variable binding: https://stackoverflow.com/questions/52968312
* Is it possible to generate *more than one* output from a given input? (compute a list of outputs - consistently - and use another clause to flatten)
* Is it possible for the transformation to be stateful?
* Walrus operator (3.8+) allows mapping before filtering https://stackoverflow.com/questions/11608238, https://stackoverflow.com/questions/48609891, https://stackoverflow.com/questions/130262, https://stackoverflow.com/questions/4097518
* * For deduplication, comprehensions are the wrong approach; see https://stackoverflow.com/questions/480214, https://stackoverflow.com/questions/7961363
* When no mapping or filtering is done, just use a constructor 
* * Special note about `dict(zip(keys, values)`
* * Special note about `list(map(f, xs))`
* There are no comprehensions for `tuple`, `bytearray` or `bytes`, but they can be passed a generator expression: https://stackoverflow.com/questions/16940293. `memoryview` requires actual bytes-like data
* The natural synergy between various Python builtins accepting an iterable (`all`, `any`, `max`, `min`, `next`, `sorted`, `sum`) and generator expressions. (N.B. `len` cannot use a generator expression) See https://stackoverflow.com/questions/9297653 (dropping parentheses), https://stackoverflow.com/questions/8534256 (clever use of `next`), https://stackoverflow.com/questions/10666163 (`all`)
* * Also `str.join` https://stackoverflow.com/questions/9060653

## Existing candidates

(N/A)