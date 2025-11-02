# Coroutine-Based Concurrency

A [coroutine](https://en.wikipedia.org/wiki/Coroutine) is a function that can pause and resume its execution.
It allows multiple entry points for suspending and resuming execution at certain locations.

A single thread may execute many coroutines in an event loop.

Unlike threads and processes where the operating system controls when a thread or process is suspended and when it is resumed and executed, coroutines themselves control when they are suspended and resumed.

Find more about coroutine-based concurrency and the asyncio module [here](./asyncio.md).
