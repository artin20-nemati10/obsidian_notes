# 🐍 Python — Stage 02 | Conditions & Logic

> **Level:** Beginner  
> **Topic:** Conditions & Logic  
> **Status:** 🟡 In Progress

---

## 🎯 Stage Goal

### Objective

Learn how to make decisions in Python using conditions and logical expressions.

### Topics

- `if`
- `elif`
- `else`
- Comparison Operators
- Logical Operators
- Nested Conditions
- Conditional Expressions
- Truthy & Falsy Values

---

## 01 — `if`

### Description

The `if` statement is used to execute code only when a condition is `True`.

### Syntax

```python
if condition:
    # code
```

### Example

```python
age = 18

if age >= 18:
    print("You are an adult.")
```

### Output

```text
You are an adult.
```

### Key Point

The code inside the `if` block only runs when the condition is `True`.

---

## 02 — `else`

### Description

The `else` statement runs when the `if` condition is `False`.

### Syntax

```python
if condition:
    # code
else:
    # code
```

### Example

```python
age = 16

if age >= 18:
    print("You are an adult.")
else:
    print("You are not an adult.")
```

### Output

```text
You are not an adult.
```

### Key Point

`else` does not have a condition. It runs when the previous `if` condition is `False`.

---

## 03 — `elif`

### Description

The `elif` statement means **else if**.

It allows us to check multiple conditions.

### Syntax

```python
if condition:
    # code

elif another_condition:
    # code

else:
    # code
```

### Example

```python
score = 75

if score >= 90:
    print("Grade A")
elif score >= 70:
    print("Grade B")
elif score >= 60:
    print("Grade C")
else:
    print("Grade F")
```

### Output

```text
Grade B
```

### Key Point

Python checks the conditions from top to bottom.

Once it finds a `True` condition, it executes that block and skips the remaining conditions.

---

## 04 — Comparison Operators

### Description

Comparison operators are used to compare values.

The result of a comparison is always a Boolean value:

`True` or `False`

### Operators

| Operator | Meaning | Example | Result |
|---|---|---|---|
| `==` | Equal | `5 == 5` | `True` |
| `!=` | Not Equal | `5 != 3` | `True` |
| `>` | Greater Than | `5 > 3` | `True` |
| `<` | Less Than | `5 < 3` | `False` |
| `>=` | Greater Than or Equal | `5 >= 5` | `True` |
| `<=` | Less Than or Equal | `5 <= 3` | `False` |

### Example

```python
a = 10
b = 5

print(a == b)
print(a != b)
print(a > b)
print(a < b)
print(a >= b)
print(a <= b)
```

### Output

```text
False
True
True
False
True
False
```

### Key Point

Do not confuse:

```python
=
```

with:

```python
==
```

`=` assigns a value.

`==` compares two values.

---

## 05 — Boolean Values

### Description

A Boolean value can only be:

```python
True
False
```

### Example

```python
is_student = True
is_admin = False

print(is_student)
print(is_admin)
```

### Output

```text
True
False
```

### Key Point

Booleans are heavily used in conditions and decision-making.

---

## 06 — Logical Operator: `and`

### Description

The `and` operator requires **both conditions** to be `True`.

### Example

```python
age = 20
has_id = True

if age >= 18 and has_id:
    print("Access granted.")
```

### Output

```text
Access granted.
```

### Truth Table

| A | B | `A and B` |
|---|---|---|
| `True` | `True` | `True` |
| `True` | `False` | `False` |
| `False` | `True` | `False` |
| `False` | `False` | `False` |

### Key Point

`and` means:

> **Both conditions must be True.**

---

## 07 — Logical Operator: `or`

### Description

The `or` operator returns `True` when **at least one condition** is `True`.

### Example

```python
day = "Saturday"

if day == "Saturday" or day == "Sunday":
    print("It's the weekend!")
```

### Output

```text
It's the weekend!
```

### Truth Table

| A | B | `A or B` |
|---|---|---|
| `True` | `True` | `True` |
| `True` | `False` | `True` |
| `False` | `True` | `True` |
| `False` | `False` | `False` |

### Key Point

`or` means:

> **At least one condition must be True.**

---

## 08 — Logical Operator: `not`

### Description

The `not` operator reverses a Boolean value.

### Example

```python
is_raining = False

if not is_raining:
    print("You don't need an umbrella.")
```

### Output

```text
You don't need an umbrella.
```

### Example

```python
print(not True)
print(not False)
```

### Output

```text
False
True
```

### Key Point

`not` changes:

```text
True  → False
False → True
```

---

## 09 — Combining Conditions

### Description

Multiple logical operators can be combined to create more complex conditions.

