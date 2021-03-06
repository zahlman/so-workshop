# Common Errors with JSON syntax

There seems to be growing consensus that https://stackoverflow.com/questions/2835559 should be restored to its original state, both it and https://stackoverflow.com/questions/20199126 cleaned of mentions of errors in the JSON data, and the two of them merged.

This would leave a large hole in Stack Overflow's body of knowledge: a reference for common errors in JSON syntax. While JSON data is normally generated by well tested tools, there are a variety of reasons one could end up with malformed or corrupted JSON data.

There is generally a strong compulsion to close such questions as not reproducible or caused by a typo. The thing is, they commonly are reproducible, and it is entirely possible to explain *why* the JSON data is wrong to OPs who *probably don't know*. It is useful for everyone to know and learn *specific* debugging techniques for this sort of problem.

## Setup

* OP has some data that is believed or intended to be JSON, but does not conform to the JSON specification. It may have been written 
* Trying to read this data in the usual way offers somewhat cryptic error messages.
* The goal is to *learn how to use* the error message to diagnose the problem.

## Standard solutions

Common failure modes include:

* The data is completely empty. This specific case is well covered by https://stackoverflow.com/questions/16573332, which can be referenced from here.
* The data has the wrong file encoding. Pedantically, JSON demands UTF-8, but the data could have been improperly stored or transmitted using a different encoding. This is probably out of scope, and people with this problem should instead be redirected to a question about text/file encoding generally; but our existing options for this are **also** a mess.
* The data is actually HTML or XHTML. This can happen when OP expects to connect to an API endpoint, but actually has a URL for a normal web page. It can also happen because a poorly designed API tries to present a web page to signal errors. (This might be out of scope.)
* The data is actually JSONL - basically, a separate JSON document on each line of a multi-line file. The JSON format only allows for one top-level entity per document. This can be unintentional with hand-rolled data, if OP neglected an enclosing pair of `[]`. See https://stackoverflow.com/questions/50475635/
* Hand-crafted JSON may accidentally swap `{}` for `[]` or vice versa (this is the issue shown in https://stackoverflow.com/questions/2835559)
* Hand-crafted JSON may conceivably fail to escape double-quotes etc. properly. There are even tools/programs in the wild that can get it wrong: see https://stackoverflow.com/questions/18514910
* The data is actually a stringified Python literal/display, or uses that syntax. It **may** be possible to handle this data using `ast.literal_eval`. Data like this was usually produced by a separate piece of code, which generally should be fixed to output proper JSON. It might have these particular issues:
* * using single quotes for strings
* * using Python literal `True`/`False`/`None` instead of the JSON equivalents `true`/`false`/`null`
* * trying to represent Python sets and tuples.
* The data has some form of leading garbage. This could be because 
* * it's missing enclosing `{}` (this is the issue shown in https://stackoverflow.com/questions/20199126, although the reported error message does not match)
* * it's a Python literal *and assignment statement* that was copied out of code (in which case it may have other problems, see above)
* * because of JSON hijacking protection (see https://stackoverflow.com/questions/2669690).

It's worth noting that the error reporting from the standard library `json` module was once quite a bit worse than it is now. Many old questions will complain about now-unreproducible `No JSON object could be decoded` error messages (today's error message would be more helpful).

Any canonical should probably mention the existence of online validation tools such as jsonlint.com.

## Existing candidates

None, assuming the consensus described at the beginning.