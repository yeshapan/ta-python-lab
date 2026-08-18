# Lab Guide 07: Modular Programming, Tuple Operations and Dictionary Architectures

Reference guide for the core concepts covered in Practical Assignment 7. This document details custom user-defined functions, key-based sorting mechanics, tuple immutability and slicing, dictionary manipulations, and real-world compound data structure patterns.

## 1. User-Defined Functions (`def`) and Modular Design
A function is a reusable block of code executed only when called. Functions promote code modularity, eliminate redundancy, and accept parameters to return processed results.

### 1.1 Function Syntax and Parameters
Functions are defined using the `def` keyword followed by the function name, input parameters in parentheses, and a colon `:`. The `return` statement exits the function and sends values back to the caller.

```python
# 1. Standard Single-Argument Function
def square(n):
    return n ** 2  # Returns calculated value

result = square(7)  # Output: 49

# 2. Multi-Argument Function
def add_three(a, b, c):
    return a + b + c  # Computes numerical sum

total = add_three(5, 10, 15)  # Output: 30
```

### 1.2 Predicate and Conditional Logic Functions
Functions can return Boolean flags (`True`/`False`) or perform conditional checks to evaluate input states.

```python
# Boolean Predicate Function
def is_even(number):
    return number % 2 == 0  # Evaluates parity

# Manual Max Value Comparator
def find_max(a, b):
    if a > b:
        return a  # Evaluates larger value
    else:
        return b

# Conditional Categorization
def check_length(text):
    if len(text) < 5:
        return "Short"  # Evaluates string length boundary
    return "Long"
```

### 1.3 Key Functions for Higher-Order Sorting (`sorted()` and `.sort()`)
Python's `sorted()` function and `.sort()` method accept a `key` parameter. A custom single-argument helper function can be passed to `key` to dictate extraction logic during sorting.

```python
# Sorting Tuples by Second Element
points = ((1, 2), (4, 1), (3, 8), (2, 5))

def get_second(item):
    return item[1]  # Extracts second element for sorting key

sorted_points = sorted(points, key=get_second) 
# Output: ((4, 1), (1, 2), (2, 5), (3, 8))

# Sorting Strings by Length
words = ["python", "java", "c", "javascript", "go"]

def get_length(word):
    return len(word)  # Extracts word length

sorted_words = sorted(words, key=get_length)
# Output: ['c', 'go', 'java', 'python', 'javascript']

# Descending Dictionary Sort using Custom Key
scores = {"Alice": 88, "Bob": 95, "Charlie": 78}

def get_score(student_name):
    return scores[student_name]  # Looks up value for key extraction

sorted_students = sorted(scores, key=get_score, reverse=True)
# Output: ['Bob', 'Alice', 'Charlie']
```

## 2. Advanced Tuple Operations & Mechanics
A tuple is an immutable, ordered sequence. Once instantiated, elements cannot be modified, assigned, or deleted. 

### 2.1 Immutability Guarding (`try-except`)
Attempting to modify an element of a tuple raises a `TypeError` runtime exception. This behavior can be handled gracefully using `try-except` blocks. 

```python
tuple_data = (10, 20, 30)

try:
    tuple_data[1] = 99  # Attempting element reassignment
except TypeError:
    print("Error: Tuples are immutable.")  # Exception caught gracefully
```

### 2.2 Tuple Slicing and Reversal
Tuples support sub-sequence extraction using slice notation [start:stop:step]. Using a step of -1 generates a reversed sub-tuple.

```python
data = (10, 20, 30, 40, 50)

# Extract sub-tuple (20, 30, 40)
sub_tuple = data[1:4]  # Extracts indices 1, 2, and 3

# Reverse sub-tuple
reversed_sub = sub_tuple[::-1]  # Output: (40, 30, 20)
```

## 3. Dictionary State Management & Manipulation
A dictionary stores key-value pairs where keys must be unique and immutable. 

### 3.1 Key Existence Check & Default Initialization
Accessing a missing key causes a `KeyError`. Safe existence validation is performed using the `in` operator prior to dynamic assignment.

```python
item = {"name": "Monitor", "price": 12000}

# Guarding key addition
if "discount" not in item:
    item["discount"] = 0  # Adds key dynamically if missing
```

### 3.2 Iteration Mechanics
Dictionaries can be iterated by direct key traversal, value traversal, or key-value tuple unpacking.

```python
inventory = {"apple": 50, "orange": 30, "grape": 20}

# Direct Key Iteration
for key in inventory:
    print(f"We have {inventory[key]} units of {key}")  # Look up value via key

# Value Iteration
for count in inventory.values():
    print(f"Stock count: {count}")

# Key-Value Tuple Unpacking (Most Pythonic)
for fruit, count in inventory.items():
    print(f"{fruit} quantity: {count}")  # Simultaneous unpacking
```

### 3.3 Merging and Cleansing Strategies
* `.update()`: Merges key-value pairs from a secondary dictionary into the target dictionary, overwriting existing keys.
* `.popitem()`: Sequentially removes and returns the last inserted (key, value) tuple.
* `.copy()` vs `del`: `.copy()` creates an independent shallow copy, protecting data from deletion commands (`del`) executed on the source dictionary.

```python
# 1. In-Place Dictionary Merge via .update()
dict1 = {"x": 10, "y": 20}
dict2 = {"y": 25, "z": 30}
dict1.update(dict2)  # dict1 becomes {'x': 10, 'y': 25, 'z': 30}

# 2. Sequential Purging with .popitem()
session = {"user": "guest", "id": 404, "active": False}
while len(session) > 0:
    popped_key, popped_val = session.popitem()  # Removes items step-by-step
    print(f"Popped: {popped_key} -> {popped_val}")

# 3. Independent Duplication vs Key Deletion
employees = {"ID1": "Ana", "ID2": "Ben"}
emp_copy = employees.copy()  # Creates shallow copy
del employees["ID1"]         # Removes key from original
# emp_copy maintains 'ID1' untouched
```

