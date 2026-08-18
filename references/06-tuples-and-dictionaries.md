# Lab Guide 06: Tuples and Dictionaries in Python
Reference guide for the concepts covered in Practical Assignment 6. This document details the memory semantics, syntax, built-in methods, iteration mechanics, and practical architectural patterns for Python's non-scalar data structures: Tuples (`tuple`) and Dictionaries (`dict`).

## 1. Python Tuples (`tuple`)
A tuple is an ordered, immutable sequence of elements enclosed in parentheses (). Because tuples are immutable, their structure and memory footprint are fixed after instantiation. Tuples are heterogenous data structures , i.e., they can store elements of different data types.

### 1.1 Creation and Indexing
Tuples support zero-based positive indexing and negative indexing.

```python
# Multi-element tuple initialization
coordinates = (10.5, 20.0, 15.2)  # homogenous tuple
person = ("Azriel", 500 , "Shadowsinger",  True)   # heterogenous tuple

# Indexing
second_item = person[1]   # 500 (Positive Indexing)
last_item = person[-1]    # True (Negative Indexing)

# Structural Inspection
print(len(coordinates))       # Returns element count (3)
print(type(coordinates))      # Returns <class 'tuple'>
```

### 1.2 Single-Element Tuple Trait
Parentheses `()` are also used for arithmetic grouping. To instantiate a single-element tuple, you must include a trailing comma `,`. Without the comma, Python treats the expression as a standard parenthesized string or number.

```python
# INCORRECT: Evaluates to str
not_a_tuple = ("Python")
print(type(not_a_tuple))  # Output: <class 'str'>

# CORRECT: Trailing comma enforces tuple instantiation
single_tuple = ("Python",)
print(type(single_tuple)) # Output: <class 'tuple'>
```

### 1.3 Tuple Immutability and Exception Handling
Attempting to modify, reassign, or delete individual elements of a tuple raises a runtime `TypeError`. You can catch this behavior using a `try-except` block.

```python
colors = ("red", "green", "blue")

try:
    colors[0] = "yellow"  # Reassignment attempt
except TypeError:
    print("Tuples are immutable!")  # Catches mutation attempt
```

### 1.4 Sequence Unpacking
Tuple unpacking allows you to assign each item of a tuple directly to individual variables in a single statement. The number of target variables on the left must exactly match the number of tuple items.

```python
point = (5, 12)[cite: 7]

# Structural unpacking
x, y = point  # x = 5, y = 12

# Unpacking inside loop iterations (e.g., GPS Coordinates)
route = [(18.52, 73.85), (19.07, 72.87)]
for lat, lon in route:
    print(f"Latitude: {lat}, Longitude: {lon}")
```

### 1.5 Tuple Built-in Methods
Tuples have only two built-in methods due to their immutability:

| Method | Syntax | Description | Example (`ranks = (1, 2, 3, 2, 4)`) |
| :--- | :--- | :--- | :--- |
| `.count()` | `tuple.count(val)` | Returns total occurrences of `val`. | `ranks.count(2)` $\rightarrow$ `2` |
| `.index()` | `tuple.index(val)` | Returns zero-based index of the first occurrence of `val`. | `ranks.index(4)` $\rightarrow$ `4` |

### 1.6 Indirect Tuple Mutation (Type Conversion Workaround)
To modify an existing tuple, convert it to a mutable list, perform the modifications, and cast it back to a tuple

```python
tuple_data = (10, 20, 30)
list_version = list(tuple_data)
list_version.append(40)             # Mutable operation
tuple_data = tuple(list_version)    # Convert back to tuple
```

## 2. Python Dictionaries (`dict`)
Dictionaries are unordered, mutable collections of key-value pairs where each key must be unique and immutable. 

### 2.1 Dictionary Properties
* **Keys** must be hashable types (immutable: strings, integers, floats, tuples).
* **Values** can be of any data type (including lists or other dictionaries).
* **Unordered** (insertion order preserved from Python 3.7+).
* **Mutable**: Keys/values can be added, updated, or deleted.

### 2.2 Dictionary Creation
Dictionaries are instantiated using curly braces `{}` or the `dict()` constructor.

```python
# Using curly braces
student = {"name": "Alice", "age": 25, "major": "Computer Science"}

# Using dict() constructor with keyword arguments
config = dict(theme="dark", language="EN", timeout=30)

# Empty dictionary
empty_dict = {}

# Dictionary with mixed value types
mixed_data = {"id": 101, "grades": [85, 90, 88], "is_active": True}
```

### 2.3 Accessing Values by Key
Values are retrieved using square bracket notation `[]` with the corresponding key.

```python
student = {"name": "Bob", "id": 202, "dept": "Physics"}

# Accessing existing key
print(student["name"])   # Output: "Bob"

# Attempting to access non-existent key raises KeyError
# print(student["email"])  # This would cause a program crash
```

### 2.4 Safe Access with `.get()`
The `.get()` method safely retrieves values without raising `KeyError` if the key is missing. It returns `None` or a specified default value instead.

```python
user = {"username": "charlie"}

# Key exists - returns value
print(user.get("username"))  # Output: "charlie"

# Key missing - returns None (default behavior)
print(user.get("email"))     # Output: None

# Key missing with specified default value
print(user.get("email", "not_provided"))  # Output: "not_provided"
```

### 2.5 Dictionary Methods
| Method | Syntax | Description |
| :--- | :--- | :--- |
| `.keys()` | `dict.keys()` | Returns a view object displaying all keys. |
| `.values()` | `dict.values()` | Returns a view object displaying all values. |
| `.items()` | `dict.items()` | Returns a view object of (key, value) tuples. |
| `.pop(key, default)` | `dict.pop(key)` | Removes specified key and returns its value. Returns default if key not found. |
| `.popitem()` | `dict.popitem()` | Removes and returns the last inserted (key, value) pair. |
| `.update(other_dict)` | `dict.update(other)` | Adds/updates dictionary items from another dictionary. |
| `.clear()` | `dict.clear()` | Removes all items from the dictionary. |

```python
options = {"theme": "dark", "fontSize": 14}

# Get all keys
print(options.keys())  # dict_keys(['theme', 'fontSize'])

# Get all values
print(options.values())  # dict_values(['dark', 14])

# Get key-value pairs
print(options.items())  # dict_items([('theme', 'dark'), ('fontSize', 14)])
```