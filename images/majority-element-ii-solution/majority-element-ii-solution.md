# Majority Element II - Solution

## Problem Statement

Given an integer array `nums` of size `n`, find all elements that appear more than `floor(n / 3)` times.

Print the qualifying elements in increasing order. If no such element exists, print an empty line.

## Input Format

First line: Integer `n`

Second line: `n` space-separated integers

## Output Format

Print all elements that appear more than `floor(n / 3)` times in increasing order.

If no such element exists, print an empty line.

## Explanation

There are three common approaches to solve this problem.

- **Brute Force:** Count the frequency of every element by scanning the array repeatedly.
- **Hash Map:** Store the frequency of every element using a hash map.
- **Extended Boyer-Moore Voting Algorithm (Optimal):** Maintain two candidates and verify their frequencies.

For example,

Input

3

3 2 3

Output

3

<approaches>
## Approach 1: Brute Force

### Algorithm

1. Read the array.
2. For every element:

- Count its occurrences by traversing the array again.

1. If its frequency is greater than `n / 3` and it has not already been printed, print it.
2. Print the elements in increasing order.

```C
#include <stdio.h>
#include <stdlib.h>

int compare(const void *a,const void *b)
{
    long long x=*(long long*)a;
    long long y=*(long long*)b;

    if(x<y) return -1;
    if(x>y) return 1;
    return 0;
}

int main()
{
    int n;
    scanf("%d",&n);

    long long arr[n];

    for(int i=0;i<n;i++)
        scanf("%lld",&arr[i]);

    qsort(arr,n,sizeof(long long),compare);

    int first=1;

    for(int i=0;i<n;i++)
    {
        if(i>0 && arr[i]==arr[i-1])
            continue;

        int count=0;

        for(int j=0;j<n;j++)
        {
            if(arr[j]==arr[i])
                count++;
        }

        if(count>n/3)
        {
            if(!first)
                printf(" ");

            printf("%lld",arr[i]);

            first=0;
        }
    }

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

    vector<long long> arr(n);

    for(int i=0;i<n;i++)
        cin>>arr[i];

    sort(arr.begin(),arr.end());

    bool first=true;

    for(int i=0;i<n;i++)
    {
        if(i>0 && arr[i]==arr[i-1])
            continue;

        int count=0;

        for(int j=0;j<n;j++)
        {
            if(arr[j]==arr[i])
                count++;
        }

        if(count>n/3)
        {
            if(!first)
                cout<<" ";

            cout<<arr[i];

            first=false;
        }
    }

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

        long[] arr=new long[n];

        for(int i=0;i<n;i++)
            arr[i]=sc.nextLong();

        Arrays.sort(arr);

        boolean first=true;

        for(int i=0;i<n;i++)
        {
            if(i>0 && arr[i]==arr[i-1])
                continue;

            int count=0;

            for(int j=0;j<n;j++)
            {
                if(arr[j]==arr[i])
                    count++;
            }

            if(count>n/3)
            {
                if(!first)
                    System.out.print(" ");

                System.out.print(arr[i]);

                first=false;
            }
        }
    }
}
```
```Python
n=int(input())

arr=list(map(int,input().split()))

arr.sort()

first=True

for i in range(n):

    if i>0 and arr[i]==arr[i-1]:
        continue

    count=0

    for j in range(n):

        if arr[j]==arr[i]:
            count+=1

    if count>n//3:

        if not first:
            print(end=" ")

        print(arr[i],end="")

        first=False
```
```C#
using System;

class Program
{
    static void Main()
    {
        int n = int.Parse(Console.ReadLine());

        long[] arr = Array.ConvertAll(Console.ReadLine().Split(), long.Parse);

        Array.Sort(arr);

        bool first = true;

        for(int i = 0; i < n; i++)
        {
            if(i > 0 && arr[i] == arr[i - 1])
                continue;

            int count = 0;

            for(int j = 0; j < n; j++)
            {
                if(arr[j] == arr[i])
                    count++;
            }

            if(count > n / 3)
            {
                if(!first)
                    Console.Write(" ");

                Console.Write(arr[i]);

                first = false;
            }
        }
    }
}
```
```JavaScript
const input = require("fs").readFileSync(0, "utf8").trim().split(/\s+/).map(Number);

let idx = 0;

const n = input[idx++];

const arr = [];

for(let i = 0; i < n; i++)
    arr.push(input[idx++]);

arr.sort((a, b) => a - b);

let first = true;

for(let i = 0; i < n; i++)
{
    if(i > 0 && arr[i] === arr[i - 1])
        continue;

    let count = 0;

    for(let j = 0; j < n; j++)
    {
        if(arr[j] === arr[i])
            count++;
    }

    if(count > Math.floor(n / 3))
    {
        if(!first)
            process.stdout.write(" ");

        process.stdout.write(arr[i].toString());

        first = false;
    }
}
```

