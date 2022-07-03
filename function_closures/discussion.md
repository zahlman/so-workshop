# Understanding function closures

We need a clear canonical that talks about this common issue with creating functions dynamically with any sort of looping construct, where functions that are meant to be distinct end up doing the same thing.

## Setup

* OP has either a locally defined, inner function that will serve as a "template", or is trying to use `lambda` to "bind" a parameter to an existing function (partial application)
* Sometimes the template/existing function will itself be a lambda, because OP is just thinking in that mode
* The goal is to produce a list of related functions, so the code uses either a `for` loop or a list comprehension to create several callables
* The `lambda`/local template uses the iteration variable as a closure
* When the callables are evaluated, they all give the same result: they function as if the iteration variable had the *last* value from the loop/comprehension

The underlying *problem* can be characterized as either "late binding" or "lexical scoping". It has the same cause, working the same fundamental way, regardless of those variations in the setup. It is *especially* common in beginner/intermediate Tkinter code, where OP wants to create multiple buttons that do related things (e.g., calculator buttons that add a digit or operator to the input).

## Standard solutions

* abuse the "mutable default argument" behaviour, so that the value of the iteration variable is captured when the function is created (and stored in its `.__defaults__`)
* use `functools.partial` to bind an argument explicitly (my strong preference, but it may require some prep work)
* use another function or lambda to create an explicit scope (i.e., call a "factory" function that takes the iteration variable as a parameter)

## Existing candidates

https://stackoverflow.com/questions/2295290/ is by far the most popular, and frequently used, dupe target for these questions. Overall it is pretty good, but it is written to be specific to the loop setup and the lambda setup, and it gets into arguably too much technical detail in the question. Most people who encounter this problem do not need to focus on the concept of a "closure". Many people who have the problem might not recognize their situation in the question.

There are two other contenders I have in mind that have been used as targets already:

https://stackoverflow.com/questions/3431676/ shows the setup with a loop and a local function (with an alternate showing a lambda for the local function). It's written very clearly, and one of the answers covers all three standard solutions to the problem. However, it's lighter on technical info, and the setup question might be a bit *too* trivial. Since the local function/lambda just returns the closed-over iteration variable directly, it might not appear obvious that this also applies to using that variable to call a function (i.e. "bind" it to make partially applied callbacks for Tkinter etc).

Finally, there is https://stackoverflow.com/questions/452610. This is almost certainly not the best option, but it does get used a lot as a target, specifically because it shows the list comprehension setup with a `lambda` for "binding". There is an addendum to the question showing that the problem still occurs using a loop to build the list. The "template" function is needlessly written as a `lambda` itself. It has a "see also" link for another question - that is really just yet another bad duplicate, with a weirdly written MRE and misleading title. It has some weird answers (one of them uses `copy.deepcopy` on an integer!), and doesn't mention `functools.partial` anywhere. It does have some good explanation about closures and lexical scoping, though.