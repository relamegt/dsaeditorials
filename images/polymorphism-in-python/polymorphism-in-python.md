# Polymorphism in Python

## Introduction

Polymorphism means "many forms". In Object-Oriented Programming (OOP), polymorphism allows the same method, function, or operator to behave differently depending on the object or data it works with. This makes programs more flexible, reusable, and easier to maintain.

### Key Features

- Enables one interface to support multiple behaviors.
- Improves code reusability and scalability.
- Supports method overriding and operator overloading.
- Promotes flexible and maintainable code.
- Works with built-in functions and user-defined classes.

## Why Polymorphism?

Without polymorphism, separate functions would be needed for every object type, leading to repetitive code.

### Example Without Polymorphism

```id="q7m5r2"
def process_card():
    print("Processing Card Payment")

def process_upi():
    print("Processing UPI Payment")

process_card()
process_upi()
```

### Output
Processing Card Payment
Processing UPI Payment

### Limitation

Each payment type requires a separate function. Adding new payment methods increases code duplication.

# Runtime Polymorphism (Method Overriding)

Runtime polymorphism occurs when child classes provide their own implementation of a method defined in the parent class.

### Example

```id="k3w8n1"
class Payment:
    def process_payment(self):
        return "Payment Processing"

class CardPayment(Payment):
    def process_payment(self):
        return "Card Payment Successful"

class UpiPayment(Payment):
    def process_payment(self):
        return "UPI Payment Successful"

payments = [
    CardPayment(),
    UpiPayment(),
    Payment()
]

for payment in payments:
    print(payment.process_payment())
```

### Output
Card Payment Successful
UPI Payment Successful
Payment Processing

### Explanation

The same method `process_payment()` behaves differently depending on the object.

# Polymorphism Using Built-in Functions

Python's built-in functions work with multiple data types.

### Example

```id="a9c6p4"
print(len("AlphaKnowledge"))
print(len([1, 2, 3, 4]))

print(max(5, 8, 3))
print(max("a", "z", "m"))
```

### Output
14
4
8
z

### Explanation

- `len()` works with strings and lists.
- `max()` works with numbers and characters.

# Polymorphism with Functions

Functions can work with different object types if they provide the required behavior.

### Example

```id="v4t7e8"
class Keyboard:
    def use(self):
        return "Typing"

class Mouse:
    def use(self):
        return "Clicking"

def perform_action(device):
    print(device.use())

perform_action(Keyboard())
perform_action(Mouse())
```

### Output
Typing
Clicking

### Explanation

The function `perform_action()` works with different objects as long as they provide a `use()` method.

# Operator Polymorphism

Operators can perform different operations depending on the operand types.

### Example

```id="p2h9s6"
print(10 + 5)

print("Alpha" + "Knowledge")

print([1, 2] + [3, 4])
```

### Output
15
AlphaKnowledge
[1, 2, 3, 4]

### Explanation

The `+` operator:

- Adds integers.
- Concatenates strings.
- Merges lists.

# Simulating Compile-Time Polymorphism

Python does not support traditional method overloading, but similar behavior can be achieved using default arguments.

### Example

```id="u6x1b5"
class Calculator:
    def multiply(
        self,
        a=1,
        b=1,
        *args
    ):
        result = a * b

        for num in args:
            result *= num

        return result

calc = Calculator()

print(calc.multiply())

print(calc.multiply(5))

print(calc.multiply(2, 3))

print(calc.multiply(2, 3, 4))
```

### Output
1
5
6
24

### Explanation

The same method handles different numbers of arguments, producing different results.

# Polymorphism with Multiple Objects

Different classes can share the same method name.

### Example

```id="r8j2m7"
class Mentor:
    def introduce(self):
        return "Mohit Chandaluri"

class Student:
    def introduce(self):
        return "Abhiram Gopisetti"

class Instructor:
    def introduce(self):
        return "Adapa Hemesh"

people = [
    Mentor(),
    Student(),
    Instructor()
]

for person in people:
    print(person.introduce())
```

### Output
Mohit Chandaluri
Abhiram Gopisetti
Adapa Hemesh

### Explanation

The same method name `introduce()` produces different results depending on the object.

# Advantages of Polymorphism

1. Reduces code duplication.
2. Improves code reusability.
3. Makes applications easier to extend.
4. Simplifies maintenance.
5. Promotes flexible program design.

# Limitations

1. Can make debugging more difficult.
2. Excessive use may increase complexity.
3. Understanding runtime behavior may be challenging for beginners.

# Summary

Polymorphism is one of the fundamental concepts of Object-Oriented Programming. It allows the same method, function, or operator to exhibit different behaviors depending on the object or data being used. Python supports polymorphism through method overriding, built-in functions, operator overloading, and duck typing, enabling developers to build reusable, scalable, and maintainable applications.

