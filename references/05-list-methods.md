# Lab Guide 05: List Slicing, Built-in Functions, and List Methods in Python

Reference cheatsheet for concepts in Practical Assignment 5.
This guide covers list slicing syntax, built-in functions, list methods, memory aliasing v/s copying, and common practical problem-solving patterns.

---

## 1. Advanced List Slicing Syntax

List slicing allows you to extract sub-lists dynamically without modifying the original collection.

$$\text{list}[ \text{start} : \text{stop} : \text{step} ]$$

* **`start`**: Index where the slice begins (inclusive). Defaults to `0`.
* **`stop`**: Index where the slice ends (**exclusive**). Defaults to `len(list)`.
* **`step`**: Index increment value. Defaults to `1`.

```python
data = [10, 20, 30, 40, 50, 60, 70, 80]

# Basic slice [start:stop]
sub = data[2:5]         # [30, 40, 50] (indices 2, 3, 4)

# Strided slice [::step]
even_step = data[::2]   # [10, 30, 50, 70] (every 2nd item)

# Negative index slicing (Tail extraction)
tail_4 = data[-4:]      # [50, 60, 70, 80] (last 4 items)

# Reverse list slice
reversed_data = data[::-1] # Returns a complete reversed copy
```

## 2. Built-in Functions for Lists

Python provides high-performance built-in functions to summarize list data:

| Function | Syntax | Description | Example (`scores = [88, 42, 95]`) |
| :--- | :--- | :--- | :--- |
| `min()` | `min(lst)` | Returns the smallest item. | `min(scores)` → 42 |
| `max()` | `max(lst)` | Returns the largest item. | `max(scores)` → 95 |
| `sum()` | `sum(lst)` | Computes total numerical sum. | `sum(scores)` → 225 |
| `len()` | `len(lst)` | Returns total item count. | `len(scores)` → 3 |

**Tip (Calculate Averages)**

Combine `sum()` and `len()` to calculate averages dynamically:
```python
avg = sum(scores) / len(scores)
```

## 3. Essential List Methods Summary

| Method | Mutation Type | Description |
| :--- | :--- | :--- |
| `.extend(iterable)` | In-Place | Merges an iterable's elements into the end of the current list. |
| `.count(val)` | Non-Mutating | Returns integer count of how many times `val` appears. |
| `.index(val)` | Non-Mutating | Returns 0-based index of first occurrence of `val`. Throws `ValueError` if missing. |
| `.sort(reverse=Bool)` | In-Place | Sorts elements in ascending (`False`) or descending (`True`) order. |
| `.reverse()` | In-Place | Reverses list elements in-place. |
| `.copy()` | Non-Mutating | Returns a new shallow copy of the list structure. |
| `.clear()` | In-Place | Empties all elements, making `len(list) == 0`. |

**NOTE (`.append` v/s `.extend`)**

```python
# .append() v/s .extend()
a = [1, 2]
a.append([3, 4])  # Result: [1, 2, [3, 4]] -> Nested List

b = [1, 2]
b.extend([3, 4])  # Result: [1, 2, 3, 4]   -> Flattened Merge
```

## 4. Aliasing vs. Shallow Copying (`.copy()`)
In Python, assigning a list to a new variable using `=` creates a reference alias, not a duplicate list.

```python
# ALIASING (Dangerous side-effects)
original = [1, 2, 3]
alias = original
alias.append(99)
print(original)  # Output: [1, 2, 3, 99] (Original changed!)

# SHALLOW COPYING (Safe duplication)
original = [1, 2, 3]
copy_list = original.copy()
copy_list.append(99)
print(original)  # Output: [1, 2, 3] (Original untouched)
```

## 5. Standard Problem-Solving Patterns

### Pattern A: Removing All Occurrences of an Item
Because `.remove()` deletes only the first match, use a `while` loop to purge all duplicate targets:

```python
values = [12, 0, 45, 0, 78, 0]
while 0 in values:
    values.remove(0)  # Repeats until all 0s are removed
```

### Pattern B: Middle Index Insertion
Calculate exact middle insertion points using integer floor division (`//`):

```python
lst = ["A", "B", "D", "E"]
mid_idx = len(lst) // 2  # 4 // 2 = 2
lst.insert(mid_idx, "C") # Inserts "C" at index 2
```

### Pattern C: Deduplication with Order Preservation
Remove duplicates while maintaining initial sequence ordering:

```python
raw_data = [101, 102, 101, 103, 102]
unique_data = []

for item in raw_data:
    if item not in unique_data:
        unique_data.append(item)
```

### Pattern D: Safe Searching (`in` + `.index()`)
Always guard `.index()` calls with the `in` membership operator to prevent code crashes:

```python
items = ["pen", "paper"]
target = "eraser"

if target in items:
    idx = items.index(target)
else:
    print("Item not found")
```