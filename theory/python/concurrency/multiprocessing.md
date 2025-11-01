# Mulitprocessing

A [process](<https://en.wikipedia.org/wiki/Process_(computing)>) refers to a computer program.

Every Python program is a process and has one thread called the main thread used to execute your program instructions.
Each process is in fact one instance of the Python interpreter that executes Python instructions (Python byte-code),
which is a slightly lower level than the code you type into your Python program.

We can create new processes to run concurrently alongside our Python program.

Python provides real system-level processes via the [multiprocessing](https://docs.python.org/3/library/multiprocessing.html) module.

The underlying operating system controls how new processes are created.
On some systems that may require spawning a new process and on others it may require that the process is forked.
The operating-specific method used for creating new processes in Python is not something we need to worry about as it is managed by your installed Python interpreter.

A task can be run in a new process by creating an instance of the Process class and specifying the function to run in the new process via the “target” argument.

For example:

```python
from multiprocessing import Process

def square(x):
    print(x * x)

process = Process(target=square, args=(10,))

process.start()

process.join()
```

Running the example creates the process object to run the square() function with the argument 10.
The process is started and the square() function is executed in the child process.
The join() method is called to wait for the child process to complete before continuing with the main program.

The multiprocessing module provides a suite of synchronization primitives for developing concurrent programs with processes, including:

- Mutual exclusion locks in the multiprocessing.Lock class.
- Reentrant mutex locks in the multiprocessing.RLock class.
- Condition variables in the multiprocessing.Condition class.
- Semaphores in the multiprocessing.Semaphore class.
- Process-safe events in the multiprocessing.Event class.
- Barriers in the multiprocessing.Barrier class.

Processes do not have shared memory, instead, data is transmitted between processes using inter-process communication.

This adds a computational cost to sharing data between processes and also means that some objects cannot be shared directly or easily.

The multiprocessing module provides many conveniences for sharing data between processes.

The first is provides process-safe pipe and queue data structures for sharing data between processes, such as:

- Pipe in the multiprocessing.Pipe class.
- FIFO queue in the multiprocessing.Queue class.
- Simplified FIFO queue in the multiprocessing.SimpleQueue class.
- Joinable FIFO queue in the multiprocessing.JoinableQueue class.

The multiprocessing module also provides managers that create a server process to host Python objects and proxy objects for the hosted objects that can be shared among processes easily.

Rather than creating a new process for every task, worker processes can be reused to execute ad hoc tasks. This is a programming pattern called a process pool.

Two process pools are provided in the Python standard library, including:

- Classical process pools in the multiprocessing.pool.Pool class.
- Modern executor process pools in the concurrent.futures.ProcessPoolExecutor class.

## Process Pool

A process pool is a programming pattern for automatically managing a pool of worker processes.

The pool is responsible for a fixed number of processes.

It controls when they are created, such as when they are needed.
It also controls what they should do when they are not being used, such as making them wait without consuming computational resources.
The pool can provide a generic interface for executing ad hoc tasks with a variable number of arguments, much like the target property on the Process object,
but does not require that we choose a process to run the task, start the process, or wait for the task to complete.

### PrrocessPoolExecutor

The ProcessPoolExecutor Python class is used to create and manage process pools and is provided in the concurrent.futures module.

#### Example

```python
from concurrent.futures import ProcessPoolExecutor

def square(x):
    return x * x

with ProcessPoolExecutor() as executor:
    result = executor.submit(square, 10)
    print(result.result())
```

The result is a Future object that represents the result of the task. The result() method is called to retrieve the result of the task.

## Threads vs. Processes

A process refers to a computer program.

Each process is in fact one instance of the Python interpreter that executes Python instructions (Python byte-code),
which is a slightly lower level than the code you type into your Python program.

some systems, that may require spawning a new process, and on others, it may require that the process is forked.
The operating-specific method used for creating new processes in Python is not something we need to worry about as it is managed by your installed Python interpreter.

A thread always exists within a process and represents the manner in which instructions or code is executed.

A process will have at least one thread, called the main thread.
Any additional threads that we create within the process will belong to that process.

The Python process will terminate once all (non background threads) are terminated.

- Process: An instance of the Python interpreter has at least one thread called the MainThread.
- Thread: A thread of execution within a Python process, such as the MainThread or a new thread.
