Title: Making a flat list out of list of lists
Date: 2016-01-20
Category: Python
Tags: python, lists

Sometimes we have arbitrary nested lists and we need to make them flat. There are several approaches to do that.

First of all let's view approach based on list comprehension.

```python
>>> suite = [[1, 2, 3], [4, 5, 6], [7], [8, 9]]
>>> [item for sublist in suite for item in sublist]
[1, 2, 3, 4, 5, 6, 7, 8, 9]
```

For using nested list comprehension we need to put the `for` statements in the same order as they would go in regular nested for statements.

Just like that:

```python
for sublist in suite:
    for item in sublist:
        ...
```

Another example with deeper nested list:

```python
>>> suite = [[[1, 2], [3, 4]], [[5, 6], [7, 8]], [[9, 10], [11, 12]], [[13, 14], [15]]]
>>> [item for sublist in suite for subsublist in sublist for item in subsublist]
[1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15]
```

```python
for sublist in suite:
    for subsublist in sublist:
        for item in subsublist:
            ...
```

This approach have a couple of obvious disadvantages:

* that's really ugly and hard to read
* all nested elements should have same nesting level otherwise we will get an error.

But in general for single nested lists it is ok.

[Flattening a shallow list in Python - Stack Overflow](http://stackoverflow.com/questions/406121/flattening-a-shallow-list-in-python/406296#406296)

Second approach based on [itertools.chain()](https://docs.python.org/2/library/itertools.html#itertools.chain) or [itertools.chain.from_iterable()](https://docs.python.org/2/library/itertools.html#itertools.chain.from_iterable) (if python >= 2.6).

```python
>>> suite = [[1, 2, 3], [4, 5, 6], [7], [8, 9]]
>>> list(itertools.chain(*suite))
[1, 2, 3, 4, 5, 6, 7, 8, 9]
>>> list(itertools.chain.from_iterable(suite))
[1, 2, 3, 4, 5, 6, 7, 8, 9]
```

It is easier to read and has better performance. But still doesn't care about complex nested lists.

```python
>>> suite = [[[1, 2, 3], [4, 5]], 6]
>>> list(itertools.chain.from_iterable(suite))
TypeError: 'int' object is not iterable
```

[Making a flat list out of list of lists in Python - Stack Overflow](http://stackoverflow.com/questions/952914/making-a-flat-list-out-of-list-of-lists-in-python/953097#953097)

To be aware about complex structured list of lists we need to add create advanced generator:

```python
import collections

def flatten(l):
    for el in l:
        if isinstance(el, collections.Iterable) and not isinstance(el, basestring):
            for sub in flatten(el):
                yield sub
        else:
            yield el


>>> suite = [[[1, 2, 3], [4, 5]], 6]
>>> list(flatten(suite))
[1, 2, 3, 4, 5, 6]
```

[Flatten (an irregular) list of lists in Python - Stack Overflow](http://stackoverflow.com/questions/2158395/flatten-an-irregular-list-of-lists-in-python/2158532#2158532)