### Example

```python
age = 20
has_ticket = True

if age >= 18 and has_ticket:
    print("You can enter.")
else:
    print("You cannot enter.")
```

### Output

```text
You can enter.
```

### Key Point

Combining conditions allows programs to make more specific decisions.

---

## 10 — Nested Conditions

### Description

A nested condition is a condition placed inside another condition.

### Example

```python
age = 20
has_id = True

if age >= 18:
    if has_id:
        print("Access granted.")
    else:
        print("You need an ID.")
else:
    print("You are too young.")
```

### Output

```text
Access granted.
```

### Key Point

Nested conditions can be useful when one decision depends on another decision.

---

## 11 — Conditional Expressions

### Description

A conditional expression is a short way to write a simple `if/else`.

### Syntax

```python
value_if_true if condition else value_if_false
```

### Example

```python
age = 20

status = "Adult" if age >= 18 else "Minor"

print(status)
```

### Output

```text
Adult
```

### Key Point

Conditional expressions are useful for short and simple decisions.

---

## 12 — Truthy & Falsy Values

### Description

Python treats some values as `True` and some values as `False` when used in a condition.

### Common Falsy Values

```python
False
None
0
0.0
""
[]
{}
set()
```

### Example

```python
name = ""

if name:
    print("Name exists.")
else:
    print("Name is empty.")
```

### Output

```text
Name is empty.
```

### Key Point

An empty string, zero, `None`, and empty collections are commonly treated as `False`.

---

# 🧪 Mini Project — Grade Calculator

## Description

Let's build a program that takes a score and determines the student's grade.

### Code

```python
score = float(input("Enter your score: "))

if score >= 90:
    grade = "A"
elif score >= 80:
    grade = "B"
elif score >= 70:
    grade = "C"
elif score >= 60:
    grade = "D"
else:
    grade = "F"

print("Your grade is:", grade)
```

### Example Input

```text
Enter your score: 85
```

### Output

```text
Your grade is: B
```

### Concepts Used

- `if`
- `elif`
- `else`
- Comparison Operators
- Variables
- `input()`
- `float()`

---

# 🧪 Mini Project — Login System

## Description

Let's create a simple login system using conditions.

### Code

```python
username = input("Username: ")
password = input("Password: ")

if username == "admin" and password == "1234":
    print("Login successful.")
else:
    print("Invalid username or password.")
```

### Example Input

```text
Username: admin
Password: 1234
```

### Output

```text
Login successful.
```

### Key Point

The `and` operator requires both conditions to be `True`.

---

# 🧠 Stage Summary

## What I Learned

- [ ] `if`
- [ ] `elif`
- [ ] `else`
- [ ] Comparison Operators
- [ ] Boolean Values
- [ ] `and`
- [ ] `or`
- [ ] `not`
- [ ] Nested Conditions
- [ ] Conditional Expressions
- [ ] Truthy & Falsy Values

---

# 📌 Quick Reference

## Conditional Statements

```python
if condition:
    # code

elif another_condition:
    # code

else:
    # code
```

## Comparison Operators

```text
==    Equal
!=    Not Equal
>     Greater Than
<     Less Than
>=    Greater Than or Equal
<=    Less Than or Equal
```

## Logical Operators

```text
and   Both conditions must be True
or    At least one condition must be True
not   Reverses the Boolean value
```

---

# 🏆 Stage Challenge

## Task

Build a simple **Age & Access Checker**.

The program should:

1. Ask for the user's name.
2. Ask for the user's age.
3. Convert the age to an integer.
4. Check whether the user is 18 or older.
5. Display an appropriate message.

### Example

```text
Enter your name: Artin
Enter your age: 20

Hello Artin!
Access granted.
```

### Extra Challenge

Add another condition:

- If the age is below 13 → `"Child"`
- If the age is between 13 and 17 → `"Teenager"`
- If the age is 18 or older → `"Adult"`

### Expected Output

```text
Enter your name: Artin
Enter your age: 17

Hello Artin!
Category: Teenager
```

---

# 🧠 Practice Challenge

## Task

Create a program that asks for:

- Username
- Password

Then check:

- Username must be `"admin"`
- Password must be `"python123"`

If both are correct:

```text
Login successful!
```

Otherwise:

```text
Invalid credentials!
```

### Concepts to Use

- `input()`
- `if`
- `else`
- `==`
- `and`

---

# 🔗 Next Stage

## Stage 03 — Loops

### Topics

- `for`
- `while`
- `range()`
- Loop Control
- `break`
- `continue`
- Nested Loops
- Loop Patterns

---

> 🐍 **Think → Code → Test → Improve.** 🚀