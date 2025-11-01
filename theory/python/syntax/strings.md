# Strings

Strings in Python are surrounded by either single quotation marks, or double quotation marks.

```python
name = 'John'
last_name = "Doe"
```

You can assign a multiline string to a variable by using three quotes.

```python
multiline_string = """This is a
multiline string"""
```

You can also use the `+` operator to concatenate strings.

```python
full_name = name + ' ' + last_name
```

You can also use the `*` operator to multiply strings.

```python
print(name * 3) # JohnJohnJohn
```

You can also access characters in a string by referring to the index number.

```python
name = 'John'
print(name[1]) # o
```

You can also slice strings.

```python
name = 'John'

# Get the characters from position 2 to position 5 (not included)
print(name[2:5]) # hn

# Get the characters from the start to position 5 (not included)
print(name[:5]) # John

# Get the characters from position 2 to the end
print(name[2:]) # hn

# Get the characters from the start to the end
print(name[:]) # John
```

You can also use the `in` keyword to check if a certain phrase or character is present in a string.

```python
name = 'John'
print('o' in name) # True
```

You can also use the `len()` function to get the length of a string.

```python
name = 'John'
print(len(name)) # 4
```

You can also use the `format()` method to insert numbers into strings.

```python
age = 30
name = 'John'
print('My name is {} and I am {} years old'.format(name, age))

# You can also use the index number to specify the order of the arguments
print('My name is {1} and I am {0} years old'.format(age, name))

# You can also use named indexes
print('My name is {name} and I am {age} years old'.format(name=name, age=age))
```

You can also use the `f-string` method to insert numbers into strings.

```python
age = 30
name = 'John'
print(f'My name is {name} and I am {age} years old')

# You can also use expressions inside the curly braces
print(f'5 times 5 is {5 * 5}')

# You can also use the `%` operator to insert numbers into strings
print('My name is %s and I am %d years old' % (name, age))
```
