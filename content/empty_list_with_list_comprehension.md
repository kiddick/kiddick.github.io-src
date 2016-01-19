Title: Empty list by list comprehension
Date: 2016-01-19
Category: Python
Tags: python, lists

We will view some interesting case with list comprehension in python. Actually we have the spoiler in the name of the article. But don't worry.

What if when we are trying to create a new list by list comprehension with some condition and no element would meet requirements?

Let's check this out.

```python
>>> suite = range(10)
>>> suite
Out[2]: [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]

>>> [i for i in suite if i < 0]
Out[3]: []

>>> [i for i in suite if i < 0][0]
IndexError: list index out of range
```

As you can see we are just getting an empty list.

We need to care about such edge cases since it may lead to errors.
And if we need to get an element by index we should verifications or error handling with exceptions.
