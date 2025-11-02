# Classes

Classes are a way to bundle data and functionality together.
Creating a new class creates a new type of object, allowing new instances of that type to be made. Each class instance can have attributes attached to it for maintaining its state.
Class instances can also have methods (defined by its class) for modifying its state.

```python
class MyClass:
    x = 5

# Create an object of the class
obj = MyClass()

print(obj.x)  # 5
```

## Class Constructor (`__init__`)

The `__init__` method is a special method that is called when a class is instantiated.
It is used to initialize the object's attributes.

```python
class Person:
    def __init__(self, name, age):
        self.name = name
        self.age = age

# Create an object of the class
person = Person("Alice", 25)

print(person.name)  # Alice
print(person.age)  # 25
```

## The `__str__` Method

The `__str__` method is a special method that is called when the `str()` function is used on the object.
It should return a string representation of the object.

```python
class Person:
    def __init__(self, name, age):
        self.name = name
        self.age = age

    def __str__(self):
        return f"{self.name} is {self.age} years old"

# Create an object of the class
person = Person("Alice", 25)

print(str(person))  # Alice is 25 years old
```

## Class and Instance Variables

Class variables are shared among all instances of a class, while instance variables are unique to each instance.

```python
class Person:
    # Class variable
    species = "Homo sapiens"

    def __init__(self, name, age):
        # Instance variable
        self.name = name
        self.age = age

# Set the class variable
Person.species

# Create an object of the class
person = Person("Alice", 25)

print(person.name)  # Alice
print(person.age)  # 25
```

Every Person object shares the class variable species, meaning all instances of the class will have the same value for this variable unless it is explicitly modified at the class level.
However, each Person object has its own unique instance variables name and age, which are specific to each instance of the class.

For instance:
The class variable species is shared among all Person objects.
If you print Person.species, it will display "Homo sapiens", and every instance of Person will have access to this value.
The instance variables name and age are set individually when creating new instances of the class.
In the example, the object person has name set to "Alice" and age set to 25, and this data is unique to the person object.

## Instance-, Static- and Object Methods

### Instance Methods

Instance methods are the most common type of method.
They take self as the first parameter, which refers to the instance of the class.
Instance methods can access and modify instance variables, and can also call other methods defined in the class.

```python
class Person:
    species = "Homo sapiens"  # Class variable

    def __init__(self, name, age):
        self.name = name  # Instance variable
        self.age = age    # Instance variable

    # Instance method
    def introduce(self):
        return f"Hello, my name is {self.name} and I am {self.age} years old."

# Create an instance
person = Person("Alice", 25)

# Call the instance method
print(person.introduce())  # "Hello, my name is Alice and I am 25 years old."
```

In the example above, the introduce method is an instance method because it operates on a specific instance of the Person class.
It has access to self.name and self.age, which are instance variables.

### Class Methods

Class methods are methods that take cls (class) as the first parameter instead of self.
They are defined using the @classmethod decorator and operate on the class itself rather than on instances.
Class methods can modify class variables but cannot modify instance variables because they don’t operate on a specific instance.

```python
class Person:
    species = "Homo sapiens"  # Class variable

    def __init__(self, name, age):
        self.name = name  # Instance variable
        self.age = age    # Instance variable

    @classmethod
    def change_species(cls, new_species):
        cls.species = new_species  # Modify the class variable

# Call the class method
Person.change_species("Homo sapiens sapiens")

print(Person.species)  # "Homo sapiens sapiens"
```

In the example above, the change_species method is a class method because it modifies the class variable species for all instances of the Person class.
This method doesn't require a specific instance to be called; it operates directly on the class.

### Static Methods

Static methods are methods that do not operate on either the class or instances of the class.
They behave just like regular functions, but they are included inside the class for organizational purposes.
Static methods don’t take self or cls as their first parameter.
They are defined using the @staticmethod decorator.

```python
class Person:
    species = "Homo sapiens"  # Class variable

    def __init__(self, name, age):
        self.name = name  # Instance variable
        self.age = age    # Instance variable

    @staticmethod
    def is_adult(age):
        return age >= 18  # Returns True if the age is 18 or older

# Call the static method
print(Person.is_adult(20))  # True
print(Person.is_adult(15))  # False
```

