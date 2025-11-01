# Asyncio

Asyncio is a library in Python that allows for asynchronous programming,
making it easier to write and manage I/O-bound programs using an event loop.

Asyncio provides a framework for writing single-threaded concurrent code using coroutines,
which can yield control to allow other coroutines to run.

This is particularly useful in I/O-bound operations (like web requests or database queries), helping to keep your program responsive.

## Key Components

### Event Loop

The event loop is the core of Asyncio.
It runs in a single thread and manages the execution of multiple coroutines and tasks.

You can start the event loop using:

```python
import asyncio

asyncio.run(main())
```

### Coroutines

Coroutines are special functions that can pause execution and yield control back to the event loop.

They are defined using the `async def` syntax:

```python
async def my_coroutine():
    print("Hello")
    await asyncio.sleep(1)
    print("World")
```

### Tasks

Tasks are a higher-level wrapper for coroutines.
They allow coroutines to run concurrently.

You can create a task using:

```python
task = asyncio.create_task(my_coroutine())
```

### Futures

Futures represent a result that hasn't been computed yet.
They are essentially placeholders for results of asynchronous operations.

## Basic Usage

To effectively use Asyncio, you'll typically follow these steps:

1. Define your coroutines.
2. Create tasks from those coroutines.
3. Use the event loop to execute the tasks.

## Example

Here’s a simple coroutine to demonstrate its functionality:

```python
import asyncio

async def say_hello():
    print("Hello")
    await asyncio.sleep(1)
    print("world")

if __name__ == "__main__":
    asyncio.run(say_hello())
```

Output:

```
Hello
world
```

## Running Multiple Coroutines

You can run multiple coroutines concurrently using `asyncio.gather()`:

```python
import asyncio

async def say_after(delay, message):
    await asyncio.sleep(delay)
    print(message)

async def main():
    await asyncio.gather(
        say_after(1, 'Hello'),
        say_after(2, 'World'),
        say_after(3, 'from asyncio!')
    )

if __name__ == "__main__":
    asyncio.run(main())
```

Output:

```
Hello
World
from asyncio!
```

## Using Async/Await Syntax

### Defining and Calling Coroutines

You can define and call coroutines using the `async` and `await` keywords:

```python
import asyncio

async def countdown(number):
    while number > 0:
        print(number)
        await asyncio.sleep(1)
        number -= 1

async def main():
    await countdown(5)

if __name__ == "__main__":
    asyncio.run(main())
```

Output:

```
5
4
3
2
1
```

## Error Handling in Asyncio

Errors can be handled within coroutines using standard try-except blocks:

```python
import asyncio

async def risky_coroutine():
    await asyncio.sleep(1)
    raise Exception("Something went wrong!")

async def main():
    try:
        await risky_coroutine()
    except Exception as e:
        print(f"Caught an error: {e}")

if __name__ == "__main__":
    asyncio.run(main())
```

Output:

```
Caught an error: Something went wrong!
```
