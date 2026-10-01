# 🐍 Python — Stage 03 | Loops

> **Level:** Beginner  
> **Topic:** Loops & Iteration  
> **Status:** 🟡 In Progress

---

## 🎯 Stage Goal

### Objective

Learn how to repeat code efficiently using loops and understand how Python handles repeated tasks.

### Topics

- `for`
- `while`
- `range()`
- Loop Variables
- `break`
- `continue`
- Nested Loops
- `else` with Loops
- Loop Patterns

---

## 01 — What Is a Loop?

### Description

A loop allows us to execute the same block of code multiple times.

Instead of writing:

```python
print("Hello")
print("Hello")
print("Hello")
print("Hello")
print("Hello")
```

We can use a loop.

### Example

```python
for i in range(5):
    print("Hello")
```

### Output

```text
Hello
Hello
Hello
Hello
Hello
```

### Key Point

Loops are useful when we need to repeat an action multiple times.

---

## 02 — `for` Loop

### Description

A `for` loop is used to iterate over a sequence or collection of values.

### Syntax

```python
for variable in sequence:
    # code
```

### Example

```python
for number in [1, 2, 3, 4, 5]:
    print(number)
```

### Output

```text
1
2
3
4
5
```

### Key Point

The loop takes each value from the sequence one by one.

---

## 03 — Loop Variable

### Description

The variable after `for` stores the current value during each iteration.

### Example

```python
for number in [10, 20, 30]:
    print(number)
```

### Output

```text
10
20
30
```

### Explanation

During each iteration:

```text
First iteration → number = 10
Second iteration → number = 20
Third iteration → number = 30
```

### Key Point

The loop variable changes automatically during every iteration.

---

## 04 — `range()`

### Description

The `range()` function generates a sequence of numbers.

### Syntax

```python
range(stop)
```

### Example

```python
for number in range(5):
    print(number)
```

### Output

```text
0
1
2
3
4
```

### Key Point

`range(5)` starts from `0` and stops before `5`.

---

## 05 — `range(start, stop)`

### Description

We can specify both the starting and ending values.

### Example

```python
for number in range(1, 6):
    print(number)
```

### Output

```text
1
2
3
4
5
```

### Key Point

The `stop` value is not included.

```python
range(1, 6)
```

means:

```text
1 → 2 → 3 → 4 → 5
```

---

## 06 — `range(start, stop, step)`

### Description

The third argument controls how much the number changes each time.

### Syntax

```python
range(start, stop, step)
```

### Example

```python
for number in range(0, 11, 2):
    print(number)
```

### Output

```text
0
2
4
6
8
10
```

### Key Point

The `step` controls the amount added after each iteration.

---

## 07 — Counting Backwards

### Description

A negative step can be used to count backwards.

### Example

```python
for number in range(10, 0, -1):
    print(number)
```

### Output

```text
10
9
8
7
6
5
4
3
2
1
```

### Key Point

A negative `step` moves through the range backwards.

---

## 08 — Looping Through a String

### Description

Strings are sequences of characters, so we can use a `for` loop to process each character.

### Example

```python
name = "Python"

for letter in name:
    print(letter)
```

### Output

```text
P
y
t
h
o
n
```

### Key Point

A `for` loop can iterate through each character in a string.

---

## 09 — `while` Loop

### Description

A `while` loop repeats code as long as its condition is `True`.

### Syntax

```python
while condition:
    # code
```

### Example

```python
number = 1

while number <= 5:
    print(number)
    number += 1
```

### Output

```text
1
2
3
4
5
```

### Key Point

A `while` loop continues running while its condition remains `True`.

---

## 10 — Updating a `while` Loop

### Description

A `while` loop usually needs a variable that changes during each iteration.

### Example

```python
count = 1

while count <= 5:
    print(count)
    count += 1
```

### Output

```text
1
2
3
4
5
```

### Key Point

If the condition never becomes `False`, the loop can continue forever.

### ⚠️ Infinite Loop

```python
count = 1

while count <= 5:
    print(count)
```

This loop never changes `count`, so the condition remains `True`.

---

## 11 — `break`

### Description

The `break` statement immediately stops a loop.

### Example

```python
for number in range(1, 11):

    if number == 6:
        break

    print(number)
```

### Output

