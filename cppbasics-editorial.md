<img src="https://r2cdn.perplexity.ai/pplx-full-logo-primary-dark%402x.png" style="height:64px;margin-right:32px"/>

# no not like that dont keep subsection wise i want single page editorial

<img src="https://r2cdn.perplexity.ai/pplx-full-logo-primary-dark%402x.png" style="height:64px;margin-right:32px"/>

# C++ Basics - Complete Programming Guide

C++ is a powerful, high-performance programming language that extends C with object-oriented programming capabilities, making it essential for system programming, game development, and competitive programming. This comprehensive guide covers fundamental concepts including syntax, data types, operators, and conditional statements.

## Algorithm Explanation

Learning C++ basics involves understanding core programming concepts in a structured manner:

1. Start with basic syntax and program structure
2. Learn fundamental data types and variable declarations
3. Master input/output operations for user interaction
4. Understand different types of operators for calculations and comparisons
5. Implement conditional statements for decision-making logic
6. Practice combining all concepts in practical applications

## Implementation
Learning C++ basics involves understanding core programming concepts in a structured manner:

1. Start with basic syntax and program structure
2. Learn fundamental data types and variable declarations
3. Master input/output operations for user interaction
4. Understand different types of operators for calculations and comparisons
5. Implement conditional statements for decision-making logic
6. Practice combining all concepts in practical applications
### Basic Syntax and Hello World

```cpp
#include <iostream>
using namespace std;

int main() {
    cout << "Hello, World!" << endl;
    return 0;
}
```

```java
public class HelloWorld {
    public static void main(String[] args) {
        System.out.println("Hello, World!");
    }
}
```

```python
print("Hello, World!")
```


### Data Types and Variables

```cpp
#include <iostream>
#include <string>
using namespace std;

int main() {
    // Integer types
    int age = 25;
    long population = 1234567890L;
    long long bigNumber = 123456789012345LL;
    
    // Floating point types
    float price = 19.99f;
    double pi = 3.14159265359;
    
    // Character and string types
    char grade = 'A';
    string name = "John Doe";
    
    // Boolean type
    bool isActive = true;
    
    cout << "Age: " << age << endl;
    cout << "Name: " << name << endl;
    cout << "Grade: " << grade << endl;
    cout << "Active: " << isActive << endl;
    
    return 0;
}
```

```java
public class DataTypes {
    public static void main(String[] args) {
        // Integer types
        int age = 25;
        long population = 1234567890L;
        
        // Floating point types
        float price = 19.99f;
        double pi = 3.14159265359;
        
        // Character and string types
        char grade = 'A';
        String name = "John Doe";
        
        // Boolean type
        boolean isActive = true;
        
        System.out.println("Age: " + age);
        System.out.println("Name: " + name);
        System.out.println("Grade: " + grade);
        System.out.println("Active: " + isActive);
    }
}
```

```python
# Python is dynamically typed
age = 25
population = 1234567890
price = 19.99
pi = 3.14159265359
grade = 'A'
name = "John Doe"
is_active = True

print(f"Age: {age}")
print(f"Name: {name}")
print(f"Grade: {grade}")
print(f"Active: {is_active}")
```


### Input and Output Operations

```cpp
#include <iostream>
#include <string>
using namespace std;

int main() {
    string firstName, fullName;
    int age;
    
    cout << "Enter your first name: ";
    cin >> firstName;
    
    cout << "Enter your age: ";
    cin >> age;
    
    // Clear the input buffer
    cin.ignore();
    
    cout << "Enter your full name: ";
    getline(cin, fullName);
    
    cout << "\nHello " << firstName << "!" << endl;
    cout << "You are " << age << " years old." << endl;
    cout << "Full name: " << fullName << endl;
    
    return 0;
}
```