## 4. Architectural Problem-Solving Patterns
### Pattern A: Custom Filtering and Transformation Loops
Iterate over sequences to filter elements or perform unit conversions

```python
# 1. Odds Extractor Filter
def extract_odds(numbers_list):
    odds = []
    for num in numbers_list:
        if num % 2 != 0:
            odds.append(num)  # Appends odd numbers
    return odds

# 2. Formula Transformation ($F = C \times 1.8 + 32$)
celsius = [0, 20, 37, 100]
fahrenheit = []
for c in celsius:
    f = (c * 1.8) + 32  # Applies conversion formula
    fahrenheit.append(f)
```

### Pattern B: Word Frequency Counter
Count item occurrences in a collection using a dictionary lookup loop

```python
paragraph = "She was fire, and light, and ash, and embers. She was Aelin Fireheart, and she bowed for no one and nothing, save the crown that was hers by blood and survival and triumph"
words = paragraph.split()
counts = {}

for word in words:
    if word in counts:
        counts[word] += 1  # Increment count
    else:
        counts[word] = 1   # Initialize count
```

### Pattern C: Sentinel-Controlled Data Aggregation
Continuously collect inputs using a while loop until a sentinel termination value (e.g., -1) is entered

```python
inputs = []
while True:
    val = int(input("Enter number (-1 to stop): "))
    if val == -1:
        break  # Exit condition[cite: 9]
    inputs.append(val)[cite: 9]

# Manual Maximum Finder without built-in max()
def find_highest(lst):
    if not lst:
        return None
    highest = lst[0]
    for num in lst:
        if num > highest:
            highest = num  # Tracks largest element[cite: 9]
    return highest
```

### Pattern D: Dictionaries with Tuple Keys (Coordinate Lookups)
Since tuples are immutable, they can serve as hashable keys for grid or coordinate systems

```python
# Seat Allocation Map (Row, Seat_Letter)
flight_seats = {(1, "A"): "Occupied", (1, "B"): "Vacant", (2, "A"): "Occupied"}
requested_seat = (1, "B")

if requested_seat in flight_seats:
    if flight_seats[requested_seat] == "Vacant":
        flight_seats[requested_seat] = "Occupied"  # Book seat
        print("Booking confirmed!")
    else:
        # Scan for alternative vacant seats
        vacant_seats = [seat for seat, status in flight_seats.items() if status == "Vacant"]
```

### Pattern E: Dict-Tuple Record Unpacking and Mutation
When values stored inside a dictionary are tuples, unpack them into local variables during loop iteration to update records

```python
payroll = {"E101": (50000, "Tech"), "E102": (75000, "Exec")}

def calculate_tax(salary):
    return salary * 0.10 if salary <= 50000 else salary * 0.20

for emp_id in payroll:
    salary, dept = payroll[emp_id]  # Unpacks original tuple
    net_salary = salary - calculate_tax(salary) # Calculates net salary
    payroll[emp_id] = (salary, net_salary, dept)  # Stores updated record tuple
```

### Pattern F: List of Dictionaries Complex Operations
Manage collections of structured entities (e.g., e-commerce products or student records)

```python
products = [
    {"name": "Laptop", "price": 85000},
    {"name": "Mouse", "price": 800},
    {"name": "Keyboard", "price": 2500}
]

# Helper Key Functions
def sort_by_price(item):
    return item["price"]

def sort_by_name(item):
    return item["name"]

# Interactive Sorting Pass
choice = "price"
if choice == "price":
    sorted_prods = sorted(products, key=sort_by_price)
else:
    sorted_prods = sorted(products, key=sort_by_name)
```

### Pattern G: Multi-Branch Warehouse Inventory Aggregation
Merge two inventory sets while accumulating overlapping stock quantities

```python
warehouse_A = {"Items_A": 150, "Items_B": 80}
warehouse_B = {"Items_B": 50, "Items_C": 60}

master_stock = warehouse_A.copy()  # Duplicate base stock

for item, stock in warehouse_B.items():
    if item in master_stock:
        master_stock[item] += stock  # Accumulate overlapping stock
    else:
        master_stock[item] = stock   # Insert new item entry

def get_stock(item_key):
    return master_stock[item_key]

# Sort inventory high to low
sorted_inventory = sorted(master_stock, key=get_stock, reverse=True)
```

5. Structural Comparison Matrix

| Concept / Technique | Primary Syntax / Primitive | Mutability / Behavior | Primary Practical Use Case |
| :--- | :--- | :--- | :--- |
| **Custom Function** | `def name(args):` | Executable block | Modular logic, custom sorting keys, calculations |
| **Tuple Slicing** | `tup[start:stop:step]` | Non-mutating (creates new tuple) | Sequence extraction and sub-tuple reversal (`[::-1]`) |
| **Tuple Key Map** | `{(x, y): value}` | Immutable Keys, Mutable Dict | Grid systems, seat maps, multi-part coordinates |
| **Dict Merging** | `d1.update(d2)` | In-place mutation | Combining records, bulk key updating |
| **Dict Purging** | `d.popitem()` | In-place removal | Sequential FIFO/LIFO stack/queue item removal |
| **Shallow Copying** | `d.copy()` | Non-mutating creation | Isolating data prior to destructive modifications (`del`) |

