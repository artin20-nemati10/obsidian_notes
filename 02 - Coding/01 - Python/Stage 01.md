# 🐍 Python — Stage 01 | Basics

> **Level:** Beginner  
> **Topic:** Python Fundamentals  
> **Status:** 🟡 In Progress

---

## 🎯 Stage Goal

### Objective

Learn the fundamental concepts of Python and understand how basic Python programs work.

### Topics

- `print()`
- Variables
- Data Types
- `input()`
- Type Conversion
- Arithmetic Operators
- Comments

---

## 01 — `print()`

### Description

The `print()` function is used to display information in the console.

### Syntax

```python
print(value)
```

### Example

```python
print("Hello, World!")
print("My name is Artin")
```

### Output

```text
Hello, World!
My name is Artin
```

### Key Point

The `print()` function displays information in the console.

---

## 02 — Variables

### Description

A variable is a name used to store a value.

### Syntax

```python
variable_name = value
```

### Example

```python
name = "Artin"
age = 17

print(name)
print(age)
```

### Output

```text
Artin
17
```

### Key Point

Python automatically determines the data type of a variable.

---

## 03 — Data Types

### Description

A data type defines what kind of value a variable contains.

### Common Data Types

| Type | Example | Description |
|---|---|---|
| `str` | `"Artin"` | Text |
| `int` | `17` | Integer |
| `float` | `3.14` | Decimal number |
| `bool` | `True` | Boolean |
| `None` | `None` | No value |

### Example

```python
name = "Artin"
age = 17
height = 1.75
student = True
```

### Key Point

Python has many built-in data types. These are some of the most important beginner types.

---

## 04 — `type()`

### Description

The `type()` function is used to check the data type of a value.

### Syntax

```python
type(value)
```

### Example

```python
name = "Artin"
age = 17

print(type(name))
print(type(age))
```

### Output

```text
<class 'str'>
<class 'int'>
```

### Key Point

`type()` is useful when you want to know what type of data you are working with.

---

## 05 — `input()`

### Description

The `input()` function allows the user to enter information into the program.

### Syntax

```python
input("message")
```

### Example

```python
name = input("Enter your name: ")

print("Hello", name)
```

### Output

```text
Enter your name: Artin
Hello Artin
```

### Key Point

The program waits for the user to enter something and press Enter.

### Important

`input()` returns a `str` by default.

### Example

```python
age = input("Enter your age: ")

print(type(age))
```

### Output

```text
Enter your age: 17
<class 'str'>
```

---

## 06 — Type Conversion

### Description

Type conversion means changing a value from one data type to another.

### Common Functions

```python
int()
float()
str()
bool()
```

### Example

```python
age = "17"

age = int(age)

print(age)
print(type(age))
```

### Output

```text
17
<class 'int'>
```

### Another Example

```python
price = 19

price = float(price)

print(price)
```

### Output

```text
19.0
```

### Key Point

Type conversion is especially useful when working with values received from `input()`.

---

## 07 — Arithmetic Operators

### Description

Arithmetic operators are used to perform mathematical calculations.

### Operator Table

| Operator | Name | Example | Result |
|---|---|---|---|
| `+` | Addition | `10 + 3` | `13` |
| `-` | Subtraction | `10 - 3` | `7` |
| `*` | Multiplication | `10 * 3` | `30` |
| `/` | Division | `10 / 3` | `3.333...` |
| `//` | Floor Division | `10 // 3` | `3` |
| `%` | Modulo | `10 % 3` | `1` |
| `**` | Power | `10 ** 3` | `1000` |

### Example

```python
a = 10
b = 3

print(a + b)
print(a - b)
print(a * b)
print(a / b)
print(a // b)
print(a % b)
print(a ** b)
```

### Output

```text
13
7
30
3.3333333333333335
3
1
1000
```

### Key Point

The `%` operator returns the remainder of a division.

### Example

```python
print(10 % 3)
```

### Output

```text
1
```

---

## 08 — Comments

### Description

Comments are notes written inside the code for humans.

Python ignores comments when executing the program.

### Syntax

```python
# This is a comment
```

### Example

```python
# Store the user's name
name = "Artin"

print(name)
```

### Output

```text
Artin
```

### Key Point

Comments make code easier to understand and maintain.

---

# 🧪 Mini Project — Simple Calculator

## Description

Let's combine variables, `input()`, type conversion, and arithmetic operators.

### Code

```python
num1 = float(input("Enter first number: "))
num2 = float(input("Enter second number: "))

print("Sum:", num1 + num2)
print("Difference:", num1 - num2)
print("Multiplication:", num1 * num2)
print("Division:", num1 / num2)
```

### Example Input

```text
Enter first number: 10
Enter second number: 5
```

### Output

```text
Sum: 15.0
Difference: 5.0
Multiplication: 50.0
Division: 2.0
```

### Concepts Used

- Variables
- `input()`
- `float()`
- `print()`
- Arithmetic Operators

---

# 🧠 Stage Summary

## What I Learned

- [ ] `print()`
- [ ] Variables
- [ ] Data Types
- [ ] `type()`
- [ ] `input()`
- [ ] Type Conversion
- [ ] Arithmetic Operators
- [ ] Comments

---

# 🏆 Stage Challenge

## Task

Build a program that:

1. Asks the user for their name.
2. Asks the user for their age.
3. Converts the age into an integer.
4. Calculates their approximate birth year.
5. Displays the information clearly.

### Expected Output

```text
Enter your name: Artin
Enter your age: 17

Name: Artin
Age: 17
Birth Year: 2009
```

### Extra Challenge

Add the user's favorite programming language.

### Expected Output

```text
Name: Artin
Age: 17
Birth Year: 2009
Favorite Language: Python
```

---

# 📌 Quick Reference

## Functions

```python
print()
input()
type()
int()
float()
str()
bool()
```

## Data Types

```python
str
int
float
bool
None
```

## Operators

```text
+     Addition
-     Subtraction
*     Multiplication
/     Division
//    Floor Division
%     Modulo
**    Power
```

---

# 🔗 Next Stage

## Stage 02 — Conditions & Logic

### Topics

- `if`
- `elif`
- `else`
- Comparison Operators
- Logical Operators
- Nested Conditions
- Conditional Expressions

---

> 🐍 **Learn → Practice → Build → Repeat.** 🚀