```text
1
2
3
4
5
```

### Key Point

`break` completely exits the current loop.

---

## 12 — `continue`

### Description

The `continue` statement skips the current iteration and moves to the next one.

### Example

```python
for number in range(1, 6):

    if number == 3:
        continue

    print(number)
```

### Output

```text
1
2
4
5
```

### Key Point

`continue` skips only the current iteration.

---

## 13 — `break` vs `continue`

### Description

These two statements have different purposes.

| Statement | Purpose |
|---|---|
| `break` | Stop the entire loop |
| `continue` | Skip the current iteration |

### Example

```python
for number in range(1, 6):

    if number == 3:
        break

    print(number)
```

### Output

```text
1
2
```

### Example

```python
for number in range(1, 6):

    if number == 3:
        continue

    print(number)
```

### Output

```text
1
2
4
5
```

### Key Point

Use `break` when you want to **stop**.

Use `continue` when you want to **skip**.

---

## 14 — Nested Loops

### Description

A nested loop is a loop inside another loop.

### Example

```python
for i in range(3):

    for j in range(3):
        print(i, j)
```

### Output

```text
0 0
0 1
0 2
1 0
1 1
1 2
2 0
2 1
2 2
```

### Key Point

The inner loop runs completely for every iteration of the outer loop.

---

## 15 — Looping Through a List

### Description

Loops are commonly used to process items inside a list.

### Example

```python
languages = ["Python", "Go", "Java", "C++"]

for language in languages:
    print(language)
```

### Output

```text
Python
Go
Java
C++
```

### Key Point

The `for` loop is one of the most common ways to process list elements.

---

## 16 — `enumerate()`

### Description

`enumerate()` allows us to get both the index and the value while looping.

### Example

```python
languages = ["Python", "Go", "Java"]

for index, language in enumerate(languages):
    print(index, language)
```

### Output

```text
0 Python
1 Go
2 Java
```

### Key Point

`enumerate()` is useful when you need both the item's position and its value.

---

## 17 — Looping with `else`

### Description

Python allows an `else` block after a loop.

The `else` block runs when the loop finishes normally.

### Example

```python
for number in range(5):
    print(number)
else:
    print("Loop finished.")
```

### Output

```text
0
1
2
3
4
Loop finished.
```

### Key Point

The loop's `else` does not run if the loop is stopped using `break`.

### Example

```python
for number in range(5):

    if number == 3:
        break

    print(number)

else:
    print("Loop finished.")
```

### Output

```text
0
1
2
```

---

## 18 — Nested `while` Loops

### Description

A `while` loop can also contain another `while` loop.

### Example

```python
i = 1

while i <= 3:

    j = 1

    while j <= 3:
        print(i, j)
        j += 1

    i += 1
```

### Output

```text
1 1
1 2
1 3
2 1
2 2
2 3
3 1
3 2
3 3
```

### Key Point

Nested loops are useful for working with grids, tables, patterns, and multidimensional data.

---

# 🧪 Mini Project — Number Counter

## Description

Create a program that prints numbers from 1 to 10.

### Code

```python
for number in range(1, 11):
    print(number)
```

### Output

```text
1
2
3
4
5
6
7
8
9
10
```

### Concepts Used

- `for`
- `range()`
- Loop Variable

---

# 🧪 Mini Project — Even Numbers

## Description

Create a program that prints all even numbers from 1 to 20.

### Code

```python
for number in range(1, 21):

    if number % 2 == 0:
        print(number)
```

### Output

```text
2
4
6
8
10
12
14
16
18
20
```

### Concepts Used

- `for`
- `range()`
- `if`
- `%`
- Comparison Operators

---

# 🧪 Mini Project — Password Attempts

## Description

Create a simple program that gives the user multiple attempts to enter the correct password.

### Code

```python
correct_password = "python123"

for attempt in range(3):

    password = input("Enter password: ")

    if password == correct_password:
        print("Login successful.")
        break

    print("Incorrect password.")

else:
    print("Too many failed attempts.")
```

### Example Input

```text
Enter password: hello
Incorrect password.

Enter password: test
Incorrect password.

Enter password: python123
Login successful.
```

### Key Point

The `break` statement stops the loop when the correct password is entered.

---

# 🧪 Mini Project — Multiplication Table

