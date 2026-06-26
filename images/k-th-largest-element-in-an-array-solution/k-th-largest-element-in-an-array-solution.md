# K-th Largest Element in an Array - Solution

## Problem Statement

Given an unsorted array `arr` of size `N` and an integer `K`, find the `K`-th largest element in the array.

The `K`-th largest element is the element that would appear at position `K` in the array sorted in non-increasing order.

## Input Format

First line: Integer `N`

Second line: `N` space-separated integers representing `arr`

Third line: Integer `K`

## Output Format

Print a single integer representing the `K`-th largest element.

## Explanation

There are three approaches to solve this problem.

- **Approach 1:** Sort the Array
- **Approach 2:** Min Heap
- **Approach 3:** Quick Select (Optimal)

For example,

Input

6

3 2 1 5 6 4

2

Output

5

<approaches>
## Approach 1: Sort the Array

### Algorithm

1. Read the array and the value of `K`.
2. Sort the array in non-decreasing order.
3. The `K`-th largest element is at index `N - K`.
4. Print the answer.

```C
#include <stdio.h>
#include <stdlib.h>

int cmp(const void *a,const void *b)
{
    return (*(int *)a-*(int *)b);
}

int main()
{
    int n;
    scanf("%d",&n);

    int arr[n];

    for(int i=0;i<n;i++)
        scanf("%d",&arr[i]);

    int k;
    scanf("%d",&k);

    qsort(arr,n,sizeof(int),cmp);

    printf("%d",arr[n-k]);

    return 0;
}
```
```cpp
#include <iostream>
#include <vector>
#include <algorithm>
using namespace std;

int main()
{
    int n;
    cin>>n;

    vector<int> arr(n);

    for(int i=0;i<n;i++)
        cin>>arr[i];

    int k;
    cin>>k;

    sort(arr.begin(),arr.end());

    cout<<arr[n-k];

    return 0;
}
```
```Java
import java.util.*;

public class Main
{
    public static void main(String[] args)
    {
        Scanner sc=new Scanner(System.in);

        int n=sc.nextInt();

        int[] arr=new int[n];

        for(int i=0;i<n;i++)
            arr[i]=sc.nextInt();

        int k=sc.nextInt();

        Arrays.sort(arr);

        System.out.print(arr[n-k]);
    }
}
```
```Python
n=int(input())

arr=list(map(int,input().split()))

k=int(input())

arr.sort()

print(arr[n-k])
```
```C#
using System;

class Program
{
    static void Main()
    {
        int n=int.Parse(Console.ReadLine());

        int[] arr=Array.ConvertAll(Console.ReadLine().Split(),int.Parse);

        int k=int.Parse(Console.ReadLine());

        Array.Sort(arr);

        Console.Write(arr[n-k]);
    }
}
```
```JavaScript
const input=require("fs").readFileSync(0,"utf8").trim().split(/\s+/).map(Number);

let idx=0;

const n=input[idx++];

const arr=[];

for(let i=0;i<n;i++)
    arr.push(input[idx++]);

const k=input[idx++];

arr.sort((a,b)=>a-b);

console.log(arr[n-k]);
```

### Output
Input

6

3 2 1 5 6 4

2

Output

5

# Time Complexity
O(N log N)

# Space Complexity
O(1) (excluding sorting space used by the language implementation)

## Approach 2: Min Heap

### Algorithm

1. Create a min heap.
2. Traverse the array.
3. Insert each element into the heap.
4. If the heap size becomes greater than `K`, remove the minimum element.
5. After processing all elements, the root of the heap is the `K`-th largest element.

