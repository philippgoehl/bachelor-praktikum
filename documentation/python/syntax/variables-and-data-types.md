# Variables and Types

## Naming Variables

```python
# Good
name = 'John'
last_name = 'Doe'

# Bad
n = 'John'
ln = 'Doe'
```

## Variable Types

- Text Type: `str`
- Numeric Types: `int`, `float`, `complex`
- Sequence Types: `list`, `tuple`, `range`
- Mapping Type: `dict`
- Set Types: `set`, `frozenset`
- Boolean Type: `bool`
- Binary Types: `bytes`, `bytearray`, `memoryview`
- None Type: `None`or `NoneType`

You can also specify the type of a variable - this is called type hinting and is only used for documentation purposes.

```python
name: str = 'John'
age: int = 30
```

You can also check the type of a variable using the `type()` function.

```python
name = 'John'
print(type(name)) # <class 'str'>
```

You can also convert a variable to a different type using the `int()`, `float()`, `str()`, `list()`, `tuple()`, `dict()`, `set()`, `bool()`, `bytes()`, `bytearray()`, `memoryview()` functions.

```python
x = 1
print(type(x)) # <class 'int'>

y = float(x)
print(y) # 1.0
print(type(y)) # <class 'float'>
```
