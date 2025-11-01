# Errors, Error Handling and Exceptions

## try / except / finally

- The `try` statement allows you to test a block of code for errors. It contains the code that may raise an exception.
- The `except` block contains the code that will be executed if an error occurs in the `try` block.
- The `finally` block contains code that will always be executed, regardless of whether an error occurs or not.

**Tip**: It is good practice to only place the code in the `try` block that could actually raise an error. This makes it easier to identify and fix the error.

```python
try:
    print(10 / 0)
except ZeroDivisionError:
    print("Division by zero is not allowed.")
finally:
    print("This will always be executed.")
```

## Error Hierarchy

```
|   |
|---|
|BaseException|
|+-- SystemExit|
|+-- KeyboardInterrupt|
|+-- GeneratorExit|
|+-- Exception|
|+-- StopIteration|
|+-- StandardError|
|\|    +-- BufferError|
|\|    +-- ArithmeticError|
|\|    \|    +-- FloatingPointError|
|\|    \|    +-- OverflowError|
|\|    \|    +-- ZeroDivisionError|
|\|    +-- AssertionError|
|\|    +-- AttributeError|
|\|    +-- EnvironmentError|
|\|    \|    +-- IOError|
|\|    \|    +-- OSError|
|\|    \|         +-- WindowsError (Windows)|
|\|    \|         +-- VMSError (VMS)|
|\|    +-- EOFError|
|\|    +-- ImportError|
|\|    +-- LookupError|
|\|    \|    +-- IndexError|
|\|    \|    +-- KeyError|
|\|    +-- MemoryError|
|\|    +-- NameError|
|\|    \|    +-- UnboundLocalError|
|\|    +-- ReferenceError|
|\|    +-- RuntimeError|
|\|    \|    +-- NotImplementedError|
|\|    +-- SyntaxError|
|\|    \|    +-- IndentationError|
|\|    \|         +-- TabError|
|\|    +-- SystemError|
|\|    +-- TypeError|
|\|    +-- ValueError|
|\|         +-- UnicodeError|
|\|              +-- UnicodeDecodeError|
|\|              +-- UnicodeEncodeError|
|\|              +-- UnicodeTranslateError|
|+-- Warning|
|+-- DeprecationWarning|
|+-- PendingDeprecationWarning|
|+-- RuntimeWarning|
|+-- SyntaxWarning|
|+-- UserWarning|
|+-- FutureWarning|
|+-- ImportWarning|
|+-- UnicodeWarning|
|+-- BytesWarning|
```

## Syntax Errors

- Syntax Errors in Python occur when the Python interpreter cannot interpret the entered code correctly. This is often due to typos or missing parentheses.

```python
print("Hello, World!"
```

The above code will raise a `SyntaxError` because the closing parenthesis is missing.

## Runtime Errors

- Runtime Errors occur when the code is syntactically correct, but an error occurs during execution.

```python
print(10 / 0)
```

The above code will raise a `ZeroDivisionError` because division by zero is not allowed.

## Custom Exceptions

- You can create custom exceptions by creating a new class that inherits from the `Exception` class.
- You can add custom attributes to the exception class to provide additional information about the error.

```python
class MyError(Exception):
    def __init__(self, message, code):
        super().__init__(message)
        self.code = code

try:
    raise MyError("An error occurred", 500)
except MyError as e:
    print(e)
    print(e.code)
```

The above code will raise a `MyError` exception with the message "An error occurred" and the code 500.

## Context Managers

- Context Managers are objects that define the runtime context to be established when executing a `with` statement (instead of using `try` and `finally`).
- They are commonly used to manage resources such as files, network connections, and database connections.

```python
with open("file.txt", "r") as file:
    print(file.read())
```
