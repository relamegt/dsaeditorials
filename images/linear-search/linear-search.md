# Linear Search

## 1. What is Linear Search?

 **Linear Search**  (also called  **Sequential Search** ) is a simple searching algorithm that checks  **each element one by one**  in a list until:

- the target element is found, or
- the list ends.

It works on  **both sorted and unsorted arrays** .

---

## 2. How Linear Search Works

1. Start from the first element.
2. Compare the current element with the key.
3. If it matches → return the index.
4. If not → move to the next element.
5. If the end is reached → element not found

---

## 3. Algorithm (Steps)

 **Input:**  Array  `A` , size  `n` , search key  `x` 

 *for i = 0 to n-1
    if A[i] == x
        return i
return -1* 

---

## 4. Time & Space Complexity

| Case | Time Complexity |
| --- | --- |
Best Case | O(1)
Average Case | O(n)
Worst Case | O(n)

### **Space Complexity:**  O(1)

---

## 5. Advantages & Disadvantages

### Advantages

- Very simple to implement
- Works on unsorted data
- No extra memory required

### Disadvantages

- Slow for large datasets
- Inefficient compared to binary search

---

## Below is Slide Play

<carousel>
<img src="https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/linear-search/1768483224034-Slide1.JPG" />
<img src="https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/linear-search/1768483225252-Slide2.JPG" />
<img src="https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/linear-search/1768483226569-Slide3.JPG" />
<img src="https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/linear-search/1768483228002-Slide4.JPG" />
<img src="https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/linear-search/1768483229015-Slide5.JPG" />
</carousel>

<approaches>
## Implementation

1. Define the array/list
The program stores elements in an array (or list) where the search will be performed.
2. Take the search key
A variable is used to store the element that needs to be searched.
3. Create a Linear Search function
A function is defined that takes the array and the search key as input.
4. Start loop from first element
The loop begins from index 0 and moves sequentially till the last element.
5. Compare elements one by one
Each element of the array is compared with the search key using an if condition.
6. Element found condition
If a match is found, the function immediately returns the index (position) of the element.
7. Continue search if not found
If the current element does not match, the loop continues to the next element.
8. Element not found condition
If the loop completes and no match is found, the function returns -1.
9. Check returned value in main program
The main function checks the returned value to decide whether the element exists.
10. Display output
If the return value is not -1, the element is found and its index is displayed; otherwise, a “not found” message is printed.

```cpp
#include <iostream>
using namespace std;

int linearSearch(int arr[], int n, int key) {
    for(int i = 0; i < n; i++) {
        if(arr[i] == key)
            return i;
    }
    return -1;
}

int main() {
    int arr[] = {5, 15, 25, 35};
    int key = 35;
    int n = 4;

    int result = linearSearch(arr, n, key);

    if(result != -1)
        cout << "Element found at index " << result;
    else
        cout << "Element not found";

    return 0;
}

```

```java
class LinearSearch {
    static int linearSearch(int arr[], int key) {
        for(int i = 0; i < arr.length; i++) {
            if(arr[i] == key)
                return i;
        }
        return -1;
    }

    public static void main(String args[]) {
        int arr[] = {2, 4, 6, 8, 10};
        int key = 8;

        int result = linearSearch(arr, key);

        if(result != -1)
            System.out.println("Element found at index " + result);
        else
            System.out.println("Element not found");
    }
}

```

```python
def linear_search(arr, key):
    for i in range(len(arr)):
        if arr[i] == key:
            return i
    return -1

arr = [1, 3, 7, 5, 9]
key = 5

result = linear_search(arr, key)

if result != -1:
    print("Element found at index", result)
else:
    print("Element not found")

```

```c
#include <stdio.h>

int linearSearch(int arr[], int n, int key) {
    for(int i = 0; i < n; i++) {
        if(arr[i] == key)
            return i;
    }
    return -1;
}

int main() {
    int arr[] = {10, 20, 40, 30, 50};
    int key = 30;
    int n = 5;

    int result = linearSearch(arr, n, key);

    if(result != -1)
        printf("Element found at index %d", result);
    else
        printf("Element not found");

    return 0;
}

```

```javascript
function linearSearch(arr, key) {
    for(let i = 0; i < arr.length; i++) {
        if(arr[i] === key)
            return i;
    }
    return -1;
}

let arr = [11, 44, 33, 22];
let key = 22;

let result = linearSearch(arr, key);

if(result !== -1)
    console.log("Element found at index " + result);
else
    console.log("Element not found");

```

### Output
Element found at index 3

# Time Complexity
O(N) Traverses the array only once

# Space Complexity
O(1) No Extra space required

</approaches>



### *Special Thanks to  [Mohit](https://www.linkedin.com/in/mohit-ch/)*

<img src="https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/linear-search/1768490206043-Slide1.JPG" />
