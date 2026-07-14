# Lab Guide 02: Variables, Data Types, and Operators in Python

Cheatsheet for concepts in Practical Assignment 2. This document provides a foundational breakdown of how Python handles data storage, mathematical computations, type casting and logical expressions.

---

## 1. Variables and Core Data Types

* A **variable** is a named location in memory used to store data.
* Unlike statically typed languages (like Java or C++), Python uses **dynamic typing**.
* You do not need to declare a variable's type explicitly; Python infers it automatically at runtime.

### The Four Primary Primitive Types:
1. **String (`str`)**: Textual data enclosed in single (`'`) or double (`"`) quotes.
2. **Integer (`int`)**: Whole numbers without decimals (positive, negative, or zero).
3. **Float (`float`)**: Real numbers containing a fractional decimal component.
4. **Boolean (`bool`)**: Represents logical values: either `True` or `False`.

```python
# Example Declarations
first_name = "Alice"  # str
age = 25              # int
pi_value = 3.1415     # float
is_active = True      # bool
```

## 2. Advanced Arithmetic Operators

While standard operators like addition (`+`), subtraction (`-`), multiplication (`*`), and division (`/`) behave predictably, Python introduces specific operators for advanced math:

| Operator | Name | Description | Example (`a = 27`, `b = 5`) |
| :--- | :--- | :--- | :--- |
| `**` | Exponentiation | Raises the left operand to the power of the right. | `a ** 2` $\rightarrow 729$ |
| `%` | Modulus | Returns the remainder left over after division. | `a % b` $\rightarrow 2$ |
| `//` | Floor Division | Divides numbers and rounds down to the nearest whole integer. | `a // b` $\rightarrow 5$ |

### Key Distinction: `/` vs `//`
* **Normal Division (`/`)** *always* returns a `float`, even if the numbers divide perfectly (e.g., `4 / 2` output is `2.0`).
* **Floor Division (`//`)** truncates the fractional part, returning an `int` (unless one of the operands is a float).

## 3. Assignment and Compound Assignment Operators

The basic assignment operator is `=`. However, when updating a variable based on its current value, **Compound Assignment Operators** provide shorthand syntax.

```python
wallet = 100

# Traditional method
wallet = wallet + 50  # wallet is now 150

# Compound Shorthand (Highly Preferred)
wallet += 50   # Equivalent to wallet = wallet + 50
wallet -= 20   # Equivalent to wallet = wallet - 20
wallet *= 2    # Equivalent to wallet = wallet * 2
```

## 4. Relational (Comparison) Operators

Relational operators compare two values and evaluate to a Boolean result (`True` or `False`).

* `>` (Greater than)
* `<` (Less than)
* `>=` (Greater than or equal to)
* `<=` (Less than or equal to)
* `==` (Equal to)
* `!=` (Not equal to)

### Chaining Comparisons
Python allows intuitive operator chaining, which is unique compared to languages like C++ or Java:
```python
score = 85
# Checks if score is between 70 (exclusive) and 90 (inclusive)
is_valid = 70 < score <= 90  # Evaluates to True
```

## 6. Data Type Conversion (Type Casting)

Python provides built-in constructor functions to explicitly convert data from one type to another. This is crucial when handling user input, as the `input()` function *always* captures data as a string (`str`).

```python
# Reading user input
user_input = input("Enter a number: ")  # Captured as '10.5' (str)

# Explicit Type Casting
numeric_value = float(user_input)       # Converted to 10.5 (float)
```

> *Note:*
> Attempting to cast an incompatible string (like "abc") to an int or float will raise a ValueError.
> Always verify your string contains numeric characters before casting.