```java
import java.util.Scanner;

public class InputOutput {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        
        System.out.print("Enter your first name: ");
        String firstName = scanner.next();
        
        System.out.print("Enter your age: ");
        int age = scanner.nextInt();
        
        // Clear the buffer
        scanner.nextLine();
        
        System.out.print("Enter your full name: ");
        String fullName = scanner.nextLine();
        
        System.out.println("\nHello " + firstName + "!");
        System.out.println("You are " + age + " years old.");
        System.out.println("Full name: " + fullName);
        
        scanner.close();
    }
}
```

```python
first_name = input("Enter your first name: ")
age = int(input("Enter your age: "))
full_name = input("Enter your full name: ")

print(f"\nHello {first_name}!")
print(f"You are {age} years old.")
print(f"Full name: {full_name}")
```


### Operators and Mathematical Operations

```cpp
#include <iostream>
using namespace std;

int main() {
    int a = 15, b = 4;
    
    cout << "Arithmetic Operations:" << endl;
    cout << "a + b = " << (a + b) << endl;
    cout << "a - b = " << (a - b) << endl;
    cout << "a * b = " << (a * b) << endl;
    cout << "a / b = " << (a / b) << endl;
    cout << "a % b = " << (a % b) << endl;
    
    // Relational operations
    cout << "\nRelational Operations:" << endl;
    cout << "a > b: " << (a > b) << endl;
    cout << "a < b: " << (a < b) << endl;
    cout << "a == b: " << (a == b) << endl;
    cout << "a != b: " << (a != b) << endl;
    
    // Logical operations
    bool x = true, y = false;
    cout << "\nLogical Operations:" << endl;
    cout << "x && y: " << (x && y) << endl;
    cout << "x || y: " << (x || y) << endl;
    cout << "!x: " << (!x) << endl;
    
    // Assignment operations
    int c = 10;
    cout << "\nAssignment Operations:" << endl;
    cout << "Initial c: " << c << endl;
    c += 5;  // c = c + 5
    cout << "After c += 5: " << c << endl;
    c *= 2;  // c = c * 2
    cout << "After c *= 2: " << c << endl;
    
    return 0;
}
```

```java
public class Operators {
    public static void main(String[] args) {
        int a = 15, b = 4;
        
        System.out.println("Arithmetic Operations:");
        System.out.println("a + b = " + (a + b));
        System.out.println("a - b = " + (a - b));
        System.out.println("a * b = " + (a * b));
        System.out.println("a / b = " + (a / b));
        System.out.println("a % b = " + (a % b));
        
        // Relational operations
        System.out.println("\nRelational Operations:");
        System.out.println("a > b: " + (a > b));
        System.out.println("a < b: " + (a < b));
        System.out.println("a == b: " + (a == b));
        System.out.println("a != b: " + (a != b));
        
        // Logical operations
        boolean x = true, y = false;
        System.out.println("\nLogical Operations:");
        System.out.println("x && y: " + (x && y));
        System.out.println("x || y: " + (x || y));
        System.out.println("!x: " + (!x));
        
        // Assignment operations
        int c = 10;
        System.out.println("\nAssignment Operations:");
        System.out.println("Initial c: " + c);
        c += 5;  // c = c + 5
        System.out.println("After c += 5: " + c);
        c *= 2;  // c = c * 2
        System.out.println("After c *= 2: " + c);
    }
}
```

```python
a, b = 15, 4

print("Arithmetic Operations:")
print(f"a + b = {a + b}")
print(f"a - b = {a - b}")
print(f"a * b = {a * b}")
print(f"a / b = {a / b}")
print(f"a % b = {a % b}")

# Relational operations
print("\nRelational Operations:")
print(f"a > b: {a > b}")
print(f"a < b: {a < b}")
print(f"a == b: {a == b}")
print(f"a != b: {a != b}")

# Logical operations
x, y = True, False
print("\nLogical Operations:")
print(f"x and y: {x and y}")
print(f"x or y: {x or y}")
print(f"not x: {not x}")

# Assignment operations
c = 10
print("\nAssignment Operations:")
print(f"Initial c: {c}")
c += 5  # c = c + 5
print(f"After c += 5: {c}")
c *= 2  # c = c * 2
print(f"After c *= 2: {c}")
```


