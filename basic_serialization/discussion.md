# Basic Serialization

## Setup

* OP has some kind of structured data - a class instance; nested dicts and lists; a Pandas Dataframe; a Numpy array...
* The goal is to write the data into a file in an appropriate way, such that the original structure can be recovered on a later run of the program.

## Standard solutions

There is nothing one-size-fits-all here; the goal is to direct OP to the best solution depending on the nature of the data. Important tools include:

* Native Python serialization (`pickle` and perhaps `shelve` and `marshal`)
* Serialization to standard data formats (most notably JSON, but variants like TOML should be mentioned, and even XML is worth consideration)
* Serialization to specific formats that are idiosyncratic to the data (Numpy/Pandas/Torch built-in functionality)
* CSV for tabular data
* Very simple data can be coerced to a string that can be parsed again with `ast.literal_eval`. This is limited and should be heavily discouraged (*especially* do not suggest using `eval` anywhere).

## Existing candidates

TBD. My notes include

* https://stackoverflow.com/questions/4547274
* https://stackoverflow.com/questions/4529815
* https://stackoverflow.com/questions/42703500
* https://stackoverflow.com/questions/2259270
* https://stackoverflow.com/questions/3438675
* https://stackoverflow.com/questions/1253528
* https://stackoverflow.com/questions/8968884
* https://stackoverflow.com/questions/27745500
* https://stackoverflow.com/questions/33686747
* https://stackoverflow.com/questions/899103 (already part of the discussion for "writing a list to a file a line at a time", which is a simpler task than serialization)

A lot of the most popular questions that come up in a search for `[python] serialization` are about the details of using JSON, which prompts yet another cleanup....