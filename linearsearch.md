text
# Linear Search Editorial

## Problem Statement
Given an array of integers and a target value, find the index of the target element in the array. If the target is not found, return -1.

**Example 1:**
Input: nums = , target = 4
Output: 2
Explanation: The target 4 is found at index 2

text

**Example 2:**
Input: nums = , target = 6
Output: -1
Explanation: The target 6 is not present in the array

text

**Constraints:**
- 1 ≤ nums.length ≤ 10⁴
- -10⁴ ≤ nums[i] ≤ 10⁴
- -10⁴ ≤ target ≤ 10⁴

## Approaches

<details>
<summary><b>🔴 Brute Force Approach (Linear Search)</b></summary>

### Intuition
Linear search is the most straightforward searching algorithm. We traverse through each element of the array sequentially and compare it with the target value. If we find a match, we return the index. Ifindex. If we reach the end without finding the target, we return -1.

### Algorithm
1. Start from the first element of the array (index 0)
2. Compare the current element with the target
3. If they match, return the current index
4. If they don't match, move to the next element
5. Repeat steps 2-4 until either:
   - We find the target (return index)
   - We reach the end of array (return -1)

### Visual Explanation
Array: , Target = 4

Step 1: Check index 0 → nums = 3 ≠ 4
Step 2: Check index 1 → nums = 1 ≠ 4
Step 3: Check index 2 → nums = 4 = 4 ✅ FOUND!
Return index 2

text

### Complexity Analysis
- **Time Complexity:** O(n)
  - In worst case, we need to traverse the entire array
  - Best case: O(1) if target is at first position
  - Average case: O(n/2) ≈ O(n)
- **Space Complexity:** O(1)
  - We only use constant extra space for variables

### Implementation

// C++ Linear Search Implementation
class Solution {
public:
int search(vector<int>& nums, int target) {
// Traverse through each element
for (int i = 0; i < nums.size(); i++) {
// Check if current element matches target
if (nums[i] == target) {
return i; // Found! Return the index
}
}
// Target not found
return -1;
}
};

---java---
// Java Linear Search Implementation
class Solution {
public int search(int[] nums, int target) {
// Traverse through each element
for (int i = 0; i < nums.length; i++) {
// Check if current element matches target
if (nums[i] == target) {
return i; // Found! Return the index
}
}
// Target not found
return -1;
}
}

---python---

Python Linear Search Implementation
class Solution:
def search(self, nums, target):
# Traverse through each element with index
for i in range(len(nums)):
# Check if current element matches target
if nums[i] == target:
return i # Found! Return the index

text
    # Target not found
    return -1
text

### Dry Run Example
Input: nums = , target = 4

Iteration 1: i = 0
nums = 3, target = 4
3 ≠ 4, continue

Iteration 2: i = 1
nums = 1, target = 4
1 ≠ 4, continue

Iteration 3: i = 2
nums = 4, target = 4
4 = 4, MATCH! Return i = 2

Output: 2

text

</details>

<details>
<summary><b>🟡 Enhanced Linear Search (Early Termination)</b></summary>

### Intuition
We can optimize the basic linear search by adding early termination conditions or using built-in functions that are optimized at the language level.

### Key Optimizations
1. **Early termination:** Stop as soon as we find the target
2. **Use built-in functions:** Languages often have optimized search functions
3. **Range-based loops:** More readable and potentially faster

### Algorithm
Same as basic linear search but with optimizations:
1. Use range-based iteration where possible
2. Early return on first match
3. Leverage language-specific optimizations

### Implementation

// C++ Enhanced Linear Search
class Solution {
public:
int search(vector<int>& nums, int target) {
// Method 1: Range-based loop with manual index tracking
int index = 0;
for (const int& num : nums) {
if (num == target) return index;
index++;
}
return -1;

text
    // Method 2: Using STL find function
    // auto it = find(nums.begin(), nums.end(), target);
    // return (it != nums.end()) ? distance(nums.begin(), it) : -1;
}
};

---java---
// Java Enhanced Linear Search
class Solution {
public int search(int[] nums, int target) {
// Method 1: Enhanced for loop
int index = 0;
for (int num : nums) {
if (num == target) return index;
index++;
}
return -1;

text
    // Method 2: Using Collections (for List)
    // List<Integer> list = Arrays.asList(nums);
    // return list.indexOf(target);
}
}

---python---

Python Enhanced Linear Search
class Solution:
def search(self, nums, target):
# Method 1: Using enumerate for cleaner code
for i, num in enumerate(nums):
if num == target:
return i
return -1

text
    # Method 2: Using built-in index method with exception handling
    # try:
    #     return nums.index(target)
    # except ValueError:
    #     return -1
text

### Complexity Analysis
- **Time Complexity:** O(n) - Same as basic approach
- **Space Complexity:** O(1) - Constant extra space
- **Advantages:** More readable code, potentially better performance due to compiler optimizations

</details>

<details open>
<summary><b>🟢 Optimal Approach (Problem-Specific Optimizations)</b></summary>

### Intuition
While linear search is already optimal for unsorted arrays, we can discuss when other approaches might be better and what optimizations are possible.

### When Linear Search is Optimal
Linear search is the **best possible approach** when:
1. **Unsorted array:** No better algorithm exists for unsorted data
2. **Small datasets:** Overhead of other algorithms isn't worth it
3. **Single search:** For one-time searches, sorting isn't beneficial
4. **Unknown data distribution:** No assumptions about data organization

