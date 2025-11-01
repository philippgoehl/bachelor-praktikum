# Interators and Generators

## Basics

An iterator in Python is an object that represents a stream of data. 
It is an object that implements the iterator protocol, which consists of two methods: `__iter__()` and `__next__()`. 
The `__iter__()` method returns the iterator object itself, and the `__next__()` method returns the next element in the stream. When there are no more elements to return, the `__next__()` method raises a `StopIteration` exception.

Here is an example of a simple iterator that generates the first `n` numbers:

```python
class Numbers:
    def __init__(self, n):
        self.n = n
        self.i = 0

    def __iter__(self):
        return self

    def __next__(self):
        if self.i < self.n:
            self.i += 1
            return self.i
        else:
            raise StopIteration

numbers = Numbers(5)
for number in numbers:
    print(number)
```

Output:

```
1
2
3
4
5
```

In this example, the `Numbers` class implements the iterator protocol by defining the `__iter__()` and `__next__()` methods. 
The `__iter__()` method returns the iterator object itself, and the `__next__()` method generates the next number in the stream. 
When there are no more numbers to generate, the `__next__()` method raises a `StopIteration` exception.

## Generators

Generators are a simpler way to create iterators in Python. They are functions that use the `yield` keyword to return data. 
When a generator function is called, it returns a generator object that implements the iterator protocol.

Here is the previous example rewritten as a generator:

```python
def numbers(n):
    i = 0
    while i < n:
        i += 1
        yield i

for number in numbers(5):
    print(number)
```

Output:

```
1
2
3
4
5
```

In this example, the `numbers()` function is a generator that uses the `yield` keyword to return the next number in the stream. When the `yield` statement is reached, the function is paused, and the value is returned. 
When the function is called again, it resumes execution from where it left off.

Generators are more concise and easier to read than custom iterator classes. 
They are a powerful tool for creating iterators in Python.