## Description

Create a multiplication table using a `for` loop.

### Code

```python
number = int(input("Enter a number: "))

for i in range(1, 11):
    print(number, "x", i, "=", number * i)
```

### Example Input

```text
Enter a number: 5
```

### Output

```text
5 x 1 = 5
5 x 2 = 10
5 x 3 = 15
5 x 4 = 20
5 x 5 = 25
5 x 6 = 30
5 x 7 = 35
5 x 8 = 40
5 x 9 = 45
5 x 10 = 50
```

### Concepts Used

- `input()`
- `int()`
- `for`
- `range()`
- Arithmetic Operators

---

# 🧪 Mini Project — Sum of Numbers

## Description

Calculate the sum of numbers from 1 to 100.

### Code

```python
total = 0

for number in range(1, 101):
    total += number

print("Total:", total)
```

### Output

```text
Total: 5050
```

### Key Point

`total += number` is a shorter version of:

```python
total = total + number
```

---

# 🧪 Mini Project — Guessing Game

## Description

Create a simple number guessing game.

### Code

```python
secret_number = 7

while True:

    guess = int(input("Guess the number: "))

    if guess == secret_number:
        print("Correct!")
        break

    elif guess < secret_number:
        print("Too low.")

    else:
        print("Too high.")
```

### Example

```text
Guess the number: 4
Too low.

Guess the number: 9
Too high.

Guess the number: 7
Correct!
```

### Concepts Used

- `while`
- `if`
- `elif`
- `else`
- `break`
- `input()`
- `int()`

---

# 🧠 Stage Summary

## What I Learned

- [ ] What loops are
- [ ] `for`
- [ ] `while`
- [ ] Loop Variables
- [ ] `range()`
- [ ] `break`
- [ ] `continue`
- [ ] Nested Loops
- [ ] `enumerate()`
- [ ] Loop `else`
- [ ] Infinite Loops
- [ ] Loop Patterns

---

# 📌 Quick Reference

## `for` Loop

```python
for item in sequence:
    # code
```

## `while` Loop

```python
while condition:
    # code
```

## `range()`

```python
range(stop)

range(start, stop)

range(start, stop, step)
```

## Loop Control

```python
break
continue
```

## `enumerate()`

```python
for index, value in enumerate(items):
    print(index, value)
```

---

# 🏆 Stage Challenge

## Challenge 01 — Number Analyzer

Build a program that asks the user for a number `N`.

Then:

1. Print all numbers from `1` to `N`.
2. Print all even numbers.
3. Print all odd numbers.
4. Calculate the total sum.
5. Count how many even numbers there are.
6. Count how many odd numbers there are.

### Example

```text
Enter a number: 10

Numbers:
1 2 3 4 5 6 7 8 9 10

Even Numbers:
2 4 6 8 10

Odd Numbers:
1 3 5 7 9

Sum: 55
Even Count: 5
Odd Count: 5
```

---

# 🏆 Stage Challenge 02 — Pattern

## Task

Use nested loops to create this pattern:

```text
*
**
***
****
*****
```

### Hint

Use:

```python
for
range()
```

---

# 🏆 Stage Challenge 03 — Advanced

## Task

Create a simple menu program.

The menu should look like:

```text
===== MENU =====

1. Say Hello
2. Show Numbers
3. Exit
```

The program should continue running until the user chooses option `3`.

### Concepts to Use

- `while`
- `if`
- `elif`
- `else`
- `break`
- `input()`
- `for`
- `range()`

---

# 🧠 Important Concepts

## When Should I Use `for`?

Use `for` when you know what you want to iterate over.

```python
for number in range(10):
    print(number)
```

## When Should I Use `while`?

Use `while` when you want to continue until a condition changes.

```python
while password != "python123":
    password = input("Password: ")
```

## When Should I Use `break`?

Use `break` when you need to stop the loop immediately.

## When Should I Use `continue`?

Use `continue` when you want to skip the current iteration.

---

# 🔗 Next Stage

## Stage 04 — Strings

### Topics

- String Basics
- Indexing
- Slicing
- String Methods
- String Formatting
- f-Strings
- Escape Characters
- String Searching
- String Validation

---

> 🐍 **Don't repeat code. Automate it with loops.** 🔁🚀