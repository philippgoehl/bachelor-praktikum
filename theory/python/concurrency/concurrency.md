# Concurrency in Python

Find the complete guide [here](https://superfastpython.com).

Python concurrency refers to a suite of capabilities provided by specific Python modules and in some cases (coroutines) the Python language itself.
The capabilities are not provided by other means and have to do with executing code simultaneously, asynchronously, and /or in parallel.
These capabilities are implemented in specific Python modules in the standard library such as the “threading“, “multiprocessing“, and “asyncio” modules.

## Overview

Concurrency, broadly conceived, bring three new capabilities, they are:

- Concurrent execution.
- Parallel execution.
- Asynchronous execution.

They are different but related.

### Concurrent Execution

[Concurrent execution](<https://en.wikipedia.org/wiki/Concurrency_(computer_science)>) is a pre-condition for parallel and asynchronous execution.
Concurrent means that pieces of a program can run out of order, or overlap in some way.
It does not mean that the execution “will” be out of order or will overlap with each other, only that it “can” be.
Concurrent means simultaneous or at the same time, as opposed to asynchronous which means not at the same time.

Concurrent programming refers to a type of programming focused on executing independent tasks at the same time.
For example, when programming, if we refer to two or more tasks as executing concurrently, we mean that they execute at the same time.
Concurrency is about multiple tasks that can happen independently from one another.
This means that concurrent tasks may execute in any order, such as in parallel, overlapping, interleaved, and more.

Let’s make concurrency concrete. We do things concurrently all the time.
We could drive, then talk, but that would be strange. Instead, we do both things concurrently.

Unlike traditional programming where instructions or tasks are executed one after the other,
concurrent programming allows multiple tasks to make progress at the same time.
It facilitates other types of programming, such as parallel programming where tasks are executed simultaneously on separate CPUs.

Just like functions allow a long program to be split into discrete pieces and reused.
An atom of concurrent execution, like a lambda, function, or method, can be executed at some potentially overlapping time with another atom of concurrent execution.

For example, we may read from 3 files concurrently.
There is a prescription that the tasks are separate and that each can happen at an arbitrary time, although there are many ways this could be achieved.

The files could be read a little bit each in a round-robin until completed.
They could each be read in parallel (discussed next), they could be read asynchronously and the caller may check in on the results later.

Concurrent execution facilitates “concurrency” implementation details, just like subroutines facilitate reuse.
Details like pre-emptive multitasking, cooperative multitasking, and parallel execution.

Let’s look at a diagram that might make concurrent execution clearer:

![Concurrency](/_images/backend/concurrency/concurrency.webp)

The diagram shows the concurrent execution of three tasks.
Time executing the tasks starts at the top of the chart and travels down, one step at a time.

We can see that in this case, although all three tasks are executed concurrently, only one task is actually executed at a time.
Nevertheless, they all make progress.

### Parallel Execution

[Parallel execution](https://en.wikipedia.org/wiki/Parallel_computing) means being executed at the same time.
Parallel means simultaneous, which sounds a lot like the definition of concurrent above.
In programming, parallel has a slightly different meaning.
Parallel tasks are executed strictly at the same time.
Concurrent tasks may execute at the same time, or not.
Their order is not prescribed. Parallel tasks are concurrent tasks that specify that they are to be completed at the same time.

Therefore, concurrency is a precondition for parallelism.

- Concurrent tasks may parallel tasks.
- Parallel tasks are concurrent tasks.

As such, parallel execution is typically a function of the parallelism of the underlying hardware.
This may mean multiple GPUs or CPUs, multiple cores per CPU, multiple machines, and so on.

For example:

- We may complete task1, then complete task2 (sequential).
- We may do a little of task1, all of task2, then the rest of task1 (overlapping).
- We may do a little of task1, a little of task2, a little of task1, and so on (interleaved).
- We may perform task1 and task 2 at the same time (parallel).

The tasks are examples of completing the tasks concurrently.
They are happening at the same time, although the caller is not interested in how they are being performed.

Parallelism is often what is meant when describing python concurrency casually, e.g. that we want things to happen at the same time.

In practice, parallelism allows the full or fuller extent of the underlying hardware to be utilized.
This means we may be able to run on all CPUs or all cores, instead of one.

It may mean that a series of sequential tasks can be completed in the time it takes to complete one task, offering a speed-up and in turn scalability of a program.

Let’s look at a diagram that might make parallel execution clearer.

![Parallelism](/_images/backend/concurrency/parallelism.webp)

The diagram shows the parallel execution of three tasks.
Time executing the tasks starts at the top of the chart and travels down, one step at a time.

We can see that all three tasks are started at the same time, concurrently.
In this case, we can see that each task is able to execute each time step, allowing all tasks to make progress simultaneously.

### Asynchronous Execution

[Asynchronous execution](<https://en.wikipedia.org/wiki/Asynchrony_(computer_programming)>) means not at the same time, e.g. at some later time.

It may be in parallel. It may be when there are sufficient resources. It may be when there’s time.
It may be when we choose to suspend and allow it.

Asynchronous execution facilitates a new programming style, called asynchronous programming.
Asynchronous programming is a programming paradigm that does not block.

Instead, requests and function calls are issued and executed somehow in the background at some future time.
This frees the caller to perform other activities and handle the results of issued calls at a later time when results are available or when the caller is interested.

Tasks and function calls can be dispatched and results handled later, as required.
External events can trigger the execution of functions as required.
In turn, this can require far fewer resources, and in turn, supports significantly more concurrent tasks.

This approach is most common when using non-blocking I/O.

Let’s look at a diagram that might make asynchronous execution clearer.

![Asynchronous](/_images/backend/concurrency/asynchronous.webp)

The diagram shows the asynchronous execution of three tasks.
Time executing the tasks starts at the top of the chart and travels down, one step at a time.

One task is started and then schedules a second task.
The first task continues for a moment.
The second task is then given an opportunity to execute and schedules the third task.
The third task then runs and completes.
The second task completes and the first task runs a moment longer.

All three tasks are executed concurrently, although in a different manner from what we have seen previously.

When programming, asynchronous means that the action is requested, although not performed at the time of the request.
It is performed later.

For example, we can make an asynchronous function call.

This will issue the request to make the function call and will not wait around for the call to complete.
We can choose to check on the status or result of the function call later.

Asynchronous Function Call: Request that a function is called at some time and in some manner, allowing the caller to resume and perform other activities.
The function call will happen somehow and at some time, in the background, and the program can perform other tasks or respond to other events.

This is key. We don’t have control over how or when the request is handled, only that we would like it handled while the program does other things.

Issuing an asynchronous function call often results in some handle on the request that the caller can use to check on the status of the call or get results.
This is often called a future.

#### Future

A handle on an asynchronous function call allowing the status of the call to be checked and results to be retrieved.
The combination of the asynchronous function call and future together are often referred to as an asynchronous task.
This is because it is more elaborate than a function call, such as allowing the request to be canceled and more.

#### Asynchronous Task

Used to refer to the aggregate of an asynchronous function call and resulting future.
Issuing asynchronous tasks and making asynchronous function calls is referred to as asynchronous programming.

#### Asynchronous Programming

The use of asynchronous techniques, such as issuing asynchronous tasks or function calls.
Asynchronous programming is primarily used with non-blocking I/O, such as reading and writing from socket connections with other processes or other systems.
Non-blocking I/O is a way of performing I/O where reads and writes are requested, although performed asynchronously.
The caller does not need to wait for the operation to complete before returning.

The read and write operations are performed somehow (e.g. by the underlying operating system or systems built upon it), and the status of the action and/or data is retrieved by the caller later, once available, or when the caller is ready.

#### Non-blocking I/O

Performing I/O operations via asynchronous requests and responses, rather than waiting for operations to complete.
As such, we can see how non-blocking I/O is related to asynchronous programming.
In fact, we use non-blocking I/O via asynchronous programming or non-blocking I/O is implemented via asynchronous programming.

The combination of non-blocking I/O with asynchronous programming is so common that it is commonly referred to by the shorthand of asynchronous I/O.

#### Asynchronous I/O

A shorthand that refers to combining asynchronous programming with non-blocking I/O.

## Types of Concurrency in Python

- Process-Based Concurrency: See [here](./multiprocessing.md).
- Thread-Based Concurrency: See [here](./threads.md).
- Coroutine-Based Concurrency: See [here](./coroutines.md).