### Alternative Approaches (When Applicable)

#### Binary Search (If Array is Sorted)
// Only applicable if array is sorted
int binarySearch(vector<int>& nums, int target) {
int left = 0, right = nums.size() - 1;
while (left <= right) {
int mid = left + (right - left) / 2;
if (nums[mid] == target) return mid;
if (nums[mid] < target) left = mid + 1;
else right = mid - 1;
}
return -1;
}
// Time: O(log n), Space: O(1)

text

#### Hash Map (For Multiple Searches)
// If we need to search multiple times
unordered_map<int, vector<int>> buildIndex(vector<int>& nums) {
unordered_map<int, vector<int>> index;
for (int i = 0; i < nums.size(); i++) {
index[nums[i]].push_back(i);
}
return index;
}
// Time: O(n) build, O(1) search, Space: O(n)

text

### Most Optimized Linear Search

// C++ Most Optimized Linear Search
class Solution {
public:
int search(vector<int>& nums, int target) {
// Use iterators for potential compiler optimizations
for (auto it = nums.begin(); it != nums.end(); ++it) {
if (*it == target) {
return distance(nums.begin(), it);
}
}
return -1;
}

text
// Alternative: Unrolled loop for small arrays
int searchUnrolled(vector<int>& nums, int target) {
    int n = nums.size();
    int i = 0;
    
    // Process 4 elements at a time
    for (; i <= n - 4; i += 4) {
        if (nums[i] == target) return i;
        if (nums[i + 1] == target) return i + 1;
        if (nums[i + 2] == target) return i + 2;
        if (nums[i + 3] == target) return i + 3;
    }
    
    // Handle remaining elements
    for (; i < n; i++) {
        if (nums[i] == target) return i;
    }
    
    return -1;
}
};

---java---
// Java Most Optimized Linear Search
class Solution {
public int search(int[] nums, int target) {
// Basic optimized version
for (int i = 0; i < nums.length; i++) {
if (nums[i] == target) return i;
}
return -1;
}

text
// Alternative: Using parallel streams for large arrays
public int searchParallel(int[] nums, int target) {
    return IntStream.range(0, nums.length)
                  .parallel()
                  .filter(i -> nums[i] == target)
                  .findFirst()
                  .orElse(-1);
}
}

---python---

Python Most Optimized Linear Search
class Solution:
def search(self, nums, target):
# Most Pythonic and optimized
try:
return nums.index(target)
except ValueError:
return -1

text
# Alternative: Using list comprehension with next()
def search_alternative(self, nums, target):
    return next((i for i, x in enumerate(nums) if x == target), -1)

# Alternative: Using numpy for large arrays
def search_numpy(self, nums, target):
    import numpy as np
    arr = np.array(nums)
    indices = np.where(arr == target)
    return int(indices) if len(indices) > 0 else -1
text

### Performance Comparison

| Approach | Time Complexity | Space Complexity | Best Use Case |
|----------|----------------|------------------|---------------|
| Linear Search | O(n) | O(1) | Unsorted arrays, single search |
| Binary Search | O(log n) | O(1) | Sorted arrays |
| Hash Map | O(1) search, O(n) build | O(n) | Multiple searches |

### Complexity Analysis
- **Time Complexity:** O(n) - Must check each element in worst case
- **Space Complexity:** O(1) - Only using constant extra variables
- **Best Case:** O(1) - Target is first element
- **Average Case:** O(n/2) - Target is in middle on average
- **Worst Case:** O(n) - Target is last element or not present

</details>

## Key Takeaways

### When to Use Linear Search
✅ **Unsorted data:** Only option for unsorted arrays  
✅ **Small datasets:** Simple and efficient for small arrays  
✅ **One-time search:** No preprocessing overhead  
✅ **Unknown patterns:** When data distribution is unknown  

### When to Consider Alternatives
❌ **Large sorted arrays:** Binary search is better O(log n)  
❌ **Multiple searches:** Hash map preprocessing might help  
❌ **Frequent updates:** Consider balanced trees or other data structures  

### Optimization Tips
1. **Early termination:** Return immediately when found
2. **Use built-in functions:** Language-optimized implementations
3. **Consider data patterns:** If data has patterns, exploit them
4. **Memory access:** Sequential access is cache-friendly

## Practice Problems

Try these related problems to master linear search:

1. **[Search Insert Position](https://leetcode.com/problems/search-insert-position/)** - Find position to insert in sorted array
2. **[First Bad Version](https://leetcode.com/problems/first-bad-version/)** - Binary search variation
3. **[Peak Index in Mountain Array](https://leetcode.com/problems/peak-index-in-a-mountain-array/)** - Finding peak element
4. **[Find First and Last Position](https://leetcode.com/problems/find-first-and-last-position-of-element-in-sorted-array/)** - Multiple occurrences

## Real-world Applications

- **Database scanning:** When indexes aren't available
- **Log file analysis:** Searching through unstructured logs  
- **Small datasets:** Contact lists, small inventories
- **Streaming data:** When data arrives sequentially
- **Embedded systems:** When memory is limited

---

*Remember: Linear search might seem basic, but it's fundamental to understanding how 