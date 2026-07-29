# Practical 4 Cheat Sheet: Python Lists & Control Flow

This reference guide covers the core Python list operations, indexing rules, looping mechanisms, and control flow keywords used in Practical 4. Use this document to revise key concepts and syntax.

---

## 1. Python Lists: Basics

A **list** is an ordered, mutable (changeable) collection of items enclosed in square brackets `[]`. Lists can contain duplicate values and mixed data types (strings, integers, floats, booleans).

```python
# Creating lists
fruits = ["apple", "banana", "cherry"]  # String list
numbers = [10, 20, 30]                  # Integer list
empty_list = []                         # Empty list

# Checking type and length
print(type(fruits))  # Output: <class 'list'>
print(len(fruits))   # Output: 3 (Returns total element count)
```

## 2. Indexing and Slicing

### Indexing
Elements in a list are assigned a zero-based position (index).
* Positive Indexing: Starts at 0 for the first element and moves left-to-right.
* Negative Indexing: Starts at -1 for the last element and moves right-to-left.

```python
days = ["Mon", "Tue", "Wed", "Thu", "Fri", "Sat", "Sun"]

print(days[0])   # "Mon" (First item)
print(days[-1])  # "Sun" (Last item)
```

| List Item | "Mon" | "Tue" | "Wed" | "Thu" | "Fri" | "Sat" | "Sun" |
| :--- | :---: | :---: | :---: | :---: | :---: | :---: | :---: |
| **Positive Index** | 0 | 1 | 2 | 3 | 4 | 5 | 6 |
| **Negative Index** | -7 | -6 | -5 | -4 | -3 | -2 | -1 |

### Slicing
Slicing extracts a sub-list using the syntax: `list[start : stop : step]`.
* Rule: start index is included, but stop index is excluded.

```python
# Extract weekdays (index 0 through 4)
weekdays = days[0:5]  # Returns ["Mon", "Tue", "Wed", "Thu", "Fri"]
```

## 3. Important List Methods

| Method | Syntax | Description |
|---|---|---|
| `.append()` | `lst.append(item)` | Adds item to the very end of the list. |
| `.insert()` | `lst.insert(index, item)` | Inserts item at a specific index, shifting existing items right. |
| `.remove()` | `lst.remove(value)` | Deletes the first occurrence of value. Throws ValueError if not found. |
| `.pop()` | `lst.pop(index)` | Removes & returns item at index (defaults to the last item if left empty). |

```python
items = ["pen", "paper"]

# Adding items
items.append("eraser")         # Adds to end
items.insert(1, "ruler")       # Inserts at index 1

# Removing items
items.remove("ruler")          # Removes "ruler"
last_item = items.pop()        # Removes & returns last item
item_at_0 = items.pop(0)       # Removes & returns item at index 0
```

## 4. Membership Testing (`in` Keyword)
The in keyword checks if an item exists inside a list and returns a Boolean (True or False).

```python
checked_in = ["Alice", "Bob", "Charlie"]

if "Alice" in checked_in:
    print("Already inside!")
```

## 5. Control Flow & Loops

### `for` Loop
Used when you want to iterate over a collection item-by-item.

```python
scores = [45, 78, 89]
for score in scores:
    print(score)
```

### `while` Loop
Repeats as long as a specified condition evaluates to `True`

```python
actions = ["Type", "Bold", "Underline"]
while len(actions) > 0:
    print("Undoing:", actions.pop())  # Empties the list item-by-item
```

## 6. Loop Control Keywords

* `break`: Terminates the loop immediately and jumps out.
* `continue`: Skips the rest of the current iteration and jumps to the next item.
* `pass`: A null statement that acts as a syntactical placeholder (does nothing).

```python
# 'continue' example: Print even numbers only
numbers = [1, 2, 3, 4, 5]
for n in numbers:
    if n % 2 != 0:
        continue  # Skip odd numbers
    print(n)

# 'break' example: Emergency stop
temps = [22, 28, 32, 25]
for t in temps:
    if t >= 30:
        print("Overheat warning!")
        break  # Stop checking further
```

## 7. Useful Problem-Solving Patterns

### A. The Accumulator Pattern (Running Totals)
Used to sum or aggregate values manually without built-in functions.

```python
prices = [100, 250, 80]
total = 0
for price in prices:
    total += price  # Equivalent to total = total + price
print("Total is:", total)
```

### B. Flag Variables
A Boolean variable used to track whether a specific event occurred inside a loop.

```python
warning_triggered = False
# ... loop checks condition ...
if warning_triggered:
    print("Action required")
else:
    print("All systems normal")
```

### C. Filtering into Brackets (Categorization)
Iterating through a master list and appending items into separate sub-lists based on criteria

```python
all_marks = [85, 42, 90, 38]
distinction_pool = []
retest_pool = []

for mark in all_marks:
    if mark >= 75:
        distinction_pool.append(mark)
    elif mark < 50:
        retest_pool.append(mark)
    else:
        pass
```