```C
#include <stdio.h>
#include <stdlib.h>

void swap(int *a,int *b)
{
    int t=*a;
    *a=*b;
    *b=t;
}

void heapifyUp(int heap[],int idx)
{
    while(idx>0)
    {
        int p=(idx-1)/2;

        if(heap[p]<=heap[idx])
            break;

        swap(&heap[p],&heap[idx]);
        idx=p;
    }
}

void heapifyDown(int heap[],int size,int idx)
{
    while(1)
    {
        int smallest=idx;
        int left=2*idx+1;
        int right=2*idx+2;

        if(left<size && heap[left]<heap[smallest])
            smallest=left;

        if(right<size && heap[right]<heap[smallest])
            smallest=right;

        if(smallest==idx)
            break;

        swap(&heap[idx],&heap[smallest]);
        idx=smallest;
    }
}

int main()
{
    int n;
    scanf("%d",&n);

    int heap[n];
    int size=0;

    for(int i=0;i<n;i++)
    {
        int x;
        scanf("%d",&x);

        heap[size]=x;
        heapifyUp(heap,size);
        size++;
    }

    int k;
    scanf("%d",&k);

    while(size>k)
    {
        heap[0]=heap[size-1];
        size--;
        heapifyDown(heap,size,0);
    }

    printf("%d",heap[0]);

    return 0;
}
```
```cpp
#include <iostream>
#include <queue>
using namespace std;

int main()
{
    int n;
    cin>>n;

    priority_queue<int,vector<int>,greater<int>> pq;

    int k;
    int x;

    vector<int> arr(n);

    for(int i=0;i<n;i++)
        cin>>arr[i];

    cin>>k;

    for(int num:arr)
    {
        pq.push(num);

        if((int)pq.size()>k)
            pq.pop();
    }

    cout<<pq.top();

    return 0;
}
```
```Java
import java.util.*;

public class Main
{
    public static void main(String[] args)
    {
        Scanner sc=new Scanner(System.in);

        int n=sc.nextInt();

        int[] arr=new int[n];

        for(int i=0;i<n;i++)
            arr[i]=sc.nextInt();

        int k=sc.nextInt();

        PriorityQueue<Integer> pq=new PriorityQueue<>();

        for(int x:arr)
        {
            pq.offer(x);

            if(pq.size()>k)
                pq.poll();
        }

        System.out.print(pq.peek());
    }
}
```
```Python
import heapq

n=int(input())

arr=list(map(int,input().split()))

k=int(input())

heap=[]

for x in arr:

    heapq.heappush(heap,x)

    if len(heap)>k:
        heapq.heappop(heap)

print(heap[0])
```
```C#
using System;
using System.Collections.Generic;

class Program
{
    static void Main()
    {
        int n=int.Parse(Console.ReadLine());

        int[] arr=Array.ConvertAll(Console.ReadLine().Split(),int.Parse);

        int k=int.Parse(Console.ReadLine());

        PriorityQueue<int,int> pq=new PriorityQueue<int,int>();

        foreach(int x in arr)
        {
            pq.Enqueue(x,x);

            if(pq.Count>k)
                pq.Dequeue();
        }

        Console.Write(pq.Peek());
    }
}
```
```JavaScript
class MinHeap
{
    constructor()
    {
        this.heap=[];
    }

    push(val)
    {
        this.heap.push(val);

        let i=this.heap.length-1;

        while(i>0)
        {
            let p=(i-1)>>1;

            if(this.heap[p]<=this.heap[i])
                break;

            [this.heap[p],this.heap[i]]=[this.heap[i],this.heap[p]];

            i=p;
        }
    }

    pop()
    {
        if(this.heap.length===1)
            return this.heap.pop();

        this.heap[0]=this.heap.pop();

        let i=0;

        while(true)
        {
            let s=i;
            let l=2*i+1;
            let r=2*i+2;

            if(l<this.heap.length && this.heap[l]<this.heap[s])
                s=l;

            if(r<this.heap.length && this.heap[r]<this.heap[s])
                s=r;

            if(s===i)
                break;

            [this.heap[s],this.heap[i]]=[this.heap[i],this.heap[s]];

            i=s;
        }
    }

    top()
    {
        return this.heap[0];
    }

    size()
    {
        return this.heap.length;
    }
}

const input=require("fs").readFileSync(0,"utf8").trim().split(/\s+/).map(Number);

let idx=0;

const n=input[idx++];

const arr=[];

for(let i=0;i<n;i++)
    arr.push(input[idx++]);

const k=input[idx++];

const heap=new MinHeap();

for(const x of arr)
{
    heap.push(x);

    if(heap.size()>k)
        heap.pop();
}

console.log(heap.top());
```

### Output
Input

6

3 2 1 5 6 4

2

Output

5

# Time Complexity
O(N log K)

# Space Complexity
O(K)

## Approach 3: Quick Select (Optimal)

### Algorithm

1. Convert the problem into finding the element at index `N - K` in sorted order.
2. Choose the last element as the pivot.
3. Partition the array so that all elements smaller than the pivot come before it.
4. If the pivot reaches the target index, print it.
5. Otherwise, continue the search in the left or right partition until the answer is found.

