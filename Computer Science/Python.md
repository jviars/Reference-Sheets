# Comprehensive Python Cheat Sheet

## Basic Syntax and Data Types

### Variables and Data Types
```python
# Numeric Types
x = 5                   # int
y = 3.14                # float
z = 1 + 2j             # complex

# Strings
name = "Python"         # Can use single or double quotes
multi_line = """
Multiple
line string
"""

# Boolean
is_true = True
is_false = False

# None type
empty = None

# Type conversion
str_num = "123"
num = int(str_num)      # String to int
float_num = float(num)  # Int to float
str_val = str(num)      # Number to string
```

### Data Structures

#### Lists
```python
# Creation and access
my_list = [1, 2, 3, 4, 5]
first = my_list[0]          # First element
last = my_list[-1]          # Last element
sub_list = my_list[1:3]     # Slicing

# Common operations
my_list.append(6)           # Add element
my_list.extend([7, 8])      # Add multiple elements
my_list.insert(0, 0)        # Insert at position
my_list.remove(3)           # Remove first occurrence
popped = my_list.pop()      # Remove and return last element
my_list.sort()              # Sort in place
sorted_list = sorted(my_list)  # Return new sorted list
my_list.reverse()           # Reverse in place

# List comprehension
squares = [x**2 for x in range(10)]
evens = [x for x in range(10) if x % 2 == 0]
```

#### Tuples
```python
# Immutable sequences
point = (3, 4)
x, y = point              # Tuple unpacking

# Single element tuple
single = (1,)            # Note the comma

# Multiple assignment
a, b, c = 1, 2, 3
```

#### Dictionaries
```python
# Creation and access
person = {
    'name': 'John',
    'age': 30,
    'city': 'New York'
}

# Dictionary operations
person['email'] = 'john@example.com'  # Add/update
del person['age']                     # Delete key
age = person.get('age', 25)           # Get with default
keys = person.keys()                  # Get keys
values = person.values()              # Get values
items = person.items()                # Get key-value pairs

# Dictionary comprehension
square_dict = {x: x**2 for x in range(5)}

# Merging dictionaries
dict1 = {'a': 1, 'b': 2}
dict2 = {'c': 3, 'd': 4}
merged = {**dict1, **dict2}  # Python 3.5+
```

#### Sets
```python
# Creation
my_set = {1, 2, 3, 3}    # Duplicates removed automatically
empty_set = set()        # Creating empty set

# Set operations
my_set.add(4)           # Add element
my_set.remove(1)        # Remove element (raises error if not found)
my_set.discard(1)       # Remove element (no error if not found)

# Set operations
set1 = {1, 2, 3}
set2 = {3, 4, 5}
union = set1 | set2                # Union
intersection = set1 & set2         # Intersection
difference = set1 - set2           # Difference
symmetric_diff = set1 ^ set2       # Symmetric difference
```

## Control Flow

### Conditional Statements
```python
# if-elif-else
if condition:
    # code block
elif another_condition:
    # code block
else:
    # code block

# Ternary operator
value = x if condition else y

# Match statement (Python 3.10+)
match value:
    case 1:
        # code
    case 2:
        # code
    case _:
        # default case
```

### Loops
```python
# For loops
for i in range(5):
    # code block

for item in iterable:
    # code block

# While loops
while condition:
    # code block

# Loop control
for i in range(5):
    if i == 2:
        continue    # Skip rest of iteration
    if i == 4:
        break       # Exit loop
else:
    # Executed when loop completes normally
```

## Functions and Modules

### Function Definition
```python
# Basic function
def greet(name):
    return f"Hello, {name}!"

# Default parameters
def greet(name="World"):
    return f"Hello, {name}!"

# Multiple parameters
def function(pos1, pos2, /, pos_or_kwd, *, kwd1, kwd2):
    # pos1, pos2 are positional-only
    # pos_or_kwd can be positional or keyword
    # kwd1, kwd2 are keyword-only
    pass

# Variable arguments
def func(*args, **kwargs):
    # args is tuple of positional arguments
    # kwargs is dictionary of keyword arguments
    pass

# Type hints (Python 3.5+)
def add(x: int, y: int) -> int:
    return x + y
```

### Lambda Functions
```python
# Anonymous functions
square = lambda x: x**2
add = lambda x, y: x + y

# With built-in functions
numbers = [1, 2, 3, 4, 5]
squares = list(map(lambda x: x**2, numbers))
evens = list(filter(lambda x: x % 2 == 0, numbers))
```

### Modules and Packages
```python
# Importing
import module
from module import function
from module import *
from module import function as alias

# Creating modules
# file: mymodule.py
def my_function():
    pass

class MyClass:
    pass

# Using modules
import mymodule
mymodule.my_function()
```

## Classes and Objects

### Class Definition
```python
class Person:
    # Class variable
    species = "Homo sapiens"
    
    # Constructor
    def __init__(self, name, age):
        self.name = name    # Instance variable
        self.age = age
    
    # Instance method
    def greet(self):
        return f"Hello, I'm {self.name}"
    
    # Class method
    @classmethod
    def from_birth_year(cls, name, year):
        return cls(name, 2024 - year)
    
    # Static method
    @staticmethod
    def is_adult(age):
        return age >= 18
    
    # Property decorator
    @property
    def age_group(self):
        if self.age < 18:
            return "minor"
        return "adult"
```