### Conditional Statements and Decision Making

```cpp
#include <iostream>
using namespace std;

int main() {
    int score, choice;
    cout << "Enter your score (0-100): ";
    cin >> score;
    
    // if-else-if ladder for grade calculation
    if (score >= 90) {
        cout << "Grade: A+" << endl;
    } else if (score >= 80) {
        cout << "Grade: A" << endl;
    } else if (score >= 70) {
        cout << "Grade: B" << endl;
    } else if (score >= 60) {
        cout << "Grade: C" << endl;
    } else if (score >= 50) {
        cout << "Grade: D" << endl;
    } else {
        cout << "Grade: F" << endl;
    }
    
    // Nested if-else example
    int age;
    bool hasLicense;
    cout << "\nEnter your age: ";
    cin >> age;
    
    if (age >= 18) {
        cout << "Do you have a driving license? (1 for yes, 0 for no): ";
        cin >> hasLicense;
        
        if (hasLicense) {
            cout << "You are eligible to drive!" << endl;
        } else {
            cout << "You need to get a driving license first." << endl;
        }
    } else {
        cout << "You are not old enough to drive." << endl;
    }
    
    // Switch statement example
    cout << "\nSelect operation (1-4): ";
    cout << "\n1. Addition\n2. Subtraction\n3. Multiplication\n4. Division\n";
    cin >> choice;
    
    switch (choice) {
        case 1:
            cout << "Addition selected" << endl;
            break;
        case 2:
            cout << "Subtraction selected" << endl;
            break;
        case 3:
            cout << "Multiplication selected" << endl;
            break;
        case 4:
            cout << "Division selected" << endl;
            break;
        default:
            cout << "Invalid choice" << endl;
    }
    
    return 0;
}
```

```java
import java.util.Scanner;

public class ConditionalStatements {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        
        System.out.print("Enter your score (0-100): ");
        int score = scanner.nextInt();
        
        // if-else-if ladder for grade calculation
        if (score >= 90) {
            System.out.println("Grade: A+");
        } else if (score >= 80) {
            System.out.println("Grade: A");
        } else if (score >= 70) {
            System.out.println("Grade: B");
        } else if (score >= 60) {
            System.out.println("Grade: C");
        } else if (score >= 50) {
            System.out.println("Grade: D");
        } else {
            System.out.println("Grade: F");
        }
        
        // Nested if-else example
        System.out.print("\nEnter your age: ");
        int age = scanner.nextInt();
        
        if (age >= 18) {
            System.out.print("Do you have a driving license? (true/false): ");
            boolean hasLicense = scanner.nextBoolean();
            
            if (hasLicense) {
                System.out.println("You are eligible to drive!");
            } else {
                System.out.println("You need to get a driving license first.");
            }
        } else {
            System.out.println("You are not old enough to drive.");
        }
        
        // Switch statement example
        System.out.println("\nSelect operation (1-4):");
        System.out.println("1. Addition\n2. Subtraction\n3. Multiplication\n4. Division");
        int choice = scanner.nextInt();
        
        switch (choice) {
            case 1:
                System.out.println("Addition selected");
                break;
            case 2:
                System.out.println("Subtraction selected");
                break;
            case 3:
                System.out.println("Multiplication selected");
                break;
            case 4:
                System.out.println("Division selected");
                break;
            default:
                System.out.println("Invalid choice");
        }
        
        scanner.close();
    }
}
```

