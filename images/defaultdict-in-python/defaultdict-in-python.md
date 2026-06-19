# Defaultdict in Python

## Introduction

`defaultdict` is a subclass of Python's built-in dictionary available in the `collections` module. It automatically provides a default value when a missing key is accessed, eliminating the need to check whether a key exists before using it.

Unlike a normal dictionary, a `defaultdict` does not raise a `KeyError` for missing keys if a default factory is provided.

### Key Features

- Automatically creates missing keys.
- Avoids `KeyError`.
- Simplifies counting and grouping operations.
- Supports various default types.
- Reduces repetitive code.
- Inherits all dictionary functionality.

# Why Use defaultdict?

A normal dictionary raises a `KeyError` when a non-existing key is accessed. `defaultdict` automatically creates a default value, making programs simpler and easier to maintain.

### Applications

- Counting frequencies.
- Grouping elements.
- Graph representation.
- Caching.
- Text processing.
- Data aggregation.

# Syntax

```python
from collections import defaultdict

data = defaultdict(default_factory)
```

### Parameters

- `default_factory`: A callable such as `int`, `list`, `set`, `str`, or a custom function.

### Return Value

Returns a dictionary-like object that automatically creates default values for missing keys.

# Creating a defaultdict

### Example

```python
from collections import defaultdict

skills = defaultdict(list)

skills["Akash Dangudubiyyapu"].append("Python")
skills["Mohit Chandaluri"].append("Java")

print(skills)
print(skills["Abhiram Gopisetti"])
```

### Output
defaultdict(<class 'list'>, {'Akash Dangudubiyyapu': ['Python'], 'Mohit Chandaluri': ['Java']})
[]

### Explanation

A missing key automatically receives an empty list instead of raising an error.

# Why defaultdict is Useful

### Normal Dictionary

```python
marks = {}

marks["Akhil"] += 1
```

### Output
KeyError

### Using defaultdict

```python
from collections import defaultdict

marks = defaultdict(int)

marks["Akhil"] += 1

print(marks)
```

### Output
defaultdict(<class 'int'>, {'Akhil': 1})

### Explanation

Since `int()` returns 0, the missing key starts with zero automatically.

# Using List as Default Factory

### Example

```python
from collections import defaultdict

projects = defaultdict(list)

projects["Akash Dangudubiyyapu"].append("AlphaKnowledge")
projects["Mohit Chandaluri"].append("Portfolio")

print(projects)
```

### Output
defaultdict(<class 'list'>, {'Akash Dangudubiyyapu': ['AlphaKnowledge'], 'Mohit Chandaluri': ['Portfolio']})

### Explanation

Every missing key automatically starts with an empty list.

# Using int as Default Factory

### Example

```python
from collections import defaultdict

counter = defaultdict(int)

numbers = [1, 2, 1, 3, 2, 1]

for value in numbers:
    counter[value] += 1

print(counter)
```

### Output
defaultdict(<class 'int'>, {1: 3, 2: 2, 3: 1})

### Explanation

The integer default value is 0, which makes counting easy.

# Using str as Default Factory

### Example

```python
from collections import defaultdict

messages = defaultdict(str)

messages["welcome"] = "Hello AlphaKnowledge"

print(messages)
print(messages["new"])
```

### Output
defaultdict(<class 'str'>, {'welcome': 'Hello AlphaKnowledge'})
''

### Explanation

Missing keys automatically receive an empty string.

# Using set as Default Factory

### Example

```python
from collections import defaultdict

courses = defaultdict(set)

courses["Akash Dangudubiyyapu"].add("Python")
courses["Akash Dangudubiyyapu"].add("Python")
courses["Akash Dangudubiyyapu"].add("Java")

print(courses)
```

### Output
defaultdict(<class 'set'>, {'Akash Dangudubiyyapu': {'Python', 'Java'}})

### Explanation

Duplicate values are removed automatically because sets store unique elements.

# Grouping Items

### Example

```python
from collections import defaultdict

names = [
    "Akash Dangudubiyyapu",
    "Akhil",
    "Abhiram Gopisetti",
    "Mohit Chandaluri",
    "Hemanth"
]

grouped = defaultdict(list)

for name in names:
    grouped[name[0]].append(name)

print(grouped)
```

### Output
defaultdict(<class 'list'>, {'A': ['Akash Dangudubiyyapu', 'Akhil', 'Abhiram Gopisetti'], 'M': ['Mohit Chandaluri'], 'H': ['Hemanth']})

### Explanation

Names are grouped based on their first letter.

# Using Custom Default Values

### Example

```python
from collections import defaultdict

data = defaultdict(lambda: "Not Available")

data["Python"] = "Programming"

print(data["Python"])
print(data["Java"])
```

### Output
Programming
Not Available

### Explanation

The lambda function provides a custom default value.

# Accessing Missing Keys

### Example

```python
from collections import defaultdict

languages = defaultdict(lambda: "Unknown")

print(languages["C++"])
```

### Output
Unknown

### Explanation

The missing key automatically receives the value returned by the lambda function.

# Common Default Factories

| Factory | Default Value |
| --- | --- |
| `int` | 0 |
| `float` | 0.0 |
| `str` | "" |
| `list` | [] |
| `set` | set() |
| `dict` | {} |

# defaultdict vs Dictionary

| Feature | Dictionary | defaultdict |
| --- | --- | --- |
| Missing key raises error | Yes | No |
| Automatic default values | No | Yes |
| Supports grouping easily | No | Yes |
| Frequency counting | Requires checks | Simple |
| Built-in class | dict | collections.defaultdict |

# Advantages of defaultdict

1. Prevents KeyError.
2. Simplifies code.
3. Useful for counting and grouping.
4. Reduces conditional checks.
5. Supports custom default values.

# Limitations of defaultdict

1. Slightly higher memory usage.
2. May create unwanted keys accidentally.
3. Requires importing from collections.

# Applications of defaultdict

- Frequency counting.
- Word grouping.
- Graph adjacency lists.
- Caching.
- Data aggregation.
- Text analysis.
- Student records.

# Summary

`defaultdict` is a dictionary subclass from the `collections` module that automatically creates default values for missing keys. It simplifies counting, grouping, and data processing tasks by eliminating manual checks for key existence and reducing the chances of encountering `KeyError`.