### Output
Input

3

3 2 3

Output

3

# Time Complexity
O(N²)

# Space Complexity
O(1)

## Approach 2: Hash Map

### Algorithm

1. Read the array.
2. Store the frequency of every element in a hash map.
3. Traverse the hash map and collect all elements whose frequency is greater than `n / 3`.
4. Sort the collected elements.
5. Print them in increasing order.

```C
#include <stdio.h>
#include <stdlib.h>

#define SIZE 100003

typedef struct Node
{
    long long key;
    int freq;
    struct Node *next;
} Node;

Node *table[SIZE];

int hash(long long x)
{
    if(x < 0)
        x = -x;

    return x % SIZE;
}

Node* find(long long key)
{
    int h = hash(key);

    Node *temp = table[h];

    while(temp)
    {
        if(temp->key == key)
            return temp;

        temp = temp->next;
    }

    return NULL;
}

void insert(long long key)
{
    Node *node = find(key);

    if(node)
    {
        node->freq++;
        return;
    }

    int h = hash(key);

    node = (Node*)malloc(sizeof(Node));

    node->key = key;
    node->freq = 1;
    node->next = table[h];

    table[h] = node;
}

int compare(const void *a,const void *b)
{
    long long x=*(long long*)a;
    long long y=*(long long*)b;

    if(x<y) return -1;
    if(x>y) return 1;
    return 0;
}

int main()
{
    int n;
    scanf("%d",&n);

    for(int i=0;i<n;i++)
    {
        long long x;
        scanf("%lld",&x);
        insert(x);
    }

    long long ans[2];
    int k=0;

    for(int i=0;i<SIZE;i++)
    {
        Node *temp=table[i];

        while(temp)
        {
            if(temp->freq>n/3)
                ans[k++]=temp->key;

            temp=temp->next;
        }
    }

    qsort(ans,k,sizeof(long long),compare);

    for(int i=0;i<k;i++)
    {
        if(i)
            printf(" ");

        printf("%lld",ans[i]);
    }

    return 0;
}
```
```cpp
#include <iostream>
#include <unordered_map>
#include <vector>
#include <algorithm>
using namespace std;

int main()
{
    int n;
    cin >> n;

    unordered_map<long long,int> freq;

    for(int i = 0; i < n; i++)
    {
        long long x;
        cin >> x;
        freq[x]++;
    }

    vector<long long> ans;

    for(auto it : freq)
    {
        if(it.second > n / 3)
            ans.push_back(it.first);
    }

    sort(ans.begin(), ans.end());

    for(int i = 0; i < ans.size(); i++)
    {
        if(i)
            cout << " ";

        cout << ans[i];
    }

    return 0;
}
```
```Java
import java.util.*;

public class Main
{
    public static void main(String[] args)
    {
        Scanner sc = new Scanner(System.in);

        int n = sc.nextInt();

        HashMap<Long, Integer> map = new HashMap<>();

        for(int i = 0; i < n; i++)
        {
            long x = sc.nextLong();
            map.put(x, map.getOrDefault(x, 0) + 1);
        }

        ArrayList<Long> ans = new ArrayList<>();

        for(Map.Entry<Long, Integer> entry : map.entrySet())
        {
            if(entry.getValue() > n / 3)
                ans.add(entry.getKey());
        }

        Collections.sort(ans);

        for(int i = 0; i < ans.size(); i++)
        {
            if(i > 0)
                System.out.print(" ");

            System.out.print(ans.get(i));
        }
    }
}
```
```Python
n = int(input())

arr = list(map(int, input().split()))

freq = {}

for value in arr:
    freq[value] = freq.get(value, 0) + 1

ans = []

for key in freq:
    if freq[key] > n // 3:
        ans.append(key)

ans.sort()

print(*ans)
```
```C#
using System;
using System.Collections.Generic;

class Program
{
    static void Main()
    {
        int n = int.Parse(Console.ReadLine());

        long[] arr = Array.ConvertAll(Console.ReadLine().Split(), long.Parse);

        Dictionary<long, int> freq = new Dictionary<long, int>();

        foreach(long value in arr)
        {
            if(freq.ContainsKey(value))
                freq[value]++;
            else
                freq[value] = 1;
        }

        List<long> ans = new List<long>();

        foreach(var item in freq)
        {
            if(item.Value > n / 3)
                ans.Add(item.Key);
        }

        ans.Sort();

        for(int i = 0; i < ans.Count; i++)
        {
            if(i > 0)
                Console.Write(" ");

            Console.Write(ans[i]);
        }
    }
}
```
```JavaScript
const input = require("fs").readFileSync(0, "utf8").trim().split(/\s+/).map(Number);

let idx = 0;

const n = input[idx++];

const freq = new Map();

for(let i = 0; i < n; i++)
{
    const value = input[idx++];
    freq.set(value, (freq.get(value) || 0) + 1);
}

const ans = [];

for(const [key, value] of freq)
{
    if(value > Math.floor(n / 3))
        ans.push(key);
}

ans.sort((a, b) => a - b);

console.log(ans.join(" "));
```

