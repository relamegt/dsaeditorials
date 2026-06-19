# Global and Local Variables in Python

## Introduction

Variables are used to store data in memory, while scope determines where those variables can be accessed within a program. Depending on where a variable is created, it may have local scope or global scope.

A **local variable** is created inside a function and can only be accessed within that function. A **global variable** is created outside all functions and can be accessed throughout the program. Understanding variable scope helps avoid naming conflicts and improves program organization.

### Key Features

- Local variables exist only inside functions.
- Global variables are accessible throughout the program.
- Local variables shadow global variables with the same name.
- Global variables can be modified using the `global` keyword.
- Variables are automatically destroyed when their scope ends.
- Scope improves code organization and readability.

# Why Variable Scope?

Variable scope controls where variables can be accessed and prevents unintended changes to data.

### Example Without Proper Scope

```python
name = "Akash"

def display():
    name = "Abhiram"

display()

print(name)
```

### Output
Akash

### Limitation

The variable inside the function does not affect the global variable because it creates a separate local variable.

# Local Variables

Local variables are created inside a function and exist only during its execution.

### Example

```python
def greet():

    message = "Welcome to AlphaKnowledge"

    print(message)

greet()
```

### Output
Welcome to AlphaKnowledge

### Explanation

The variable `message` exists only inside the `greet()` function.

# Accessing Local Variables Outside a Function

Local variables cannot be accessed outside their function.

### Example

```python
def greet():

    msg = "Hello"

greet()

print(msg)
```

### Output
NameError: name 'msg' is not defined

### Explanation

The variable `msg` is destroyed after the function finishes execution.

# Global Variables

Global variables are declared outside functions and are accessible throughout the program.

### Example

```python
course = "Python Programming"

def display():

    print(course)

display()

print(course)
```

### Output
Python Programming
Python Programming

### Explanation

The variable `course` belongs to the global scope and can be accessed inside and outside functions.

# Global Variable Lookup

If Python cannot find a variable inside a function, it automatically searches the global scope.

### Example

```python
city = "Hyderabad"

def show():

    print(city)

show()
```

### Output
Hyderabad

### Explanation

Since `city` is not defined locally, Python uses the global variable.

# Local Variable Shadows Global Variable

A local variable with the same name as a global variable hides the global variable inside the function.

### Example

```python
name = "Akash"

def demo():

    name = "Abhiram"

    print(name)

demo()

print(name)
```

### Output
Abhiram
Akash

### Explanation

The local variable takes precedence inside the function, while the global variable remains unchanged.

# Modifying Global Variables Without global Keyword

Trying to modify a global variable inside a function without using `global` causes an error.

### Example

```python
count = 10

def increase():

    count += 1

increase()
```

### Output
UnboundLocalError: local variable 'count' referenced before assignment

### Explanation

Python assumes `count` is local because it is modified inside the function.

# Using global Keyword

The `global` keyword allows functions to modify global variables.

### Example

```python
count = 10

def increase():

    global count

    count += 1

increase()

print(count)
```

### Output
11

### Explanation

The `global` keyword tells Python to use the variable from global scope.

# Global and Local Variables with Same Name

### Example

```python
a = 100

def test():

    a = 200

    print("Inside function:", a)

test()

print("Outside function:", a)
```

### Output
Inside function: 200
Outside function: 100

### Explanation

The local variable hides the global variable inside the function.

# Multiple Functions Sharing Global Variables

Global variables can be accessed by multiple functions.

### Example

```python
message = "Hello"

def first():

    print(message)

def second():

    print(message)

first()
second()
```

### Output
Hello
Hello

### Explanation

Both functions access the same global variable.

# Lifetime of Variables

The lifetime of a local variable is limited to the execution of its function, while a global variable exists until the program terminates.

### Example

```python
x = 50

def demo():

    y = 20

    print(y)

demo()

print(x)
```

### Output
20
50

### Explanation

The variable `y` exists only during the execution of `demo()`, whereas `x` exists throughout the program.

# globals() Function

The `globals()` function returns a dictionary containing all global variables.

### Example

```python
language = "Python"

print(globals()["language"])
```

### Output
Python

### Explanation

The global namespace is stored internally as a dictionary.

# locals() Function

The `locals()` function returns a dictionary containing local variables.

### Example

```python
def demo():

    age = 22

    print(locals())

demo()
```

### Output
{'age': 22}

### Explanation

The dictionary contains all variables defined inside the function.

# Global Variables vs Local Variables

| Feature | Global Variables | Local Variables |
| --- | --- | --- |
| Declaration | Outside functions | Inside functions |
| Scope | Entire program | Specific function |
| Lifetime | Until program ends | Until function ends |
| Accessibility | Anywhere | Inside function only |
| Sharing | Shared among functions | Not shared |
| Memory | Global namespace | Local namespace |
| Modification | Using `global` keyword | Directly |

# Advantages of Local Variables

1. Reduce naming conflicts.
2. Improve program security.
3. Minimize accidental modifications.
4. Provide better memory management.
5. Make functions independent and reusable.

# Advantages of Global Variables

1. Allow data sharing between functions.
2. Reduce parameter passing.
3. Store constants and configuration values.
4. Improve accessibility throughout the program.

# Limitations

1. Excessive global variables can make debugging difficult.
2. Local variables cannot be accessed outside functions.
3. Global variables may accidentally change program behavior.
4. Variable shadowing can create confusion.

# Summary

Variables in Python are categorized according to their scope. Local variables are created inside functions and are accessible only within those functions, whereas global variables are declared outside functions and can be accessed throughout the program. When a local and global variable share the same name, the local variable takes precedence inside the function. The `global` keyword allows functions to modify global variables. Understanding local and global scope is essential for writing organized, maintainable, and error-free Python programs.