In this example, the is_adult method is a static method because it doesn't rely on any instance-specific data or class-specific data.
It operates solely based on its input parameters.

## Inheritance

Inheritance is a fundamental concept in object-oriented programming (OOP) that allows a class (called a child class or subclass) to inherit attributes and methods from another class (called a parent class or superclass).
This promotes code reuse and helps in creating hierarchical relationships between classes.

Basic Inheritance
When a subclass inherits from a parent class, it can access and use the methods and attributes of the parent class.
The subclass can also override or extend the behavior of the parent class by defining its own methods or modifying existing ones.

Here's a simple example of inheritance:

```python
class Animal:
    def __init__(self, name):
        self.name = name

    def speak(self):
        return f"{self.name} makes a sound."

# Dog inherits from Animal
class Dog(Animal):
    def speak(self):
        return f"{self.name} barks."

# Cat inherits from Animal
class Cat(Animal):
    def speak(self):
        return f"{self.name} meows."

# Create instances of Dog and Cat
animal = Animal("Animal")
dog = Dog("Buddy")
cat = Cat("Whiskers")

print(animal.speak())  # "Animal makes a sound."
print(dog.speak())  # "Buddy barks."
print(cat.speak())  # "Whiskers meows."
```

### super() Function

The super() function in Python is used to call a method from the parent class.
This is especially useful when you want to extend the behavior of a parent class’s method without completely overriding it.

Here's an example of using super() in inheritance:

```python
class Animal:
    def __init__(self, name):
        self.name = name

    def speak(self):
        return f"{self.name} makes a sound."

class Dog(Animal):
    def __init__(self, name, breed):
        super().__init__(name)  # Call the parent class's __init__ method
        self.breed = breed

    def speak(self):
        parent_speak = super().speak()  # Call the parent class's speak method
        return f"{parent_speak} Specifically, {self.name} barks."

# Create an instance of Dog
dog = Dog("Buddy", "Golden Retriever")

print(dog.speak())  # "Buddy makes a sound. Specifically, Buddy barks."
```

### Multiple Inheritance

Python allows multiple inheritance, where a subclass can inherit from more than one parent class.
This can lead to complex hierarchies, and it’s important to be cautious with multiple inheritance to avoid issues like the diamond problem (when two parent classes share a common ancestor).

Here's an example of multiple inheritance:

```python
class Animal:
    def __init__(self, name):
        self.name = name

    def speak(self):
        return f"{self.name} makes a sound."

class Walker:
    def walk(self):
        return "Walking on four legs."

class Swimmer:
    def swim(self):
        return "Swimming in the water."

class Dog(Animal, Walker, Swimmer):
    def speak(self):
        return f"{self.name} barks."

# Create an instance of Dog
dog = Dog("Buddy")

print(dog.speak())  # "Buddy barks."
print(dog.walk())   # "Walking on four legs."
print(dog.swim())   # "Swimming in the water."
```

Multiple Inheritance: The Dog class inherits from both the Walker and Swimmer classes, allowing the dog object to use methods from both classes.
Method Resolution Order (MRO): Python uses the Method Resolution Order (MRO) to determine the order in which parent classes are checked when a method is called. You can view the MRO of a class by using the **mro** attribute or the mro() method:

```python
print(Dog.__mro__)  # (<class '__main__.Dog'>, <class '__main__.Animal'>, <class '__main__.Walker'>, <class '__main__.Swimmer'>, <class 'object'>)
print(Dog.mro())    # [<class '__main__.Dog'>, <class '__main__.Animal'>, <class '__main__.Walker'>, <class '__main__.Swimmer'>, <class 'object'>]
```

### Abstract Base Classes

In Python, abstract base classes (ABCs) are a way to define interfaces or blueprints for other classes.
They allow you to define methods that must be implemented by any subclass, ensuring that the subclasses adhere to a specific structure.
Abstract classes cannot be instantiated directly; they can only be subclassed, and the subclasses must implement the abstract methods defined in the abstract base class.

