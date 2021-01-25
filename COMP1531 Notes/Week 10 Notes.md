# Iterators

Defining an iterator for a class so Python knows what to do with iter(object):

```python
class Square:
  def __init__(self):
    self.i = 0
  def __iter__(self):
    return self
  def __next__(self):
    self.i += 1
    return self.i * self.i
```

Iterator - stores the state of the iteration - iterable if it can be iterated over

Iterables - have just `__iter__()` methods

All iterators are iterable, but not all iterables are iterators, e.g. lists are iterable, but not iterators

For loops only need to be given something iterable

Generators: different way of writing iterators - defined via generator functions instead of classes, suspendable computation (calling next() on a generator executes it until it reaches a yield, which then suspends it until the subsequent next() call)

Generators are more efficient for big values, e.g. instead of iterating over a list of huge numbers calculated from function, but yielding each time

range() is a generator - which is why it is efficient even for large numbers

Avoid infinite yields: raise StopIteration Exception at some condition



Libraries and leftpad (Javascript library) - dependency hell

# MVP (Minimal Viable Product)

Lean Canvas - common tool used to try and articulate the core principles of a business (product and market)

![An Introduction to Lean Canvas. As an entrepreneur, one of the most… | by  Steve Mullen | Medium](https://miro.medium.com/max/1077/1*VY2L_nmmXXn4cFUyB5tXxw.jpeg)

Product-Market Fit: the degree to which a product satisfies a strong market demand

Young companies thrive to reach PMF as soon as possible - usually a key step in early growth

Verify the business viability using a MVP - sole purpose of MVP is to validate assumptions, not to build good technology

