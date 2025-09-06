<img src="https://r2cdn.perplexity.ai/pplx-full-logo-primary-dark%402x.png" style="height:64px;margin-right:32px"/>

# Linear Search Algorithm

Linear search is one of the simplest searching algorithms that sequentially checks each element in a collection until the target element is found or the entire collection has been searched.

## Brute Force Approach

The most straightforward approach to implement linear search is to traverse the entire array from beginning to end, comparing each element with the target value.

### Algorithm Explanation

1. Start from the first element of the array
2. Compare the current element with the target value
3. If they match, return the index
4. If they don't match, move to the next element
5. Repeat until found or end of array is reached
6. Return -1 if element is not found

### Implementation

**C++:**

```cpp
class Solution {
public:
    int search(vector<int>& nums, int target) {
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
class Solution {
    public int search(int[] nums, int target) {
        for (int i = 0; i < nums.length; i++) {
            if (nums[i] == target) {
                return i;
            }
        }
        return -1;
    }
}
```

**Python:**

```python
class Solution:
    def search(self, nums, target):
        for i in range(len(nums)):
            if nums[i] == target:
                return i
        return -1
```

**JavaScript:**

```javascript
class Solution {
    search(nums, target) {
        for (let i = 0; i < nums.length; i++) {
            if (nums[i] === target) {
                return i;
            }
        }
        return -1;
    }
}
```

**C:**

```c
int search(int* nums, int numsSize, int target) {
    for (int i = 0; i < numsSize; i++) {
        if (nums[i] == target) {
            return i;
        }
    }
    return -1;
}
```


## Better Approach (Sentinel Linear Search)

This approach eliminates the boundary check in each iteration by placing the target element at the end of the array as a sentinel, reducing the number of comparisons per iteration.[^1]

### Algorithm Explanation

1. Store the last element of the array temporarily
2. Place the target value at the end of the array (sentinel)
3. Start searching from the beginning without boundary checks
4. When target is found, check if it's at the original position or sentinel position
5. Restore the original last element
6. Return appropriate index or -1 if not found

### Implementation

**C++:**

```cpp
class Solution {
public:
    int search(vector<int>& nums, int target) {
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

**Java:**

```java
class Solution {
    public int search(int[] nums, int target) {
        int n = nums.length;
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
}
```

**Python:**

```python
class Solution:
    def search(self, nums, target):
        n = len(nums)
        if n == 0:
            return -1
        
        last = nums[n-1]
        nums[n-1] = target
        
        i = 0
        while nums[i] != target:
            i += 1
        
        nums[n-1] = last
        
        if i < n-1 or nums[n-1] == target:
            return i
        return -1
```

**JavaScript:**

```javascript
class Solution {
    search(nums, target) {
        let n = nums.length;
        if (n === 0) return -1;
        
        let last = nums[n-1];
        nums[n-1] = target;
        
        let i = 0;
        while (nums[i] !== target) {
            i++;
        }
        
        nums[n-1] = last;
        
        if (i < n-1 || nums[n-1] === target) {
            return i;
        }
        return -1;
    }
}
```

**C:**

```c
int search(int* nums, int numsSize, int target) {
    if (numsSize == 0) return -1;
    
    int last = nums[numsSize-1];
    nums[numsSize-1] = target;
    
    int i = 0;
    while (nums[i] != target) {
        i++;
    }
    
    nums[numsSize-1] = last;
    
    if (i < numsSize-1 || nums[numsSize-1] == target) {
        return i;
    }
    return -1;
}
```


## Optimal Approach (Two-Way Linear Search)

The most optimized version that searches from both ends simultaneously, potentially reducing search time by half in the average case.[^2]

### Algorithm Explanation

1. Initialize two pointers: left at the beginning, right at the end
2. Compare elements at both left and right positions with the target
3. If target is found at either position, return that index
4. Move left pointer forward and right pointer backward
5. Continue until pointers meet or cross each other
6. Return -1 if target is not found

### Implementation

**C++:**

```cpp
class Solution {
public:
    int search(vector<int>& nums, int target) {
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
class Solution {
    public int search(int[] nums, int target) {
        int left = 0, right = nums.length - 1;
        
        while (left <= right) {
            if (nums[left] == target) return left;
            if (nums[right] == target) return right;
            
            left++;
            right--;
        }
        return -1;
    }
}
```

**Python:**

```python
class Solution:
    def search(self, nums, target):
        left, right = 0, len(nums) - 1
        
        while left <= right:
            if nums[left] == target:
                return left
            if nums[right] == target:
                return right
            
            left += 1
            right -= 1
        
        return -1
```

**JavaScript:**

```javascript
class Solution {
    search(nums, target) {
        let left = 0, right = nums.length - 1;
        
        while (left <= right) {
            if (nums[left] === target) return left;
            if (nums[right] === target) return right;
            
            left++;
            right--;
        }
        return -1;
    }
}
```

**C:**

```c
int search(int* nums, int numsSize, int target) {
    int left = 0, right = numsSize - 1;
    
    while (left <= right) {
        if (nums[left] == target) return left;
        if (nums[right] == target) return right;
        
        left++;
        right--;
    }
    return -1;
}
```


### Complexity Analysis

| Approach | Time Complexity | Space Complexity |
| :-- | :-- | :-- |
| **Brute Force** | O(n) | O(1) |
| **Better (Sentinel)** | O(n) | O(1) |
| **Optimal (Two-Way)** | O(n/2) average | O(1) |

The **optimal approach** provides the best average-case performance while maintaining O(1) space complexity, making it the most efficient linear search implementation for unsorted arrays.

[^2]: https://books.aijr.org/index.php/press/catalog/book/123/chapter/1506

