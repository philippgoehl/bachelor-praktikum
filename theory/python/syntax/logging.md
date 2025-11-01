# Logging

Logging is pretty much a requirement in non-trivial, long-running systems.
It is especially useful in web applications where you can treat all exceptions in a generic way:
Just log the exception and return an error message to the caller.

When logging, it is useful to log the exception type, the error message, and the stacktrace.
All this information is available via the `sys.exc_info` object, but if you use the `logger.exception()` method in your exception handler, the Python logging system will extract all the relevant information for you.

```python
import logging
logger = logging.getLogger()

def f():
	try:
		flaky_func()
	except Exception:
		logger.exception()
		raise
```