### Inheritance and Polymorphism
```python
class Employee(Person):
    def __init__(self, name, age, employee_id):
        super().__init__(name, age)
        self.employee_id = employee_id
    
    # Method overriding
    def greet(self):
        return f"Hello, I'm {self.name}, ID: {self.employee_id}"

# Multiple inheritance
class A:
    pass

class B:
    pass

class C(A, B):
    pass
```

## File Operations

### File Handling
```python
# Reading files
with open('file.txt', 'r') as f:
    content = f.read()           # Read entire file
    lines = f.readlines()        # Read lines into list
    
    # Read line by line
    for line in f:
        print(line.strip())

# Writing files
with open('file.txt', 'w') as f:
    f.write('Hello\n')          # Write string
    f.writelines(['line1\n', 'line2\n'])  # Write multiple lines

# Appending to files
with open('file.txt', 'a') as f:
    f.write('New line\n')
```

### Working with JSON
```python
import json

# Reading JSON
with open('data.json', 'r') as f:
    data = json.load(f)

# Writing JSON
with open('data.json', 'w') as f:
    json.dump(data, f, indent=4)

# Converting to/from strings
json_str = json.dumps(data)
data = json.loads(json_str)
```

## Exception Handling

### Try-Except Blocks
```python
try:
    # Code that might raise an exception
    result = 10 / 0
except ZeroDivisionError as e:
    # Handle specific exception
    print(f"Error: {e}")
except Exception as e:
    # Handle any other exception
    print(f"Unexpected error: {e}")
else:
    # Executed if no exception occurs
    print("Success")
finally:
    # Always executed
    print("Cleanup")

# Custom exceptions
class CustomError(Exception):
    pass

# Context managers
class MyContext:
    def __enter__(self):
        print("Entering")
        return self
    
    def __exit__(self, exc_type, exc_value, traceback):
        print("Exiting")

with MyContext():
    # code block
```

## Advanced Python Features

### Generators
```python
# Generator function
def countdown(n):
    while n > 0:
        yield n
        n -= 1

# Generator expression
squares = (x**2 for x in range(10))

# Using generators
for num in countdown(5):
    print(num)
```

### Decorators
```python
# Function decorator
def timer(func):
    def wrapper(*args, **kwargs):
        import time
        start = time.time()
        result = func(*args, **kwargs)
        print(f"Time taken: {time.time() - start}")
        return result
    return wrapper

@timer
def my_function():
    pass

# Class decorator
def singleton(cls):
    instances = {}
    def get_instance(*args, **kwargs):
        if cls not in instances:
            instances[cls] = cls(*args, **kwargs)
        return instances[cls]
    return get_instance

@singleton
class MyClass:
    pass
```

### Context Managers
```python
from contextlib import contextmanager

@contextmanager
def temporary_change():
    # Setup
    try:
        yield
    finally:
        # Cleanup
        pass
```

## Standard Library Highlights

### Collections Module
```python
from collections import (
    defaultdict,
    Counter,
    OrderedDict,
    namedtuple,
    deque
)

# defaultdict
d = defaultdict(list)
d['key'].append(1)  # No KeyError if key doesn't exist

# Counter
c = Counter(['a', 'b', 'b', 'c'])

# OrderedDict
od = OrderedDict()

# namedtuple
Point = namedtuple('Point', ['x', 'y'])
p = Point(11, y=22)

# deque (double-ended queue)
d = deque([1, 2, 3])
```

### Itertools Module
```python
from itertools import (
    count,
    cycle,
    repeat,
    chain,
    combinations,
    permutations,
    product
)

# Infinite iterators
for i in count(10):      # Numbers from 10
    if i > 15: break

# Combinations and permutations
list(combinations('ABC', 2))    # ('A', 'B'), ('A', 'C'), ('B', 'C')
list(permutations('ABC', 2))    # All possible arrangements
```

### Regular Expressions
```python
import re

# Pattern matching
pattern = r'\d+'
text = "123 abc 456"
matches = re.findall(pattern, text)
match = re.search(pattern, text)
if match:
    print(match.group())

# String replacement
new_text = re.sub(pattern, 'X', text)
```

## Testing

### Unit Testing
```python
import unittest

class TestMathFunctions(unittest.TestCase):
    def setUp(self):
        # Setup code
        pass
    
    def test_addition(self):
        self.assertEqual(1 + 1, 2)
    
    def test_zero_division(self):
        with self.assertRaises(ZeroDivisionError):
            1 / 0
    
    def tearDown(self):
        # Cleanup code
        pass

if __name__ == '__main__':
    unittest.main()
```

### Assertions
```python
def divide(a, b):
    assert b != 0, "Division by zero!"
    return a / b
```

## Virtual Environments

### Creating and Managing
```bash
# Create virtual environment
python -m venv myenv

# Activate
# Windows
myenv\Scripts\activate
# Unix/MacOS
source myenv/bin/activate

# Install packages
pip install package_name

# Save requirements
pip freeze > requirements.txt

# Install from requirements
pip install -r requirements.txt
```
