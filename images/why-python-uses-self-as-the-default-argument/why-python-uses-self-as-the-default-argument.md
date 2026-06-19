# Why Python Uses `self` as the Default Argument

## Introduction

In Python, instance methods inside a class use `self` as their first parameter. The `self` parameter represents the current object of the class and allows methods to access and modify the object's attributes and other methods. Although `self` is not a reserved keyword, it is a widely followed naming convention in Python.

### Key Features

- Represents the current object of the class.
- Allows access to instance variables and methods.
- Makes object-oriented programming explicit and readable.
- Helps multiple objects maintain their own data.
- Promotes consistency across classes.

## Why Use `self`?

Every object created from a class contains its own data. The `self` parameter helps methods determine which object's data they should access.

### Example Without `self`

```id="q8n4k7"
class Student:
    name = "Akash Dangudubiyyapu"

    def display():
        print(name)
```

### Limitation

Without `self`, methods cannot access object-specific data. Python would not know which object's attributes should be used.

# Understanding `self`

The `self` parameter refers to the current instance of the class. Python automatically passes the object as the first argument when a method is called.

### Example

```id="f2m7x1"
class Student:
    def __init__(self, name):
        self.name = name

    def display(self):
        print(self.name)

student = Student(
    "Akash Dangudubiyyapu"
)

student.display()
```

### Output
Akash Dangudubiyyapu

### Explanation

- `self.name` stores the value inside the object.
- `display()` uses `self.name` to access the object's data.
- Python automatically passes `student` as the `self` argument.

# Why Doesn't Python Use Implicit References?

Python follows the philosophy:

> Explicit is better than implicit.

Using `self` makes it clear that methods are working with object data instead of local variables.

### Benefits

- Improves readability.
- Makes code easier to understand.
- Avoids ambiguity.
- Provides flexibility.

# Accessing Instance Variables

`self` allows methods to access variables stored inside an object.

### Example

```id="r6h3v8"
class Course:
    def __init__(self, topic):
        self.topic = topic

    def show_topic(self):
        print("Topic:", self.topic)

course = Course(
    "Python Programming"
)

course.show_topic()
```

### Output
Topic: Python Programming

### Explanation

The value stored inside `self.topic` belongs to the current object and can be accessed by any method of the class.

# Multiple Objects and `self`

Each object maintains its own data through `self`.

### Example

```id="w9k1a5"
class Mentor:
    def __init__(self, name):
        self.name = name

    def display(self):
        print(self.name)

mentor1 = Mentor("Mohit Chandaluri")
mentor2 = Mentor("Abhiram Gopisetti")

mentor1.display()
mentor2.display()
```

### Output
Mohit Chandaluri
Abhiram Gopisetti

### Explanation

Even though both objects use the same class, `self` ensures that each object accesses its own data.

# Using `self` for Calculations

Methods can use instance variables through `self` to perform computations.

### Example

```id="u4c8j2"
class Circle:
    def __init__(self, radius):
        self.radius = radius

    def area(self):
        return 3.14 * self.radius ** 2

circle = Circle(5)

print(circle.area())
```

### Output
78.5

### Explanation

The `area()` method uses `self.radius`, which belongs to the current object.

# Is `self` a Keyword?

No. `self` is not a keyword. You can technically use another name.

### Example

```id="n5b2e9"
class Student:
    def __init__(current, name):
        current.name = name

    def display(current):
        print(current.name)

student = Student(
    "Adapa Hemesh"
)

student.display()
```

### Output
Adapa Hemesh

### Explanation

Although any name can be used, `self` is the standard convention followed by Python programmers.

# Advantages of Using `self`

1. Identifies the current object.
2. Provides access to instance variables.
3. Enables interaction between methods.
4. Makes code explicit and readable.
5. Supports multiple objects with separate data.

# Limitations

1. Beginners may initially find it confusing.
2. Forgetting `self` causes errors.
3. Using inconsistent names reduces readability.

# Summary

Python uses `self` to represent the current instance of a class. It enables methods to access object attributes and other methods, making object-oriented programming explicit and easy to understand. Although `self` is not a keyword, it is the standard naming convention and plays a fundamental role in creating and managing objects in Python.

