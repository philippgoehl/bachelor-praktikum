# Loops

## If ... Else

Even though If ... Else is not a loop, it is a control structure that is often used in loops.

```python
x = 10

if x > 5:
    print("x is greater than 5")
else:
    print("x is less than or equal to 5")
```

## For Loop

For loops are used to iterate over a sequence (e.g., a list, tuple, string, or dictionary).

```python
fruits = ["apple", "banana", "cherry"]

for fruit in fruits:
    print(fruit)
```

### Range Function

The `range()` function is used to generate a sequence of numbers.

```python
for x in range(6):
    print(x)

for x in range(2, 6, 3):
    # The range starts at 2, ends at 6 (not included), and increments by 3
    print(x)
```

### For Else

The `else` statement can be used with a `for` loop to execute a block of code once the loop has finished iterating over the entire sequence.

```python
fruits = ["apple", "banana", "cherry"]

for fruit in fruits:
    print(fruit)
else:
    print("Finished!")
```

## While Loop

While loops are used to execute a block of code as long as a condition is true.

```python
i = 1

while i < 6:
    print(i)
    i += 1
```

### While Else

The `else` statement can be used with a `while` loop to execute a block of code once the condition is no longer true.

```python
i = 1

while i < 6:
    print(i)
    i += 1
else:
    print("Finished!")
```

## Break Statement

The `break` statement is used to exit a loop prematurely.

```python
fruits = ["apple", "banana", "cherry"]

for fruit in fruits:
    print(fruit)
    if fruit == "banana":
        break
```

## Continue Statement

The `continue` statement is used to skip the rest of the code inside a loop for the current iteration only.

```python
fruits = ["apple", "banana", "cherry"]

for fruit in fruits:
    if fruit == "banana":
        continue
    print(fruit)
```

## Pass Statement

The `pass` statement is used as a placeholder when a statement is required syntactically but you do not want to execute any code.

```python
fruits = ["apple", "banana", "cherry"]

for fruit in fruits:
    pass
```
