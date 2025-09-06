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

```javascript
function search(nums, target) {
    for (let i = 0; i < nums.length; i++) {
        if (nums[i] === target) {
            return i;
        }
    }
    return -1;
}
```

```python
def search(nums, target):
    for i in range(len(nums)):
        if nums[i] == target:
            return i
    return -1
```


### Time Complexity

O(n) where n is the number of elements in the array. In worst case, we might have to check all elements.

### Space Complexity

O(1) as we only use a constant amount of extra space for the loop variable.

## Optimized Approach

For linear search, there isn't much room for optimization in terms of time complexity, but we can make small improvements.

### Early Termination with Sentinel

We can add the target element at the end of the array to avoid boundary checking in every iteration.

```cpp
class Solution {
public:
    int searchWithSentinel(vector<int>& nums, int target) {
        int n = nums.size();
        if (n == 0) return -1;
        
        // Store the last element
        int last = nums[n-1];
        
        // Put target at the end
        nums[n-1] = target;
        
        int i = 0;
        while (nums[i] != target) {
            i++;
        }
        
        // Restore the last element
        nums[n-1] = last;
        
        // Check if target was found before the last element
        // or if the last element was the target
        if (i < n-1 || nums[n-1] == target) {
            return i;
        }
        
        return -1;
    }
};
```

```java
class Solution {
    public int searchWithSentinel(int[] nums, int target) {
        int n = nums.length;
        if (n == 0) return -1;
        
        // Store the last element
        int last = nums[n-1];
        
        // Put target at the end
        nums[n-1] = target;
        
        int i = 0;
        while (nums[i] != target) {
            i++;
        }
        
        // Restore the last element
        nums[n-1] = last;
        
        // Check if target was found before the last element
        // or if the last element was the target
        if (i < n-1 || nums[n-1] == target) {
            return i;
        }
        
        return -1;
    }
}
```

```javascript
function searchWithSentinel(nums, target) {
    const n = nums.length;
    if (n === 0) return -1;
    
    // Store the last element
    const last = nums[n-1];
    
    // Put target at the end
    nums[n-1] = target;
    
    let i = 0;
    while (nums[i] !== target) {
        i++;
    }
    
    // Restore the last element
    nums[n-1] = last;
    
    // Check if target was found before the last element
    // or if the last element was the target
    if (i < n-1 || nums[n-1] === target) {
        return i;
    }
    
    return -1;
}
```

```python
def search_with_sentinel(nums, target):
    n = len(nums)
    if n == 0:
        return -1
    
    # Store the last element
    last = nums[n-1]
    
    # Put target at the end
    nums[n-1] = target
    
    i = 0
    while nums[i] != target:
        i += 1
    
    # Restore the last element
    nums[n-1] = last
    
    # Check if target was found before the last element
    # or if the last element was the target
    if i < n-1 or nums[n-1] == target:
        return i
    
    return -1
```


### Time Complexity

O(n) - Same as brute force but with slightly better constants due to reduced boundary checking.

### Space Complexity

O(1) - Still constant space complexity.

## Better Approach

For unsorted arrays, linear search is optimal. However, if we can sort the array first, we can use binary search for better performance.

### Pre-sorting + Binary Search

```cpp
class Solution {
public:
    int searchInSorted(vector<int>& nums, int target) {
        // This assumes array is already sorted
        int left = 0, right = nums.size() - 1;
        
        while (left <= right) {
            int mid = left + (right - left) / 2;
            
            if (nums[mid] == target) {
                return mid;
            } else if (nums[mid] < target) {
                left = mid + 1;
            } else {
                right = mid - 1;
            }
        }
        
        return -1;
    }
};
```

```java
class Solution {
    public int searchInSorted(int[] nums, int target) {
        // This assumes array is already sorted
        int left = 0, right = nums.length - 1;
        
        while (left <= right) {
            int mid = left + (right - left) / 2;
            
            if (nums[mid] == target) {
                return mid;
            } else if (nums[mid] < target) {
                left = mid + 1;
            } else {
                right = mid - 1;
            }
        }
        
        return -1;
    }
}
```

```javascript
function searchInSorted(nums, target) {
    // This assumes array is already sorted
    let left = 0, right = nums.length - 1;
    
    while (left <= right) {
        const mid = Math.floor(left + (right - left) / 2);
        
        if (nums[mid] === target) {
            return mid;
        } else if (nums[mid] < target) {
            left = mid + 1;
        } else {
            right = mid - 1;
        }
    }
    
    return -1;
}
```

```python
def search_in_sorted(nums, target):
    # This assumes array is already sorted
    left, right = 0, len(nums) - 1
    
    while left <= right:
        mid = left + (right - left) // 2
        
        if nums[mid] == target:
            return mid
        elif nums[mid] < target:
            left = mid + 1
        else:
            right = mid - 1
    
    return -1
```


### Time Complexity

O(log n) for searching in sorted array, but O(n log n) if we need to sort first.

### Space Complexity

O(1) for iterative binary search, O(log n) for recursive approach due to call stack.

