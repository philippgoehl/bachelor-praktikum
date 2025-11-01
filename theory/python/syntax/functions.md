# Functions

Functions are blocks of code that can be called to perform a specific task. They are defined using the `def` keyword, followed by the function name, a list of parameters, and a colon.
The function body is indented and contains the code that will be executed when the function is called.

```python
def greet(name):
    print(f"Hello, {name}!")

greet("Alice")  # Hello, Alice!
```

## Arguments

Functions can take arguments, which are values passed to the function when it is called.
Arguments are specified in the function definition within the parentheses.

```python
def greet(name):
    print(f"Hello, {name}!")

greet("Alice")  # Hello, Alice!
```

Functions can take multiple arguments.

```python
def greet(name, age):
    print(f"Hello, {name}! You are {age} years old.")

greet("Alice", 25)  # Hello, Alice! You are 25 years old.
```

### Arbitrary Arguments (\*args)

If you do not know how many arguments will be passed to a function, you can use the `*args` syntax to pass a variable number of arguments.

```python
def greet(*names):
    for name in names:
        print(f"Hello, {name}!")

greet("Alice", "Bob", "Charlie")  # Hello, Alice! Hello, Bob! Hello, Charlie!
```

### Arbitrary Keyword Arguments (\*\*kwargs)

You can also pass keyword arguments to a function using the `**kwargs` syntax.
Keyword arguments are passed as key-value pairs.

```python
def greet(**person):
    print(f"Hello, {person['name']}! You are {person['age']} years old.")

greet(name="Alice", age=25)  # Hello, Alice! You are 25 years old.
```

## Default Parameter Value

You can specify a default value for a parameter in a function.
If the function is called without passing a value for that parameter, the default value will be used.

```python
def greet(name="Alice"):
    print(f"Hello, {name}!")

greet()  # Hello, Alice!
greet("Bob")  # Hello, Bob!
```

## Return Values

Functions can return a value using the `return` keyword.
The returned value can be stored in a variable or used in other parts of the code.

```python
def add(a, b):
    return a + b

result = add(3, 5)
print(result)  # 8
```

If a function does not have a `return` statement, it will return `None`.

```python
def greet(name):
    print(f"Hello, {name}!")

result = greet("Alice")
print(result)  # None
```

## Positional-Only Arguments

You can specify that certain arguments must be passed by position and cannot be passed by keyword.

```python
def greet(name, /, greeting="Hello"):
    print(f"{greeting}, {name}!")

greet("Alice")  # Hello, Alice!
greet("Alice", "Hi")  # Hi, Alice!

# This will raise an error
# greet(name="Alice", greeting="Hi")
# TypeError: greet() got some positional-only arguments passed as keyword arguments: 'name'

# This will also raise an error
# greet(name="Alice")

# This will not raise an error
# greet("Alice", greeting="Hi")
```

## Keyword-Only Arguments

You can specify that certain arguments must be passed by keyword and cannot be passed by position.

```python
def greet(*, name, greeting="Hello"):
    print(f"{greeting}, {name}!")

greet(name="Alice")  # Hello, Alice!

# This will raise an error
# greet("Alice")
# TypeError: greet() takes 0 positional arguments but 1 was given
```

## Docstrings and Annotations

You can add documentation to a function using docstrings.
Docstrings are enclosed in triple quotes and are used to describe the purpose of the function.
You can also add type annotations to the function parameters and return value.

```python
def greet(name: str) -> str:
    """
    This function greets the person with the given name.

    Args:
        name (str): The name of the person to greet.

    Returns:
        str: A greeting message.
    """
    print(f"Hello, {name}!")
    return "Greeted"
```

## Lambda Functions

Lambda functions are small, anonymous functions defined using the `lambda` keyword.
They can have any number of arguments but can only have one expression.

Syntax:

```python
lambda arguments: expression
```

Example:

```python
add = lambda a, b: a + b

result = add(3, 5)
print(result)  # 8

# Equivalent to:
def add(a, b):
    return a + b
```

Lambda functions are often used as arguments to higher-order functions, such as `map()`, `filter()`, and `reduce()`.

```python
numbers = [1, 2, 3, 4, 5]

squared = list(map(lambda x: x**2, numbers))
print(squared)  # [1, 4, 9, 16, 25]

evens = list(filter(lambda x: x % 2 == 0, numbers))
print(evens)  # [2, 4]

total = reduce(lambda a, b: a + b, numbers)
print(total)  # 15
```

## Recursion

Recursion is a technique in which a function calls itself to solve smaller instances of the same problem.
A recursive function consists of two parts: the base case, which determines when the function should stop calling itself, and the recursive case, which defines how the function calls itself with a smaller instance of the problem.

Example:

```python
def factorial(n):
    if n == 0:
        return 1
    else:
        return n * factorial(n - 1)

result = factorial(5)
print(result)  # 120
```

## map(), filter(), and reduce()

`map()`, `filter()`, and `reduce()` are higher-order functions that take a function as an argument.

`map()` applies a function to each item in an iterable and returns a list of the results.

```python
numbers = [1, 2, 3, 4, 5]

squared = list(map(lambda x: x**2, numbers))
print(squared)  # [1, 4, 9, 16, 25]
```

`filter()` applies a function to each item in an iterable and returns a list of items for which the function returns `True`.

```python
numbers = [1, 2, 3, 4, 5]

evens = list(filter(lambda x: x % 2 == 0, numbers))
print(evens)  # [2, 4]
```

`reduce()` applies a function to the first two items in an iterable, then applies the function to the result and the next item, and so on, until the iterable is exhausted, returning a single value.

```python
from functools import reduce

numbers = [1, 2, 3, 4, 5]

total = reduce(lambda a, b: a + b, numbers)
print(total)  # 15
```