```C
#include <stdio.h>

void swap(int *a,int *b)
{
    int t=*a;
    *a=*b;
    *b=t;
}

int partition(int arr[],int low,int high)
{
    int pivot=arr[high];
    int i=low;

    for(int j=low;j<high;j++)
    {
        if(arr[j]<=pivot)
        {
            swap(&arr[i],&arr[j]);
            i++;
        }
    }

    swap(&arr[i],&arr[high]);

    return i;
}

int quickSelect(int arr[],int low,int high,int k)
{
    while(low<=high)
    {
        int p=partition(arr,low,high);

        if(p==k)
            return arr[p];

        if(p<k)
            low=p+1;
        else
            high=p-1;
    }

    return -1;
}

int main()
{
    int n;
    scanf("%d",&n);

    int arr[n];

    for(int i=0;i<n;i++)
        scanf("%d",&arr[i]);

    int k;
    scanf("%d",&k);

    printf("%d",quickSelect(arr,0,n-1,n-k));

    return 0;
}
```
```cpp
#include <iostream>
#include <vector>
using namespace std;

int partition(vector<int> &arr,int low,int high)
{
    int pivot=arr[high];
    int i=low;

    for(int j=low;j<high;j++)
    {
        if(arr[j]<=pivot)
        {
            swap(arr[i],arr[j]);
            i++;
        }
    }

    swap(arr[i],arr[high]);

    return i;
}

int quickSelect(vector<int> &arr,int low,int high,int k)
{
    while(low<=high)
    {
        int p=partition(arr,low,high);

        if(p==k)
            return arr[p];

        if(p<k)
            low=p+1;
        else
            high=p-1;
    }

    return -1;
}

int main()
{
    int n;
    cin>>n;

    vector<int> arr(n);

    for(int i=0;i<n;i++)
        cin>>arr[i];

    int k;
    cin>>k;

    cout<<quickSelect(arr,0,n-1,n-k);

    return 0;
}
```
```Java
import java.util.*;

public class Main
{
    static void swap(int[] arr,int i,int j)
    {
        int t=arr[i];
        arr[i]=arr[j];
        arr[j]=t;
    }

    static int partition(int[] arr,int low,int high)
    {
        int pivot=arr[high];
        int i=low;

        for(int j=low;j<high;j++)
        {
            if(arr[j]<=pivot)
            {
                swap(arr,i,j);
                i++;
            }
        }

        swap(arr,i,high);

        return i;
    }

    static int quickSelect(int[] arr,int low,int high,int k)
    {
        while(low<=high)
        {
            int p=partition(arr,low,high);

            if(p==k)
                return arr[p];

            if(p<k)
                low=p+1;
            else
                high=p-1;
        }

        return -1;
    }

    public static void main(String[] args)
    {
        Scanner sc=new Scanner(System.in);

        int n=sc.nextInt();

        int[] arr=new int[n];

        for(int i=0;i<n;i++)
            arr[i]=sc.nextInt();

        int k=sc.nextInt();

        System.out.print(quickSelect(arr,0,n-1,n-k));
    }
}
```
```Python
def partition(arr, low, high):

    pivot = arr[high]
    i = low

    for j in range(low, high):

        if arr[j] <= pivot:
            arr[i], arr[j] = arr[j], arr[i]
            i += 1

    arr[i], arr[high] = arr[high], arr[i]

    return i


def quickSelect(arr, low, high, k):

    while low <= high:

        p = partition(arr, low, high)

        if p == k:
            return arr[p]

        if p < k:
            low = p + 1
        else:
            high = p - 1

    return -1


n = int(input())

arr = list(map(int, input().split()))

k = int(input())

print(quickSelect(arr, 0, n - 1, n - k))
```
```C#
using System;

class Program
{
    static void Swap(int[] arr, int i, int j)
    {
        int temp = arr[i];
        arr[i] = arr[j];
        arr[j] = temp;
    }

    static int Partition(int[] arr, int low, int high)
    {
        int pivot = arr[high];
        int i = low;

        for (int j = low; j < high; j++)
        {
            if (arr[j] <= pivot)
            {
                Swap(arr, i, j);
                i++;
            }
        }

        Swap(arr, i, high);

        return i;
    }

    static int QuickSelect(int[] arr, int low, int high, int k)
    {
        while (low <= high)
        {
            int p = Partition(arr, low, high);

            if (p == k)
                return arr[p];

            if (p < k)
                low = p + 1;
            else
                high = p - 1;
        }

        return -1;
    }

    static void Main()
    {
        int n = int.Parse(Console.ReadLine());

        int[] arr = Array.ConvertAll(Console.ReadLine().Split(), int.Parse);

        int k = int.Parse(Console.ReadLine());

        Console.Write(QuickSelect(arr, 0, n - 1, n - k));
    }
}
```
```JavaScript
function partition(arr, low, high)
{
    const pivot = arr[high];

    let i = low;

    for (let j = low; j < high; j++)
    {
        if (arr[j] <= pivot)
        {
            [arr[i], arr[j]] = [arr[j], arr[i]];
            i++;
        }
    }

    [arr[i], arr[high]] = [arr[high], arr[i]];

    return i;
}

function quickSelect(arr, low, high, k)
{
    while (low <= high)
    {
        const p = partition(arr, low, high);

        if (p === k)
            return arr[p];

        if (p < k)
            low = p + 1;
        else
            high = p - 1;
    }

    return -1;
}

const input = require("fs").readFileSync(0, "utf8").trim().split(/\s+/).map(Number);

let idx = 0;

const n = input[idx++];

const arr = [];

for (let i = 0; i < n; i++)
    arr.push(input[idx++]);

const k = input[idx++];

console.log(quickSelect(arr, 0, n - 1, n - k));
```

### Output
Input

6

3 2 1 5 6 4

2

Output

5

# Time Complexity
Average Case: O(N)
Worst Case: O(N²)

# Space Complexity
Average Case:O(1) (iterative implementation)
Worst Case: O(1)

</approaches>




