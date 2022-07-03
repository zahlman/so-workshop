# Writing a list to a file, a line at a time

We need a canonical to serve as the counterpart to https://stackoverflow.com/questions/3277503/ for writing. Very simple file writing should not require complex explanation. Example questions needing this canonical include https://stackoverflow.com/questions/72829866.

## Setup

The problem is pretty straightforward and doesn't require a lot of discussion.

* OP has a `list` of `str`s, perhaps obtained by reading another file.
* The goal is to write each string to a file, on a line by itself.
* Simply passing the `list` directly to `.write` raises an exception; working around this by converting with `str` leaves Python's list markup in the file as text (not desired).

## Standard solutions

* iterate over the `list` explicitly, writing each `str` separately
* use the `.writelines` method of the file object
* Use `.join` to make a single string and write it out
* Use `print` with a `file` argument, passing the list elements as separate arguments using `*`, and specifying a separator with the `sep` argument.

Newlines will not be inserted implicitly. If the strings already all end with `'\n'`, this is typically desirable. If they don't, however, newlines need to be inserted in order to separate the outputs. With the loop, this is a straightforward matter of adding it in the `.write` call, or even adding it separately. With `.writelines`, we need to modify the input - most easily by using a generator expression (like `f.writelines(x + '\n' for x in mylist)`. With the latter two approaches, it is simple to choose between `''` and `'\n'` as a joiner, although there is some quibbling about writing a trailing newline at the end of the file.

## Existing candidates

There is a shocking lack of symmetry with the reading canonical. The most popular candidate I could find is https://stackoverflow.com/questions/899103/, which would be a perfectly fine question except that OP had already found a working approach with `.writelines` (if it were asked today, it would be seen as codereview.SE material instead). It also contains several answers that interpreted the question as a request for generic serialization methods, and thus talk exclusively about stuff like `json` and `pickle`. There's even an answer using `numpy.savetxt` (which actually can give the right result, but is quite esoteric). It's actually not as bad overall as my initial impression, but there are answers that should definitely be moved elsewhere, and it's lacking a good summary.

I was also able to find https://stackoverflow.com/questions/13730107. The setup in the question is pretty bad: OP again already knows about `.writelines` and is specifically trying to fix the missing newlines issue. The provided example is also needlessly complex. However, the answers are fairly high quality. The accepted answer shows a variety of approaches, and touches on the broader topic of serialization (in a way appropriate to the original question: OP's data was a fit for the standard library `csv` module).

I haven't found anything else that seems at all worthy.