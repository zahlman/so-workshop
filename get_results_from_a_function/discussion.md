# Getting results from a function

We need a canonical to explain how to communicate the results from calling a function back to the rest of the program. This is a separate issue from confusion between `print` and `return`; this is about the need for `return` in the first place, *as well as* alternate ways to solve the problem (such as globals, which are hard to ignore in this context).

## Setup

* OP wants to gain access to information computed by a function, after calling it.

There are at least two conceptually distinct ways that the problem may present, and *many* ways that beginners might fumble around trying to explain it.

1) Usually, OP has a mental model that involves getting information "out of" the function, and simply does not understand how `return` works. Very commonly, OP will expect `return` to "return a variable" that can be used in the caller's namespace, like:
```
def x():
   y = 1
   return y

x()
print(y)
```
OPs like this often do not have a clear mental distinction between global and local variables, but that is a separate issue. (https://stackoverflow.com/questions/291978/ is our canonical for explaining variable scope in Python, but it's possibly too technical for beginners and also is separate from the question they're actually asking.)

2) Other OPs have a mental model that involves "reaching into" the function from outside. Typically, they conceptualize a function's local variables as "part of" the function, which leads them to think in terms of either function attributes or somehow using `locals()`. Occasionally, there is someone who understands that the local variables are not attributes, but wishes to *make* them attributes for some contrived reason.

In special cases, OP wants to use the use the `locals()` that result from executing the function from outside, for some metaprogramming purpose: e.g. https://stackoverflow.com/questions/9186395/ and https://stackoverflow.com/questions/4214936/. One or both of these can probably be considered a separate question, but *almost everyone* who asks about this should be questioned as to what they really want.

Many, **many** beginners will describe the problem in a way that makes it sound like they want to know how to use global variables. Giving them that canonical, https://stackoverflow.com/questions/423379/, is *usually doing them a great disservice*.

## Standard solutions

In almost every case, the problem should be solved by `return`ing a value and using it properly in the caller. For completeness, though, the canonical should cover all viable methods:

* Return a value with `return`
* Assign to, or modify, a global
* * As a special case, assign to a function attribute (this is modifying a global)
* Modify a function parameter
* * As a special case, modify `self` in a method

It specifically needs to explain:

* Functions *return values, not variables*
* The `return` statement can use any expression (technically, `star_expressions`, but that is *way* beyond scope)
* A *call* to the function *is an expression* which can be used as a part of a larger expression, without needing to assign the result to a local variable: `f(x) + 1`
* Assigning or modifying a global variable is not modular; code that mutates the global state is harder to reason about, and this approach generally breaks recursive code
* Assigning to *the function's name itself* will replace the function and break subsequent attempts to use it (this does work properly in Visual Basic, and possibly some other languages! So there is at least a possibility that people will try it)
* Using a function attribute is "modifying a global variable", and has the same caveats
* Modifying a parameter to the function is usually discouraged, but has its uses and is the basis of OOP
* *Assigning to* a function parameter *will not work*; even though the *values* are shared, the parameters are local *names*

## Existing candidates

The clear candidate is https://stackoverflow.com/questions/16043797/, but it needs a lot of work. The question uses 2.x syntax and un-Pythonic naming (it even shadows the `list` builtin). It only shows one specific setup for the problem (although it's arguably one of the best). The one answer mentioning global variables is low quality, and there are some other answers that are even worse. There is nothing about function attributes specifically, or about modifying the inputs.

Then we have https://stackoverflow.com/questions/19326004/. Weirdly, this is the most popular question I could find that's even remotely related to the topic, despite an endless torrent of such questions. Because of how the question was asked, it got answers focused entirely on the use of function attributes, and the top answer in particular has way too much weight. It's been used many times as a duplicate for this kind of question, and many beginners are led astray this way.

Everything else is even less notable. I actually tried scanning through every single Python question with a score over 100 and matching a couple of keywords like "function return" etc. - no dice.

Notable among the lower scoring questions (I don't think any of these is plausibly the best choice, so I haven't included them in the repository):

https://stackoverflow.com/questions/32822473/ has 36k views. The setup is fairly simple, although the question could be asked more explicitly. Existing answers cover the normal use of `return`, globals, and attributes of `self` in methods; but overall I don't think the content here is as good.

https://stackoverflow.com/questions/40801789/ has 59k views. The setup is needlessly complex and not at all an MRE. OP describes what appear to be methods of a class as "functions", and does not show the class, leading to some confusion. It also uses 2.x syntax. However, the top-voted answer at least covers several bases and is well written.

For example, https://stackoverflow.com/questions/52209825/ is terribly written, has a low score and has only rarely been used as a duplicate target. The one provided answer seems to think that OP has the "print vs return" confusion (a separate issue) because of how poorly written the question is. *However, it still has 11k views somehow*.