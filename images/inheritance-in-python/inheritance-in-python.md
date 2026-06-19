# Inheritance in Python

## Introduction

Inheritance is one of the fundamental concepts of Object-Oriented Programming (OOP). It allows a class to acquire the properties and methods of another class. The existing class is called the **parent class**, while the new class that inherits from it is called the **child class**.

Inheritance helps avoid code duplication and makes programs easier to maintain and extend.

### Key Features

- Promotes code reusability.
- Reduces duplicate code.
- Supports hierarchical relationships.
- Allows method overriding.
- Improves maintainability and scalability.

## Why Inheritance?

Without inheritance, common functionality must be rewritten in every class, leading to repetitive code.

### Example Without Inheritance

```python
class Student:
    def login(self):
        print("Login Successful")

class Teacher:
    def login(self):
        print("Login Successful")

student = Student()
teacher = Teacher()

student.login()
teacher.login()
```

### Output
Login Successful
Login Successful

### Limitation

Both classes contain identical code. If the login process changes, modifications must be made in every class separately.

# Basic Inheritance

A child class can inherit methods and attributes from a parent class.

### Example

```python
class User:
    def __init__(
        self,
        username
    ):
        self.username = username

    def display_user(self):
        print(
            "Username:",
            self.username
        )

class PremiumUser(User):
    def access_premium(self):
        print(
            self.username,
            "has premium access"
        )

user1 = PremiumUser(
    "Akash"
)

user1.display_user()
user1.access_premium()
```

### Output
Username: Akash
Akash has premium access

### Explanation

- `User` is the parent class.
- `PremiumUser` is the child class.
- The child class inherits `display_user()`.
- It also defines its own method, `access_premium()`.

# Benefits of Inheritance

- Promotes code reusability.
- Creates real-world relationships.
- Simplifies maintenance.
- Makes applications extensible.
- Supports polymorphism.

# Using super()

The `super()` function allows a child class to access methods and constructors of the parent class.

### Example

```python
class Employee:
    def __init__(
        self,
        name
    ):
        self.name = name

    def show_name(self):
        print(
            "Employee:",
            self.name
        )

class Developer(Employee):
    def __init__(
        self,
        name,
        language
    ):
        super().__init__(name)
        self.language = language

    def show_details(self):
        print(
            self.name,
            "works with",
            self.language
        )

dev = Developer(
    "Rohit",
    "Python"
)

dev.show_name()
dev.show_details()
```

### Output
Employee: Rohit
Rohit works with Python

### Explanation

- `super().__init__()` calls the constructor of the parent class.
- It initializes the inherited attribute `name`.
- The child class adds its own attribute `language`.

# Method Overriding

Method overriding allows a child class to provide its own implementation of a method defined in the parent class.

### Example

```python
class Notification:
    def send(self):
        print(
            "Sending notification"
        )

class EmailNotification(Notification):
    def send(self):
        print(
            "Sending email notification"
        )

message = EmailNotification()

message.send()
```

### Output
Sending email notification

### Explanation

- The parent class defines `send()`.
- The child class overrides it with a specialized implementation.
- Python executes the child class method when the object calls `send()`.

# Types of Inheritance

Python supports different types of inheritance.

## Single Inheritance

One child class inherits from one parent class.

### Example

```python
class Appliance:
    def power_on(self):
        print(
            "Device Powered On"
        )

class Television(Appliance):
    pass

tv = Television()

tv.power_on()
```

### Output
Device Powered On

## Multilevel Inheritance

A class inherits from another child class.

### Example

```python
class Person:
    def walk(self):
        print(
            "Walking"
        )

class Employee(Person):
    def work(self):
        print(
            "Working"
        )

class Manager(Employee):
    def manage(self):
        print(
            "Managing Team"
        )

manager = Manager()

manager.walk()
manager.work()
manager.manage()
```

### Output
Walking
Working
Managing Team

## Multiple Inheritance

A class inherits from multiple parent classes.

### Example

```python
class Camera:
    def capture(self):
        print(
            "Capturing Image"
        )

class Speaker:
    def play_music(self):
        print(
            "Playing Music"
        )

class SmartPhone(
    Camera,
    Speaker
):
    pass

phone = SmartPhone()

phone.capture()
phone.play_music()
```

### Output
Capturing Image
Playing Music

## Hierarchical Inheritance

Multiple child classes inherit from the same parent class.

### Example

```python
class Account:
    def login(self):
        print(
            "Login Successful"
        )

class Student(Account):
    pass

class Faculty(Account):
    pass

student = Student()
faculty = Faculty()

student.login()
faculty.login()
```

### Output
Login Successful
Login Successful

# isinstance() Function

The `isinstance()` function checks whether an object belongs to a class.

### Example

```python
class Vehicle:
    pass

class Bike(Vehicle):
    pass

b = Bike()

print(
    isinstance(
        b,
        Bike
    )
)

print(
    isinstance(
        b,
        Vehicle
    )
)
```

### Output
True
True

### Explanation

Since `Bike` inherits from `Vehicle`, the object belongs to both classes.

# Advantages of Inheritance

1. Encourages code reuse.
2. Makes maintenance easier.
3. Reduces redundancy.
4. Supports method overriding.
5. Models real-world relationships effectively.

# Limitations

1. Deep inheritance structures can become difficult to understand.
2. Changes in parent classes may affect child classes.
3. Excessive inheritance may increase complexity.

# Summary

Inheritance allows a child class to inherit attributes and methods from a parent class. It helps reduce code duplication, promotes reusability, and supports extensible software design. Python supports single, multilevel, multiple, and hierarchical inheritance, making it easier to model real-world relationships and build scalable applications.

