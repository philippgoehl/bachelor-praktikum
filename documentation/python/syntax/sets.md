# Sets

## Basics

A set in Python is a collection that is unordered and immutable, but its elements are mutable.
This means that you cannot access and change elements by index, but you can add or remove elements.
Sets do not allow duplicates, meaning each element is unique.
They are useful for checking the existence of elements, removing duplicates, and performing mathematical operations like unions, intersections, etc.

## Creating a Set

Sets are created using curly braces {} or with the built-in set() function.

```python
# Using curly braces

my_set = {1, 2, 3}
print(my_set)

# Using the set() function

my_set = set([1, 2, 3])
print(my_set)
```

Output:

```
{1, 2, 3}
{1, 2, 3}
```

## Accessing Elements

Since sets are unordered, you cannot access elements by index.
You can loop through the set to access each element.

```python
my_set = {1, 2, 3}

for element in my_set:
    print(element)
```

Output:

```
1
2
3
```

You can also check if an element is present in a set using the `in` keyword.

```python
my_set = {1, 2, 3}

print(1 in my_set)  # True
print(4 in my_set)  # False
```

## Adding and Removing Elements

You can add elements to a set using the `add()` method and remove elements using the `remove()` method.
Another method to remove elements is `discard()`, which does not raise an error if the element is not present.

```python
my_set = {1, 2, 3}

my_set.add(4)
print(my_set)  # {1, 2, 3, 4}

my_set.remove(2)
print(my_set)  # {1, 3, 4}

my_set.discard(5)
print(my_set)  # {1, 3, 4}
```

## Set Operations

Sets support mathematical operations like `union`, `intersection`, `difference`, and `symmetric difference`.

```python
set1 = {1, 2, 3}
set2 = {3, 4, 5}

# Union
print(set1.union(set2))  # {1, 2, 3, 4, 5}

# Intersection
print(set1.intersection(set2))  # {3}

# Difference
print(set1.difference(set2))  # {1, 2}

# Symmetric Difference
print(set1.symmetric_difference(set2))  # {1, 2, 4, 5}
```

## Immutable Sets

Python also has an immutable version of sets called `frozenset`. Once created, the elements of a `frozenset` cannot be changed.

```python
my_set = frozenset([1, 2, 3])

# Attempting to add an element will raise an error
my_set.add(4)
```

Output:

```
AttributeError: 'frozenset' object has no attribute 'add'
```

## Set Comprehension

Set comprehension is a concise way to create sets using a single line of code.

```python
my_set = {x for x in range(10) if x % 2 == 0}

print(my_set)  # {0, 2, 4, 6, 8}
```

Set comprehension can also be used to perform operations on existing sets.

```python
set1 = {1, 2, 3}

set2 = {x * 2 for x in set1}

print(set2)  # {2, 4, 6}
```

Set comprehension can be used to create a set of tuples.

```python
my_set = {(x, x**2) for x in range(5)}

print(my_set)  # {(0, 0), (1, 1), (2, 4), (3, 9), (4, 16)}
```

Set comprehension can also be used to create a set of strings.

```python
my_set = {f"Number: {x}" for x in range(5)}

print(my_set)  # {'Number: 0', 'Number: 1', 'Number: 2', 'Number: 3', 'Number: 4'}
```

## Iterating Over Sets

You can iterate over sets using a `for` loop.

```python
my_set = {1, 2, 3}

for element in my_set:
    print(element)
```
