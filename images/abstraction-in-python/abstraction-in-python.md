# Abstraction in Python

## Introduction

Abstraction is one of the core concepts of Object-Oriented Programming (OOP). It focuses on hiding implementation details and exposing only the essential functionality to the user. By using abstraction, developers can simplify complex systems and provide a clear interface for interacting with objects.

Python supports abstraction through the `abc` module, which allows the creation of abstract classes and abstract methods.

### Key Features

- Hides implementation details from users.
- Exposes only essential functionality.
- Improves code maintainability.
- Promotes loose coupling between components.
- Provides a common interface for derived classes.

## Why Abstraction?

In many applications, users only need to know what an object does, not how it performs the task internally.

### Example Without Abstraction

```python
class CreditCardPayment:
    def pay(self, amount):
        print("Processing card verification")
        print("Connecting to bank server")
        print("Deducting amount")
        print("Payment Successful")

payment = CreditCardPayment()

payment.pay(500)
```

### Output
Processing card verification
Connecting to bank server
Deducting amount
Payment Successful

### Limitation

The user is exposed to all internal processing steps. If multiple payment methods are introduced, managing different implementations becomes difficult.

# Abstract Base Class

Abstract Base Classes (ABC) provide a common blueprint for subclasses. An abstract class cannot be instantiated directly and forces child classes to implement specific methods.

### Example

```python
from abc import ABC, abstractmethod

class Payment(ABC):

    @abstractmethod
    def make_payment(self, amount):
        pass

class UpiPayment(Payment):

    def make_payment(self, amount):
        return f"₹{amount} paid using UPI"

transaction = UpiPayment()

print(
    transaction.make_payment(750)
)
```

### Output
₹750 paid using UPI

### Explanation

- `Payment` is an abstract class.
- `make_payment()` is an abstract method.
- `UpiPayment` implements the abstract method.
- Objects can only be created from concrete subclasses.

# Components of Abstraction

Abstraction consists of several important components.

## 1. Abstract Method

An abstract method declares functionality without providing implementation. Subclasses must implement these methods.

### Example

```python
from abc import ABC, abstractmethod

class Notification(ABC):

    @abstractmethod
    def send(self):
        pass
```

### Explanation

The `send()` method provides a contract that every subclass must implement.

## 2. Concrete Method

Concrete methods contain implementation and can be inherited directly by subclasses.

### Example

```python
from abc import ABC, abstractmethod

class Notification(ABC):

    @abstractmethod
    def send(self):
        pass

    def status(self):
        return "Notification Service Active"

class EmailNotification(Notification):

    def send(self):
        return "Email Sent"

message = EmailNotification()

print(
    message.status()
)
```

### Output
Notification Service Active

### Explanation

The `status()` method already contains implementation, so subclasses can use it without redefining it.

## 3. Abstract Properties

Abstract properties enforce subclasses to provide property implementations.

### Example

```python
from abc import ABC, abstractmethod

class Employee(ABC):

    @property
    @abstractmethod
    def department(self):
        pass

class SoftwareEngineer(Employee):

    @property
    def department(self):
        return "Development"

emp = SoftwareEngineer()

print(
    emp.department
)
```

### Output
Development

### Explanation

The abstract property `department` must be implemented by all derived classes.

## 4. Abstract Class Instantiation

Abstract classes cannot be instantiated directly.

### Example

```python
from abc import ABC, abstractmethod

class Vehicle(ABC):

    @abstractmethod
    def start(self):
        pass

car = Vehicle()
```

### Output
TypeError:
Can't instantiate abstract class Vehicle with abstract method start

### Explanation

Since `Vehicle` contains an abstract method, Python prevents object creation until all abstract methods are implemented.

# Real-World Example of Abstraction

Abstraction is commonly used in streaming platforms. Different video qualities provide the same functionality but have different implementations.

### Example

```python
from abc import ABC, abstractmethod

class VideoPlayer(ABC):

    @abstractmethod
    def play(self):
        pass

class HDPlayer(VideoPlayer):

    def play(self):
        return "Playing video in HD quality"

class UltraHDPlayer(VideoPlayer):

    def play(self):
        return "Playing video in 4K quality"

hd = HDPlayer()
uhd = UltraHDPlayer()

print(
    hd.play()
)

print(
    uhd.play()
)
```

### Output
Playing video in HD quality
Playing video in 4K quality

### Explanation

Users only call the `play()` method. The internal implementation differs for each player, but that complexity is hidden.

# Advantages of Abstraction

1. Hides unnecessary implementation details.
2. Makes programs easier to understand.
3. Improves code reusability.
4. Provides better maintainability.
5. Enforces consistency across subclasses.

# Limitations

1. Adds extra complexity in simple applications.
2. Requires additional classes and interfaces.
3. Excessive abstraction can make debugging difficult.
4. Slightly increases development time.

# Summary

Abstraction is an OOP principle that hides internal implementation details and exposes only the necessary functionality. Python achieves abstraction using abstract classes and abstract methods through the `abc` module. This approach simplifies code, improves maintainability, and provides a clear structure for building scalable applications.