```python
score = int(input("Enter your score (0-100): "))

# if-elif-else ladder for grade calculation
if score >= 90:
    print("Grade: A+")
elif score >= 80:
    print("Grade: A")
elif score >= 70:
    print("Grade: B")
elif score >= 60:
    print("Grade: C")
elif score >= 50:
    print("Grade: D")
else:
    print("Grade: F")

# Nested if-else example
age = int(input("\nEnter your age: "))

if age >= 18:
    has_license = input("Do you have a driving license? (yes/no): ").lower() == 'yes'
    
    if has_license:
        print("You are eligible to drive!")
    else:
        print("You need to get a driving license first.")
else:
    print("You are not old enough to drive.")

# Switch-like statement using dictionary
print("\nSelect operation (1-4):")
print("1. Addition\n2. Subtraction\n3. Multiplication\n4. Division")
choice = int(input())

operations = {
    1: "Addition selected",
    2: "Subtraction selected", 
    3: "Multiplication selected",
    4: "Division selected"
}

print(operations.get(choice, "Invalid choice"))
```


### Complete Calculator Application

```cpp
#include <iostream>
#include <string>
using namespace std;

int main() {
    string userName;
    int num1, num2, choice;
    char continueChoice;
    
    cout << "=== Welcome to C++ Calculator ===" << endl;
    cout << "Enter your name: ";
    getline(cin, userName);
    
    do {
        cout << "\nHello " << userName << "!" << endl;
        cout << "Enter first number: ";
        cin >> num1;
        cout << "Enter second number: ";
        cin >> num2;
        
        cout << "\nSelect operation:" << endl;
        cout << "1. Addition (+)" << endl;
        cout << "2. Subtraction (-)" << endl;
        cout << "3. Multiplication (*)" << endl;
        cout << "4. Division (/)" << endl;
        cout << "5. Modulus (%)" << endl;
        cout << "Enter your choice (1-5): ";
        cin >> choice;
        
        int result;
        bool validOperation = true;
        
        switch (choice) {
            case 1:
                result = num1 + num2;
                cout << num1 << " + " << num2 << " = " << result << endl;
                break;
            case 2:
                result = num1 - num2;
                cout << num1 << " - " << num2 << " = " << result << endl;
                break;
            case 3:
                result = num1 * num2;
                cout << num1 << " * " << num2 << " = " << result << endl;
                break;
            case 4:
                if (num2 != 0) {
                    result = num1 / num2;
                    cout << num1 << " / " << num2 << " = " << result << endl;
                } else {
                    cout << "Error: Division by zero!" << endl;
                    validOperation = false;
                }
                break;
            case 5:
                if (num2 != 0) {
                    result = num1 % num2;
                    cout << num1 << " % " << num2 << " = " << result << endl;
                } else {
                    cout << "Error: Modulus by zero!" << endl;
                    validOperation = false;
                }
                break;
            default:
                cout << "Invalid choice!" << endl;
                validOperation = false;
        }
        
        if (validOperation && choice >= 1 && choice <= 5) {
            if (result > 0) {
                cout << "Result is positive." << endl;
            } else if (result < 0) {
                cout << "Result is negative." << endl;
            } else {
                cout << "Result is zero." << endl;
            }
        }
        
        cout << "\nDo you want to perform another calculation? (y/n): ";
        cin >> continueChoice;
        
    } while (continueChoice == 'y' || continueChoice == 'Y');
    
    cout << "Thank you for using the calculator, " << userName << "!" << endl;
    return 0;
}
```

