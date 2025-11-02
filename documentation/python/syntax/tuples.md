# Tuples

A tuple is a collection of objects which ordered and immutable. Tuples are written as comma-separated elements within parentheses.
Tuples are similar to lists, but they are immutable which means that once they are created, their elements cannot be changed.

Since tuples are immutable, they are faster than lists.
If you have a collection of objects that you do not want to change, you should use a tuple instead of a list.
You can also use duplicates in a tuple.

```python
my_tuple = (1, 2, 3, 4, 5, 1)
```

## Accessing Elements

You can access elements in a tuple by their index.
Tuples are zero-indexed, meaning the first element has an index of 0.

```python
my_tuple = (1, 2, 3, 4, 5)

print(my_tuple[0])  # 1
```

You can also access elements from the end of the tuple using negative indices.

```python
my_tuple = (1, 2, 3, 4, 5)

print(my_tuple[-1])  # 5
```

## Length of a Tuple

You can use the `len()` function to get the length of a tuple.

```python
my_tuple = (1, 2, 3, 4, 5)

print(len(my_tuple))  # 5
```

## Different Data Types in a Tuple

You can store different data types in a tuple.

```python
my_tuple = (1, 'Hello', 3.4)
```

## Tuple Unpacking

You can unpack a tuple into multiple variables.

```python
my_tuple = (1, 2, 3)

a, b, c = my_tuple

print(a)  # 1
```

## Tuple Methods

Tuples have two built-in methods: `count()` and `index()`.

- The `count()` method returns the number of times a specified value appears in the tuple.
- The `index()` method returns the index of the first occurrence of the specified value.

```python
my_tuple = (1, 2, 3, 4, 5, 1)

print(my_tuple.count(1))  # 2
print(my_tuple.index(3))  # 2
```

## Tuple Slicing

You can slice tuples in the same way as lists.

```python
my_tuple = (1, 2, 3, 4, 5)

print(my_tuple[2:4])  # (3, 4)
```

## Tuple Concatenation

You can concatenate tuples using the `+` operator.

```python
tuple1 = (1, 2, 3)
tuple2 = (4, 5, 6)

concatenated_tuple = tuple1 + tuple2

print(concatenated_tuple)  # (1, 2, 3, 4, 5, 6)
```

## Tuple Repetition

You can repeat a tuple using the `*` operator.

```python
my_tuple = (1, 2, 3)

print(my_tuple * 3)  # (1, 2, 3, 1, 2, 3, 1, 2, 3)
```

## Checking if an Element Exists

You can use the `in` keyword to check if an element exists in a tuple.

```python
my_tuple = (1, 2, 3)

print(1 in my_tuple)  # True
```

## Deleting a Tuple

You cannot delete individual elements in a tuple, but you can delete the entire tuple using the `del` keyword.

```python
my_tuple = (1, 2, 3)

del my_tuple
```

## Tuple with One Element

If you want to create a tuple with only one element, you need to include a comma after the element.

```python
my_tuple = (1,)
```

## Tuple without Parentheses

You can create a tuple without parentheses, but it is good practice to include them.

```python
my_tuple = 1, 2, 3
```

## Tuple with One Element without Parentheses

You can create a tuple with only one element without parentheses, but it is good practice to include them.

```python
my_tuple = 1,
```

## Tuple with Multiple Assignments

You can use tuples to assign multiple variables at once.

```python
a, b, c = 1, 2, 3
```

This is equivalent to:

```python
(a, b, c) = (1, 2, 3)
```

## Looping Through a Tuple

You can loop through a tuple using a `for` loop.

```python
my_tuple = (1, 2, 3)

for item in my_tuple:
    print(item)
```