### Output
Input

3

3 2 3

Output

3

# Time Complexity
O(N)

# Space Complexity
O(N)

## Approach 3: Extended Boyer-Moore Voting Algorithm (Optimal)

### Algorithm

1. Initialize two candidates (`candidate1`, `candidate2`) and their counts (`count1`, `count2`).
2. Traverse the array:

- If the current element matches `candidate1`, increment `count1`.
- Else if it matches `candidate2`, increment `count2`.
- Else if `count1` is `0`, make the current element `candidate1`.
- Else if `count2` is `0`, make the current element `candidate2`.
- Otherwise, decrement both counts.

1. Reset both counts to `0`.
2. Traverse the array again to count the actual occurrences of the two candidates.
3. Add candidates whose frequency is greater than `n / 3`.
4. Sort the answer and print it.

```C
#include <stdio.h>
#include <stdlib.h>

int compare(const void *a,const void *b)
{
    long long x=*(long long*)a;
    long long y=*(long long*)b;

    if(x<y) return -1;
    if(x>y) return 1;
    return 0;
}

int main()
{
    int n;
    scanf("%d",&n);

    long long arr[n];

    for(int i=0;i<n;i++)
        scanf("%lld",&arr[i]);

    long long candidate1=0,candidate2=1;
    int count1=0,count2=0;

    for(int i=0;i<n;i++)
    {
        if(arr[i]==candidate1)
            count1++;
        else if(arr[i]==candidate2)
            count2++;
        else if(count1==0)
        {
            candidate1=arr[i];
            count1=1;
        }
        else if(count2==0)
        {
            candidate2=arr[i];
            count2=1;
        }
        else
        {
            count1--;
            count2--;
        }
    }

    count1=0;
    count2=0;

    for(int i=0;i<n;i++)
    {
        if(arr[i]==candidate1)
            count1++;
        else if(arr[i]==candidate2)
            count2++;
    }

    long long ans[2];
    int k=0;

    if(count1>n/3)
        ans[k++]=candidate1;

    if(count2>n/3)
        ans[k++]=candidate2;

    qsort(ans,k,sizeof(long long),compare);

    for(int i=0;i<k;i++)
    {
        if(i)
            printf(" ");

        printf("%lld",ans[i]);
    }

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
    cin >> n;

    vector<long long> arr(n);

    for(int i = 0; i < n; i++)
        cin >> arr[i];

    long long candidate1 = 0, candidate2 = 1;
    int count1 = 0, count2 = 0;

    for(long long value : arr)
    {
        if(value == candidate1)
            count1++;
        else if(value == candidate2)
            count2++;
        else if(count1 == 0)
        {
            candidate1 = value;
            count1 = 1;
        }
        else if(count2 == 0)
        {
            candidate2 = value;
            count2 = 1;
        }
        else
        {
            count1--;
            count2--;
        }
    }

    count1 = 0;
    count2 = 0;

    for(long long value : arr)
    {
        if(value == candidate1)
            count1++;
        else if(value == candidate2)
            count2++;
    }

    vector<long long> ans;

    if(count1 > n / 3)
        ans.push_back(candidate1);

    if(count2 > n / 3)
        ans.push_back(candidate2);

    sort(ans.begin(), ans.end());

    for(int i = 0; i < ans.size(); i++)
    {
        if(i)
            cout << " ";

        cout << ans[i];
    }

    return 0;
}
```
```Java
import java.util.*;

public class Main
{
    public static void main(String[] args)
    {
        Scanner sc = new Scanner(System.in);

        int n = sc.nextInt();

        long[] arr = new long[n];

        for(int i = 0; i < n; i++)
            arr[i] = sc.nextLong();

        long candidate1 = 0;
        long candidate2 = 1;

        int count1 = 0;
        int count2 = 0;

        for(long value : arr)
        {
            if(value == candidate1)
                count1++;
            else if(value == candidate2)
                count2++;
            else if(count1 == 0)
            {
                candidate1 = value;
                count1 = 1;
            }
            else if(count2 == 0)
            {
                candidate2 = value;
                count2 = 1;
            }
            else
            {
                count1--;
                count2--;
            }
        }

        count1 = 0;
        count2 = 0;

        for(long value : arr)
        {
            if(value == candidate1)
                count1++;
            else if(value == candidate2)
                count2++;
        }

        ArrayList<Long> ans = new ArrayList<>();

        if(count1 > n / 3)
            ans.add(candidate1);

        if(count2 > n / 3)
            ans.add(candidate2);

        Collections.sort(ans);

        for(int i = 0; i < ans.size(); i++)
        {
            if(i > 0)
                System.out.print(" ");

            System.out.print(ans.get(i));
        }
    }
}
```
```Python
n = int(input())

arr = list(map(int, input().split()))

candidate1 = 0
candidate2 = 1
count1 = 0
count2 = 0

for value in arr:

    if value == candidate1:
        count1 += 1
    elif value == candidate2:
        count2 += 1
    elif count1 == 0:
        candidate1 = value
        count1 = 1
    elif count2 == 0:
        candidate2 = value
        count2 = 1
    else:
        count1 -= 1
        count2 -= 1

count1 = 0
count2 = 0

for value in arr:

    if value == candidate1:
        count1 += 1
    elif value == candidate2:
        count2 += 1

ans = []

if count1 > n // 3:
    ans.append(candidate1)

if count2 > n // 3:
    ans.append(candidate2)

ans.sort()

print(*ans)
```
```C#
using System;
using System.Collections.Generic;

class Program
{
    static void Main()
    {
        int n = int.Parse(Console.ReadLine());

        long[] arr = Array.ConvertAll(Console.ReadLine().Split(), long.Parse);

        long candidate1 = 0, candidate2 = 1;
        int count1 = 0, count2 = 0;

        foreach(long value in arr)
        {
            if(value == candidate1)
                count1++;
            else if(value == candidate2)
                count2++;
            else if(count1 == 0)
            {
                candidate1 = value;
                count1 = 1;
            }
            else if(count2 == 0)
            {
                candidate2 = value;
                count2 = 1;
            }
            else
            {
                count1--;
                count2--;
            }
        }

        count1 = 0;
        count2 = 0;

        foreach(long value in arr)
        {
            if(value == candidate1)
                count1++;
            else if(value == candidate2)
                count2++;
        }

        List<long> ans = new List<long>();

        if(count1 > n / 3)
            ans.Add(candidate1);

        if(count2 > n / 3)
            ans.Add(candidate2);

        ans.Sort();

        for(int i = 0; i < ans.Count; i++)
        {
            if(i > 0)
                Console.Write(" ");

            Console.Write(ans[i]);
        }
    }
}
```
```JavaScript
const input = require("fs").readFileSync(0, "utf8").trim().split(/\s+/).map(Number);

let idx = 0;

const n = input[idx++];

const arr = [];

for(let i = 0; i < n; i++)
    arr.push(input[idx++]);

let candidate1 = 0;
let candidate2 = 1;
let count1 = 0;
let count2 = 0;

for(const value of arr)
{
    if(value === candidate1)
        count1++;
    else if(value === candidate2)
        count2++;
    else if(count1 === 0)
    {
        candidate1 = value;
        count1 = 1;
    }
    else if(count2 === 0)
    {
        candidate2 = value;
        count2 = 1;
    }
    else
    {
        count1--;
        count2--;
    }
}

count1 = 0;
count2 = 0;

for(const value of arr)
{
    if(value === candidate1)
        count1++;
    else if(value === candidate2)
        count2++;
}

const ans = [];

if(count1 > Math.floor(n / 3))
    ans.push(candidate1);

if(count2 > Math.floor(n / 3))
    ans.push(candidate2);

ans.sort((a, b) => a - b);

console.log(ans.join(" "));
```

### Output
Input

3

3 2 3

Output

3

# Time Complexity
O(N)

# Space Complexity
O(1)

</approaches>




