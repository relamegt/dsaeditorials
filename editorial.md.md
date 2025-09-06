<img src="https://r2cdn.perplexity.ai/pplx-full-logo-primary-dark%402x.png" style="height:64px;margin-right:32px"/>

# Linear Search Algorithm: Complete Guide

Linear search is one of the most fundamental searching algorithms that **sequentially examines** each element in a collection until the target is found or all elements have been checked. This comprehensive guide covers all approaches from brute force to optimized implementations across multiple programming languages.[^1]

## Algorithm Approaches

### 1. Brute Force Approach (Basic)

The most **straightforward implementation** that checks every element from start to finish.[^2]

**Algorithm Steps:**

1. Start from the first element of the array[^2]
2. Compare the current element with the target value
3. If they match, return the index
4. If they don't match, move to the next element
5. Repeat until found or end of array is reached
6. Return -1 if element is not found[^3]

#### Code Implementations:

**C++:**

```cpp
class Solution {
public:
    int linearSearch(vector<int>& nums, int target) {
        for (int i = 0; i < nums.size(); i++) {
            if (nums[i] == target) {
                return i;
            }
        }
        return -1;
    }
};
```

**Java:**

```java
public class LinearSearch {
    public static int linearSearch(int[] array, int target) {
        for (int i = 0; i < array.length; i++) {
            if (array[i] == target) {
                return i;
            }
        }
        return -1;
    }
}
```

**Python:**

```python
def linear_search(arr, target):
    for i in range(len(arr)):
        if arr[i] == target:
            return i
    return -1
```

**JavaScript:**

```javascript
function linearSearch(arr, target) {
    for (let i = 0; i < arr.length; i++) {
        if (arr[i] === target) {
            return i;
        }
    }
    return -1;
}
```


### 2. Better Approach (Sentinel Linear Search)

This approach **eliminates the boundary check** in each iteration by placing the target element at the end of the array, reducing the number of comparisons.[^4]

**Algorithm Steps:**

1. Store the last element temporarily
2. Place the target at the end of the array
3. Start searching from the beginning
4. When target is found, check if it's at the original position or the sentinel position
5. Restore the original last element

#### Code Implementations:

**C++:**

```cpp
class Solution {
public:
    int sentinelSearch(vector<int>& nums, int target) {
        int n = nums.size();
        if (n == 0) return -1;
        
        int last = nums[n-1];
        nums[n-1] = target;
        
        int i = 0;
        while (nums[i] != target) {
            i++;
        }
        
        nums[n-1] = last;
        
        if (i < n-1 || nums[n-1] == target) {
            return i;
        }
        return -1;
    }
};
```

**Python:**

```python
def sentinel_search(arr, target):
    n = len(arr)
    if n == 0:
        return -1
    
    last = arr[n-1]
    arr[n-1] = target
    
    i = 0
    while arr[i] != target:
        i += 1
    
    arr[n-1] = last
    
    if i < n-1 or arr[n-1] == target:
        return i
    return -1
```


### 3. Optimal Approach (Two-Way Linear Search)

The **most optimized version** searches from both ends simultaneously, potentially reducing search time by half.[^1]

**Algorithm Steps:**

1. Initialize two pointers: left at start, right at end
2. Compare elements at both positions with target
3. If found at either position, return the index
4. Move left pointer forward and right pointer backward
5. Continue until pointers meet or target is found

#### Code Implementations:

**C++:**

```cpp
class Solution {
public:
    int twoWaySearch(vector<int>& nums, int target) {
        int left = 0, right = nums.size() - 1;
        
        while (left <= right) {
            if (nums[left] == target) return left;
            if (nums[right] == target) return right;
            
            left++;
            right--;
        }
        return -1;
    }
};
```

**Java:**

```java
public class TwoWayLinearSearch {
    public static int twoWaySearch(int[] array, int target) {
        int left = 0, right = array.length - 1;
        
        while (left <= right) {
            if (array[left] == target) return left;
            if (array[right] == target) return right;
            
            left++;
            right--;
        }
        return -1;
    }
}
```

**Python:**

```python
def two_way_search(arr, target):
    left, right = 0, len(arr) - 1
    
    while left <= right:
        if arr[left] == target:
            return left
        if arr[right] == target:
            return right
        
        left += 1
        right -= 1
    
    return -1
```

**C:**

```c
#include <stdio.h>

int twoWaySearch(int arr[], int n, int target) {
    int left = 0, right = n - 1;
    
    while (left <= right) {
        if (arr[left] == target) return left;
        if (arr[right] == target) return right;
        
        left++;
        right--;
    }
    return -1;
}
```


## Additional Optimizations

### Move to Front Optimization

For **frequently searched elements**, move the found element to the front of the array to improve future search performance.[^4]

```cpp
int moveToFrontSearch(vector<int>& nums, int target) {
    for (int i = 0; i < nums.size(); i++) {
        if (nums[i] == target) {
            // Move element to front
            if (i > 0) {
                swap(nums[^0], nums[i]);
                return 0;
            }
            return i;
        }
    }
    return -1;
}
```


### Transposition Optimization

**Swap the found element** with its predecessor to gradually improve search performance for frequently accessed items.[^4]

```cpp
int transpositionSearch(vector<int>& nums, int target) {
    for (int i = 0; i < nums.size(); i++) {
        if (nums[i] == target) {
            // Swap with previous element
            if (i > 0) {
                swap(nums[i-1], nums[i]);
                return i-1;
            }
            return i;
        }
    }
    return -1;
}
```


## Complexity Analysis

### Time Complexity

| Case | Basic Linear Search | Two-Way Search |
| :-- | :-- | :-- |
| **Best Case** | O(1)[^5] | O(1) |
| **Average Case** | O(n)[^5] | O(n/2) |
| **Worst Case** | O(n)[^5] | O(n/2) |

### Space Complexity

All linear search approaches have **O(1) space complexity** as they use only a constant amount of extra space.[^5]

## When to Use Linear Search

Linear search is **most effective** when:[^5]

- Working with small datasets
- Array is unsorted
- Need to search only once or infrequently
- Memory constraints require simple implementation
- Elements are stored in a linked list


## Complete Working Example

```cpp
#include <iostream>
#include <vector>
using namespace std;

class LinearSearchImplementations {
public:
    // Basic Linear Search
    static int basicSearch(vector<int>& nums, int target) {
        for (int i = 0; i < nums.size(); i++) {
            if (nums[i] == target) return i;
        }
        return -1;
    }
    
    // Two-Way Linear Search
    static int twoWaySearch(vector<int>& nums, int target) {
        int left = 0, right = nums.size() - 1;
        while (left <= right) {
            if (nums[left] == target) return left;
            if (nums[right] == target) return right;
            left++;
            right--;
        }
        return -1;
    }
};

int main() {
    vector<int> nums = {2, 4, 0, 1, 9, 7, 3};
    int target = 9;
    
    cout << "Basic Search: " << LinearSearchImplementations::basicSearch(nums, target) << endl;
    cout << "Two-Way Search: " << LinearSearchImplementations::twoWaySearch(nums, target) << endl;
    
    return 0;
}
```

The **two-way linear search** represents the optimal approach for unsorted arrays, offering improved average-case performance while maintaining the simplicity and reliability of the basic linear search algorithm.[^1][^4]