Python provides the abc module (short for Abstract Base Class) to define abstract base classes and abstract methods.

The key components are:

**Abstract Base Class:** 
A class that contains one or more abstract methods.

**Abstract Methods:** 
Methods that are declared but contain no implementation in the base class. 
Subclasses must provide their own implementation for these methods.

Here's an example of using abstract base classes in Python:

```python
from abc import ABC, abstractmethod

class Animal(ABC):
    @abstractmethod
    def speak(self):
        pass

    @abstractmethod
    def move(self):
        pass

# The following class will raise an error because it does not implement the abstract methods
# animal = Animal()  # TypeError: Can't instantiate abstract class Animal with abstract methods move, speak

class Dog(Animal):
    def speak(self):
        return "Bark"

    def move(self):
        return "Runs on four legs"

class Bird(Animal):
    def speak(self):
        return "Chirp"

    def move(self):
        return "Flies"

# Create instances of the subclasses
dog = Dog()
bird = Bird()

print(dog.speak())  # "Bark"
print(dog.move())   # "Runs on four legs"
print(bird.speak()) # "Chirp"
print(bird.move())  # "Flies"
```

- Abstract Methods: In the Animal class, both speak and move are abstract methods. This means any class that inherits from Animal must provide its own implementations for these methods.
- Cannot Instantiate Abstract Classes: You cannot create an instance of the Animal class directly because it contains abstract methods. If you try to instantiate it, Python will raise a TypeError.
- Subclass Responsibility: Subclasses like Dog and Bird are responsible for providing their own implementations of the abstract methods speak and move.

#### Properties

In Python, the property() function and the @property decorator provide a Pythonic way to use getter and setter methods in a class. 
It allows you to control how attributes are accessed and modified while maintaining the familiar dot notation (object.attribute) for getting and setting values. 
Properties allow us to encapsulate data and ensure that changes to attributes are controlled or validated when necessar

The @property decorator is used to define a method as a "getter" for a property.
This means that you can call the method as if it were an attribute, without using parentheses. 
You can also define corresponding setter and deleter methods, using @property_name.setter and @property_name.deleter.

Here's an example of using properties in Python:

```python
class Circle:
    def __init__(self, radius):
        self._radius = radius  # Using '_' in _radius to signify it's an internal attribute

    # Getter method
    @property
    def radius(self):
        print("Getting radius")
        return self._radius

    # Setter method
    @radius.setter
    def radius(self, value):
        print("Setting radius")
        if value < 0:
            raise ValueError("Radius cannot be negative")
        self._radius = value

    # Deleter method
    @radius.deleter
    def radius(self):
        print("Deleting radius")
        del self._radius

# Using the property
circle = Circle(5)
print(circle.radius)  # Calls the getter method (prints "Getting radius" and returns 5)

circle.radius = 10    # Calls the setter method (prints "Setting radius")
print(circle.radius)  # Getting radius again

# If you try to set a negative radius, it will raise an error:
# circle.radius = -2  # ValueError: Radius cannot be negative

del circle.radius     # Calls the deleter method (prints "Deleting radius")
```

Sometimes, you may want an attribute to be read-only, meaning it can be accessed but not modified after being set. 
You can do this by defining only a getter method and not providing a setter.

```python
class Square:
    def __init__(self, side_length):
        self._side_length = side_length

    @property
    def area(self):
        # Only provide a getter for the area; make it read-only
        return self._side_length ** 2

square = Square(4)
print(square.area)  # 16
# square.area = 25  # AttributeError: can't set attribute
```

In all cases you could still bypass the property and access the attribute directly, but using properties provides a cleaner and more controlled way to manage attribute access:

```python
circle = Circle(5)
circle._radius = 10
print(circle._radius)  # 10 -> but this is not recommended

# Instead, use the property
circle = Circle(5)
circle.radius = 10 # calls the setter method
print(circle.radius)  # 10 -> this is the recommended way as it calls the getter method
```
