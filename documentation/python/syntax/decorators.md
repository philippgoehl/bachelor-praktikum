# Decorators

## Creating a Simple Decorator

A simple decorator that converts the return value of a function to uppercase:

```python
def uppercase_decorator(function):
    def wrapper():
        func = function()
        make_uppercase = func.upper()
        return make_uppercase
    return wrapper
```

## Applying a Decorator with the `@` Symbol

With the `@` symbol, you can apply a decorator to a function:

```python
@uppercase_decorator
def say_hi():
    return 'hello there'


print(say_hi())
```

Output:

```
HELLO THERE
```

## Applying Multiple Decorators

You can apply multiple decorators to a function:

```python
def split_string_decorator(function):
    def wrapper():
        func = function()
        split_string = func.split()
        return split_string
    return wrapper

@split_string_decorator
@uppercase_decorator
def say_hi():
    return 'hello there'

print(say_hi())
```

Output:

```
['HELLO', 'THERE']
```

## Decorators with Arguments

You can pass arguments to a decorator:

```python
def decorator_with_args(arg1, arg2):
    def decorator(function):
        def wrapper(*args, **kwargs):
            print(f'Arguments passed to decorator: {arg1}, {arg2}')
            return function(*args, **kwargs)
        return wrapper
    return decorator

@decorator_with_args('arg1', 'arg2')
def say_hello():
    return 'hello'

print(say_hello())
```

Output:

```
Arguments passed to decorator: arg1, arg2
hello
```

## Decorators with Arguments and Functions

You can pass arguments to a decorator and a function:

```python
def decorator_with_args(arg1, arg2):
    def decorator(function):
        def wrapper(*args, **kwargs):
            print(f'Arguments passed to decorator: {arg1}, {arg2}')
            return function(*args, **kwargs)
        return wrapper
    return decorator

@decorator_with_args('arg1', 'arg2')
def say_hello(name):
    return f'hello {name}'

print(say_hello('John'))
```

Output:

```
Arguments passed to decorator: arg1, arg2
hello John
```
