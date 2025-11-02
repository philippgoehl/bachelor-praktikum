# Threads

See the official Thread documentation [here](https://docs.python.org/3/library/threading.html).

Every Python program is a process with one thread called the main thread used to execute your program instructions.
Each process is in fact one instance of the Python interpreter that executes Python instructions (Python byte-code),
which is a slightly lower level than the code you type into your Python program.

Sometimes, we may need to create additional threads within our Python process to execute tasks concurrently.
Python provides real naive (system-level) threads via the `threading.Thread class`.

A task can be run in a new thread by creating an instance of the Thread class and specifying the function to run in the new thread via the target argument.

```python
import threading

def print_numbers():
    for i in range(1, 11):
        print(i)

# Create a new thread
thread = threading.Thread(target=print_numbers)

# Once the thread is created, you can start it by calling the start() method.
thread.start()

# The main thread will continue to execute the code below while the new thread runs in the background.
print("Main thread")

# The join() method can be used to wait for the thread to finish before continuing.
thread.join()
```

The thread is started and the print_numbers function is executed in the new thread.
The main thread continues to execute the code below the thread.start() method.
This is useful for running one-off tasks in a separate thread, although it becomes cumbersome when you have many tasks to run.

## Thread Safety

The threading module provides a suite of synchronization primitives for developing concurrent programs with threads, including:

- Mutual exclusion locks in the threading.Lock class.
- Reentrant mutex locks in the threading.RLock class.
- Condition variables in the threading.Condition class.
- Semaphores in the threading.Semaphore class.
- Thread-safe events in the threading.Event class.
- Barriers in the threading.Barrier class.

It also provides thread-safe queue data structures in the “queue” module, such as:

- FIFO queue in the queue.Queue class.
- Simplified FIFO queue in the queue.SimpleQueue class.
- LIFO queue in the queue.LifoQueue class.
- Priority queue in the queue.PriorityQueue class.

Examples of blocking IO operations include:

- Reading or writing a file from the hard drive.
- Reading or writing to standard output, input, or error (stdin, stdout, stderr).
- Printing a document.
- Reading or writing bytes on a socket connection with a server.
- Downloading or uploading a file.
- Querying a server.
- Querying a database.
- Taking a photo or recording a video.

And so much more.
The key is that the operation is blocking, meaning that the thread will wait for the operation to complete before continuing.
Rather than creating a new thread for every task, worker threads can be reused to execute tasks.
This is a programming pattern called a thread pool.

## Thread Pool

Each thread that is created requires the application of resources (e.g. memory for the thread’s stack space).
The computational costs for setting up threads can become expensive if we are creating and destroying many threads over and over for tasks.

Instead, we would prefer to keep worker threads around for reuse if we expect to run many tasks throughout our program.
This can be achieved using a thread pool.

Two thread pools are provided in the Python standard library, including:

- Classical thread pools in the multiprocessing.pool.ThreadPool class.
- Modern executor thread pools in the concurrent.futures.ThreadPoolExecutor class.

A [thread pool](https://en.wikipedia.org/wiki/Thread_pool) is a programming pattern for automatically managing a pool of worker threads.

The pool is responsible for a fixed number of threads.
It controls when the threads are created, such as just-in-time when they are needed.
It also controls what threads should do when they are not being used, such as making them wait without consuming computational resources.

Each thread in the pool is called a worker or a worker thread.
Each worker is agnostic to the type of tasks that are executed,
along with the user of the thread pool to execute a suite of similar (homogeneous) or dissimilar tasks (heterogeneous) in terms of the function called, function arguments, task duration, and more.

Worker threads are designed to be re-used once the task is completed and provide protection against the unexpected failure of the task, such as raising an exception,
without impacting the worker thread itself.
This is unlike a single thread that is configured for the single execution of one specific task.

The pool may provide some facility to configure the worker threads, such as running an initialization function and naming each worker thread using a specific naming convention.
Thread pools can provide a generic interface for executing tasks with a variable number of arguments, but do not require that we choose a thread to run the task, start the thread, or wait for the task to complete.

It can be significantly more efficient to use a thread pool instead of manually starting, managing, and closing threads, especially with a large number of tasks.

### ThreadPool in Python

The [multiprocessing.pool.ThreadPool](https://docs.python.org/3/library/multiprocessing.html#multiprocessing.pool.ThreadPool) provides a pool of reusable threads for executing tasks.

The ThreadPool class extends the Pool class.
The Pool class provides a pool of worker processes for process-based concurrency.
Although the ThreadPool class is in the multiprocessing module it offers thread-based concurrency.

We can create a thread pool by instantiating the ThreadPool class and specifying the number of threads via the “processes” argument; for example:

```python
from multiprocessing.pool import ThreadPool

pool = ThreadPool(processes=4)
```

We can issue one-off tasks to the ThreadPool using methods such as apply() or we can apply the same function to an iterable of items using methods such as map().
The map() function matches the built-in map() function and takes a function name and an iterable of items. The target function will then be called for each item in the iterable as a separate task in the thread pool. An iterable of results will be returned if the target function returns a value.

```python
from multiprocessing.pool import ThreadPool

def square(x):
    return x * x

pool = ThreadPool(processes=4)

results = pool.map(square, range(10))

print(results)

# Output: [0, 1, 4, 9, 16, 25, 36, 49, 64, 81]
```

The above code will create a thread pool with four threads and apply the square function to each item in the range(10) iterable.
The results will be printed to the console.

We can issue tasks asynchronously to the ThreadPool, which returns an instance of an AsyncResult immediately.
One-off tasks can be used via apply_async(), whereas the map_async() offers an asynchronous version of the map() method.

The AsyncResult object provides a handle on the asynchronous task that we can use to query the status of the task, wait for the task to complete, or get the return value from the task, once it is available.

For example:

```python
from multiprocessing.pool import ThreadPool

def square(x):
    return x * x

pool = ThreadPool(processes=4)

result = pool.apply_async(square, (10,))

print(result.get())

# Output: 100
```

Once we are finished with the ThreadPool, it can be shut down by calling the close() method in order to release all of the worker threads and their resources.

For example:

```python
from multiprocessing.pool import ThreadPool

def square(x):
    return x * x

pool = ThreadPool(processes=4)

results = pool.map(square, range(10))

print(results)

pool.close()
```

The life-cycle of creating and shutting down the thread pool can be simplified by using the context manager that will automatically close the ThreadPool.

```python
from multiprocessing.pool import ThreadPool

def square(x):
    return x * x

with ThreadPool(processes=4) as pool:
    results = pool.map(square, range(10))

print(results)
```

### ThreadPoolExecutor in Python

It offers easy-to-use pools of worker threads via the modern executor design pattern.
It is ideal for making loops of I/O-bound tasks concurrent and for issuing tasks asynchronously.

The ThreadPoolExecutor class extends the abstract Executor class.
The Executor class defines three methods used to control our thread pool; they are: submit(), map(), and shutdown().

- submit(): Dispatch a function to be executed and return a future object.
- map(): Apply a function to an iterable of elements.
- shutdown(): Shut down the executor.

The Executor is started when the class is created and must be shut down explicitly by calling shutdown(), which will release any resources held by the Executor. We can also shut down automatically, by using the context manager (see below).

#### Full example of ThreadPoolExecutor from the concurrent.futures module and map()

```python
from concurrent.futures import ThreadPoolExecutor

def square(x):
    return x * x

with ThreadPoolExecutor(max_workers=4) as executor:
    results = executor.map(square, range(10))

print(list(results))
```

#### Full example of ThreadPoolExecutor from the concurrent.futures module and submit()

```python
from concurrent.futures import ThreadPoolExecutor

def square(x):
    return x * x

with ThreadPoolExecutor(max_workers=4) as executor:
    future = executor.submit(square, 10)
    print(future.result())
```

The difference here is that the submit() method returns a future object immediately, which can be used to query the status of the task, wait for the task to complete, or get the return value from the task, once it is available.

#### Futures

In Python, the Future object is returned from an Executor, such as a ThreadPoolExecutor when calling the submit() function to dispatch a task to be executed asynchronously.
In general, we do not create Future objects; we only receive them and we may need to call functions on them.

Functions that can be called on a Future object include:

- cancel(): Attempt to cancel the execution of the future. Returns True if the future was cancelled successfully.
- cancelled(): Returns True if the future was cancelled.
- running(): Returns True if the future is currently executing.
- done(): Returns True if the future has completed execution.
- result(timeout=None): Return the result of the future. If the future is not done, this method will wait up to timeout seconds for the future to complete. If the future is not done and the timeout is reached, a TimeoutError will be raised.
- exception(timeout=None): Return the exception raised by the future. If the future completed successfully, this method will return None. If the future is not done, this method will wait up to timeout seconds for the future to complete. If the future is not done and the timeout is reached, a TimeoutError will be raised.
- add_done_callback(fn): Attaches the callable fn to the future. fn will be called with the future as the only argument when the future is completed or cancelled.