```java
import java.util.Scanner;

public class Calculator {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        String userName;
        int num1, num2, choice;
        char continueChoice;
        
        System.out.println("=== Welcome to Java Calculator ===");
        System.out.print("Enter your name: ");
        userName = scanner.nextLine();
        
        do {
            System.out.println("\nHello " + userName + "!");
            System.out.print("Enter first number: ");
            num1 = scanner.nextInt();
            System.out.print("Enter second number: ");
            num2 = scanner.nextInt();
            
            System.out.println("\nSelect operation:");
            System.out.println("1. Addition (+)");
            System.out.println("2. Subtraction (-)");
            System.out.println("3. Multiplication (*)");
            System.out.println("4. Division (/)");
            System.out.println("5. Modulus (%)");
            System.out.print("Enter your choice (1-5): ");
            choice = scanner.nextInt();
            
            int result = 0;
            boolean validOperation = true;
            
            switch (choice) {
                case 1:
                    result = num1 + num2;
                    System.out.println(num1 + " + " + num2 + " = " + result);
                    break;
                case 2:
                    result = num1 - num2;
                    System.out.println(num1 + " - " + num2 + " = " + result);
                    break;
                case 3:
                    result = num1 * num2;
                    System.out.println(num1 + " * " + num2 + " = " + result);
                    break;
                case 4:
                    if (num2 != 0) {
                        result = num1 / num2;
                        System.out.println(num1 + " / " + num2 + " = " + result);
                    } else {
                        System.out.println("Error: Division by zero!");
                        validOperation = false;
                    }
                    break;
                case 5:
                    if (num2 != 0) {
                        result = num1 % num2;
                        System.out.println(num1 + " % " + num2 + " = " + result);
                    } else {
                        System.out.println("Error: Modulus by zero!");
                        validOperation = false;
                    }
                    break;
                default:
                    System.out.println("Invalid choice!");
                    validOperation = false;
            }
            
            if (validOperation && choice >= 1 && choice <= 5) {
                if (result > 0) {
                    System.out.println("Result is positive.");
                } else if (result < 0) {
                    System.out.println("Result is negative.");
                } else {
                    System.out.println("Result is zero.");
                }
            }
            
            System.out.print("\nDo you want to perform another calculation? (y/n): ");
            continueChoice = scanner.next().charAt(0);
            
        } while (continueChoice == 'y' || continueChoice == 'Y');
        
        System.out.println("Thank you for using the calculator, " + userName + "!");
        scanner.close();
    }
}
```

```python
def main():
    print("=== Welcome to Python Calculator ===")
    user_name = input("Enter your name: ")
    
    while True:
        print(f"\nHello {user_name}!")
        num1 = int(input("Enter first number: "))
        num2 = int(input("Enter second number: "))
        
        print("\nSelect operation:")
        print("1. Addition (+)")
        print("2. Subtraction (-)")
        print("3. Multiplication (*)")
        print("4. Division (/)")
        print("5. Modulus (%)")
        
        choice = int(input("Enter your choice (1-5): "))
        
        valid_operation = True
        result = 0
        
        if choice == 1:
            result = num1 + num2
            print(f"{num1} + {num2} = {result}")
        elif choice == 2:
            result = num1 - num2
            print(f"{num1} - {num2} = {result}")
        elif choice == 3:
            result = num1 * num2
            print(f"{num1} * {num2} = {result}")
        elif choice == 4:
            if num2 != 0:
                result = num1 // num2  # Integer division
                print(f"{num1} / {num2} = {result}")
            else:
                print("Error: Division by zero!")
                valid_operation = False
        elif choice == 5:
            if num2 != 0:
                result = num1 % num2
                print(f"{num1} % {num2} = {result}")
            else:
                print("Error: Modulus by zero!")
                valid_operation = False
        else:
            print("Invalid choice!")
            valid_operation = False
        
        if valid_operation and 1 <= choice <= 5:
            if result > 0:
                print("Result is positive.")
            elif result < 0:
                print("Result is negative.")
            else:
                print("Result is zero.")
        
        continue_choice = input("\nDo you want to perform another calculation? (y/n): ")
        if continue_choice.lower() != 'y':
            break
    
    print(f"Thank you for using the calculator, {user_name}!")

if __name__ == "__main__":
    main()
```


### Time Complexity

O(1) for all basic operations - variable declaration, arithmetic operations, input/output, and conditional statements execute in constant time.

### Space Complexity

O(1) - All examples use constant space regardless of input size, storing only a fixed number of variables.

Special thanks to the C++ community for contributing to programming education and making these fundamental concepts accessible to learners worldwide.

