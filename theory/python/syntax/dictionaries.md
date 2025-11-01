# Dictionaries

Dictionaries are a collection of key-value pairs. They are unordered, changeable, and indexed.
They are written with curly brackets `{}` and have keys and values separated by a colon `:`.

```python
my_dict = {
    "name": "Alice",
    "age": 25,
    "city": "New York"
}
```

## Accessing Elements

You can access elements in a dictionary by their key.

```python
my_dict = {
    "name": "Alice",
    "age": 25,
    "city": "New York"
}

print(my_dict["name"])  # Alice

# If the key does not exist, you will get a KeyError
# print(my_dict["job"])  # KeyError: 'job'

# You can also use the get() method
print(my_dict.get("age"))  # 25

# If the key does not exist, you will get None
print(my_dict.get("job"))  # None
```

## Changing Values

You can change the value of a specific item by referring to its key.

```python
my_dict = {
    "name": "Alice",
    "age": 25,
    "city": "New York"
}

my_dict["age"] = 26
```

## Adding and Removing Items

You can add items to a dictionary by using a new key as shown below.

```python
my_dict = {
    "name": "Alice",
    "age": 25,
    "city": "New York"
}

my_dict["job"] = "Developer"
```

You can also remove items from a dictionary using the `pop()` method.

```python
my_dict = {
    "name": "Alice",
    "age": 25,
    "city": "New York"
}

my_dict.pop("age")
```

## Looping Through a Dictionary

You can loop through a dictionary using a `for` loop.

```python
my_dict = {
    "name": "Alice",
    "age": 25,
    "city": "New York"
}

for key in my_dict:
    print(key, my_dict[key])
```

Output:

```
name Alice
age 25
city New York
```

You can also use the `items()` method to loop through a dictionary.

```python
my_dict = {
    "name": "Alice",
    "age": 25,
    "city": "New York"
}

for key, value in my_dict.items():
    print(key, value)
```

Output:

```
name Alice
age 25
city New York
```

## Copying a Dictionary

You can copy a dictionary using the `copy()` method.

```python
my_dict = {
    "name": "Alice",
    "age": 25,
    "city": "New York"
}

new_dict = my_dict.copy()
```

You can also use the `dict()` method to copy a dictionary.

```python
my_dict = {
    "name": "Alice",
    "age": 25,
    "city": "New York"
}

new_dict = dict(my_dict)
```

## Nested Dictionaries

You can also create nested dictionaries.

```python
my_family = {
    "child1": {
        "name": "Alice",
        "age": 25
    },
    "child2": {
        "name": "Bob",
        "age": 30
    }
}
```

You can access elements in nested dictionaries by chaining the keys.

```python
my_family = {
    "child1": {
        "name": "Alice",
        "age": 25
    },
    "child2": {
        "name": "Bob",
        "age": 30
    }
}

print(my_family["child1"]["name"])  # Alice
```

## Dictionary Methods

Dictionaries have several built-in methods.

- The `keys()` method returns a list of all the keys in the dictionary.
- The `values()` method returns a list of all the values in the dictionary.
- The `items()` method returns a list of key-value pairs in the dictionary.

```python
my_dict = {
    "name": "Alice",
    "age": 25,
    "city": "New York"
}

print(my_dict.keys())  # dict_keys(['name', 'age', 'city'])
print(my_dict.values())  # dict_values(['Alice', 25, 'New York'])
print(my_dict.items())  # dict_items([('name', 'Alice'), ('age', 25), ('city', 'New York')])
```

## Dictionary Comprehension

You can create dictionaries using dictionary comprehension.

```python
my_dict = {x: x**2 for x in range(5)}

print(my_dict)  # {0: 0, 1: 1, 2: 4, 3: 9, 4: 16}
```

Dictionary comprehension can also be used to perform operations on existing dictionaries.

```python
my_dict = {
    "name": "Alice",
    "age": 25,
    "city": "New York"
}

my_dict = {k: v for k, v in my_dict.items() if k != "age"}

print(my_dict)  # {'name': 'Alice', 'city': 'New York'}
```
