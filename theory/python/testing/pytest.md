# Pytest

Pytest is a testing framework for python.
One of the main advantages is the automatic test discovery.
Pytest will automatically find and run all files named `test_*.py` or `*_test.py` in the current directory and subdirectories.

## Documentation

- [Pytest Documentation](https://docs.pytest.org/en/latest/)

## Getting Started

```python
# my_functions.py

def add(number_one, number_two):
    return number_one + number_two

def devide(number_one, number_two):
    return number_one / number_two
```

```python
# test_my_functions.py

import pytest
import my_functions

def test_add():
    assert my_functions.add(1, 2) == 3

def test_devide():
    assert my_functions.devide(4, 2) == 2

def test_devide_by_zero():
    with pytest.raises(ZeroDivisionError):
        my_functions.devide(1, 0)
```

```bash
$ pytest
```

## Class Based Tests

```python
# my_class.py

import math

class Shape:

    def area(self):
        raise NotImplementedError("Subclass must implement abstract method")

    def perimeter(self):
        raise NotImplementedError("Subclass must implement abstract method")

class Circle(Shape):

    def __init__(self, radius):
        self.radius = radius

    def area(self):
        return math.pi * self.radius ** 2

    def perimeter(self):
        return 2 * math.pi * self.radius
```

```python
# test_my_class.py

import pytest
import my_class

class TestCircle:

    def setup_method(self, method):
        # To see the print statements run pytest with the -s flag
        print("This is executed before each test method")
        print(f"Setting up {method}")
        self.circle = my_class.Circle(10)

    def teardown_method(self, method):
        print("This is executed after each test method")
        print(f"Tearing down {method}")

    def test_area(self):
        assert self.circle.area() == pytest.approx(314.159, 0.001)

    def test_perimeter(self):
        assert self.circle.perimeter() == pytest.approx(62.831, 0.001)
```

```bash
$ pytest -s
```

## Fixtures

Fixtures are functions that run before each test function.
They can be used to setup data, create objects, etc.

```python
# my_class.py

import math

class Shape:

    def area(self):
        raise NotImplementedError("Subclass must implement abstract method")

    def perimeter(self):
        raise NotImplementedError("Subclass must implement abstract method")


class Rectangle(Shape):

        def __init__(self, width, height):
            self.width = width
            self.height = height

        def area(self):
            return self.width * self.height

        def perimeter(self):
            return 2 * (self.width + self.height)
```

```python
# test_my_class.py

import pytest
import my_class

@pytest.fixture
def rectangle_fixture():
    return my_class.Rectangle(10, 20)

def test_area(rectangle_fixture):
    assert rectangle_fixture.area() == 200

def test_perimeter(rectangle_fixture):
    assert rectangle_fixture.perimeter() == 60
```

### Conftest.py

Fixtures can be defined in a `conftest.py` file, which allows them to be shared across multiple test files.

```python
# conftest.py

import pytest
import my_class

@pytest.fixture
def rectangle_fixture():
    return my_class.Rectangle(10, 20)
```

```python
# test_my_class.py

def test_area(rectangle_fixture):
    assert rectangle_fixture.area() == 200

def test_perimeter(rectangle_fixture):
    assert rectangle_fixture.perimeter() == 60
```

```bash
$ pytest
```

## Parametrized Tests

Parametrized tests allow you to run the same test with different inputs.

```python
# my_functions.py

def add(number_one, number_two):
    return number_one + number_two
```

```python
# test_my_functions.py

import pytest

@pytest.mark.parametrize("number_one, number_two, expected", [(1, 2, 3), (2, 3, 5), (3, 4, 7)])
def test_add(number_one, number_two, expected):
    assert my_functions.add(number_one, number_two) == expected
```

```bash
$ pytest
```

## Markers

Markers are used to mark specific tests.

```python
# test_my_functions.py

import pytest
import my_functions

@pytest.mark.skip(reason="Not implemented yet")
def test_subtract():
    assert my_functions.subtract(2, 1) == 1

@pytest.mark.slow
def test_multiply():
    assert my_functions.multiply(2, 3) == 6

@pytest.mark.xfail(reason="Not implemented yet")
def test_divide():
    assert my_functions.divide(4, 2) == 2
```

````

```bash
$ pytest -m slow
````

## Mocking

Mocking is a way to replace a function with a fake function.
This is useful when you want to test a function that depends on another function that is not yet implemented or when you want to test a function that makes an external API call without performing the actual API call.

```python
# my_functions.py

import llm

def api_call(prompt):
    return llm.api_call(prompt=prompt)
```

```python
# test_my_functions.py

import pytest
import unittest.mock as mock
# here we are using the unittest.mock module to mock the llm.api_call function

@mock.patch("my_functions.llm.api_call") # path to the function to be mocked
def test_api_call(mock_api_call):
    mock_api_call.return_value = "Mocked Response"
    assert my_functions.api_call("Hello") == "Mocked Response"
```

You can also mock a `requests.get` call:

```python
# my_functions.py

import requests

def get_api_data():
    response = requests.get("https://api.example.com/data")

    if response.status_code != 200:
        raise Exception("API call failed")

    return response.json()
```

```python
# test_requests.py

import pytest
import unittest.mock as mock

@mock.patch("requests.get")
def test_requests(mock_get):
    mock_response = mock.Mock()
    mock_response.status_code = 200
    mock_response.json.return_value = {"key": "value"}
    mock_get.return_value = mock_response
    data = my_functions.get_api_data()
    assert data == {"key": "value"}

    mock_response.status_code = 404
    with pytest.raises(Exception):
        my_functions.get_api_data()
```

**Important Note:**
You will always have to use the path to the function as it is imported in the file you are testing.

```
project/
    clients/
        my_client.py
    functions/
        my_functions.py
    tests/
        test_my_functions.py
```

Let's say the `my_functions.py` file imports the `my_client.py` file:

```python
# my_functions.py

import clients.my_client

def get_data():
    return clients.my_client.get_data()
```

In the `test_my_functions.py` file, you will have to mock the `clients.my_client.get_data` function as follows:

```python
@mock.patch("functions.my_client.get_data")
def test_get_data(mock_get_data):
    mock_get_data.return_value = "Mocked Data"
    assert my_functions.get_data() == "Mocked Data"
```

So instead of using the path to `my_client.get_data`, you will have to use the path to `functions.my_client.get_data`.
