# Check Subset - Solution

## Problem Statement

Given two arrays `A` and `B`, determine whether array `B` is a subset of array `A`.

An array `B` is considered a subset of array `A` if every element of `B` appears in `A` at least as many times as it appears in `B`.

## Input Format

First line: Two integers `N` and `M`.

Second line: `N` space-separated integers representing array `A`.

Third line: `M` space-separated integers representing array `B`.

## Output Format

Print `YES` if `B` is a subset of `A`.

Otherwise, print `NO`.

## Explanation

There are two approaches to solve this problem.

- Approach 1: Sorting
- Approach 2: Hash Map (Optimal)

For example,

Input

6 4

11 1 13 21 3 7

11 3 7 1

Output

YES

<approaches>
## Approach 1: Sorting

### Algorithm

1. Read both arrays.
2. Sort both arrays.
3. Traverse both arrays using two pointers.
4. If all elements of `B` are matched, print `YES`.
5. Otherwise, print `NO`.

```C
#include <stdio.h>
#include <stdlib.h>

int cmp(const void *a,const void *b)
{
    long long x=*(long long*)a;
    long long y=*(long long*)b;

    if(x<y) return -1;
    if(x>y) return 1;
    return 0;
}

int main()
{
    int n,m;
    scanf("%d%d",&n,&m);

    long long a[n],b[m];

    for(int i=0;i<n;i++)
        scanf("%lld",&a[i]);

    for(int i=0;i<m;i++)
        scanf("%lld",&b[i]);

    qsort(a,n,sizeof(long long),cmp);
    qsort(b,m,sizeof(long long),cmp);

    int i=0,j=0;

    while(i<n && j<m)
    {
        if(a[i]==b[j])
        {
            i++;
            j++;
        }
        else if(a[i]<b[j])
            i++;
        else
        {
            printf("NO");
            return 0;
        }
    }

    if(j==m)
        printf("YES");
    else
        printf("NO");

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
    int n,m;
    cin>>n>>m;

    vector<long long> a(n),b(m);

    for(int i=0;i<n;i++)
        cin>>a[i];

    for(int i=0;i<m;i++)
        cin>>b[i];

    sort(a.begin(),a.end());
    sort(b.begin(),b.end());

    int i=0,j=0;

    while(i<n && j<m)
    {
        if(a[i]==b[j])
        {
            i++;
            j++;
        }
        else if(a[i]<b[j])
            i++;
        else
        {
            cout<<"NO";
            return 0;
        }
    }

    cout<<(j==m?"YES":"NO");

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
        int m=sc.nextInt();

        long[] a=new long[n];
        long[] b=new long[m];

        for(int i=0;i<n;i++)
            a[i]=sc.nextLong();

        for(int i=0;i<m;i++)
            b[i]=sc.nextLong();

        Arrays.sort(a);
        Arrays.sort(b);

        int i=0,j=0;

        while(i<n && j<m)
        {
            if(a[i]==b[j])
            {
                i++;
                j++;
            }
            else if(a[i]<b[j])
                i++;
            else
            {
                System.out.print("NO");
                return;
            }
        }

        System.out.print(j==m?"YES":"NO");
    }
}
```
```Python
n,m=map(int,input().split())

a=list(map(int,input().split()))
b=list(map(int,input().split()))

a.sort()
b.sort()

i=j=0

while i<n and j<m:
    if a[i]==b[j]:
        i+=1
        j+=1
    elif a[i]<b[j]:
        i+=1
    else:
        print("NO")
        exit()

print("YES" if j==m else "NO")
```
```C#
using System;

class Program
{
    static void Main()
    {
        string[] first=Console.ReadLine().Split();

        int n=int.Parse(first[0]);
        int m=int.Parse(first[1]);

        long[] a=Array.ConvertAll(Console.ReadLine().Split(),long.Parse);
        long[] b=Array.ConvertAll(Console.ReadLine().Split(),long.Parse);

        Array.Sort(a);
        Array.Sort(b);

        int i=0,j=0;

        while(i<n && j<m)
        {
            if(a[i]==b[j])
            {
                i++;
                j++;
            }
            else if(a[i]<b[j])
                i++;
            else
            {
                Console.Write("NO");
                return;
            }
        }

        Console.Write(j==m?"YES":"NO");
    }
}
```
```JavaScript
const input=require("fs").readFileSync(0,"utf8").trim().split(/\s+/).map(Number);

let idx=0;

const n=input[idx++];
const m=input[idx++];

const a=[];
const b=[];

for(let i=0;i<n;i++)
    a.push(input[idx++]);

for(let i=0;i<m;i++)
    b.push(input[idx++]);

a.sort((x,y)=>x-y);
b.sort((x,y)=>x-y);

let i=0,j=0;

while(i<n && j<m)
{
    if(a[i]===b[j])
    {
        i++;
        j++;
    }
    else if(a[i]<b[j])
        i++;
    else
    {
        console.log("NO");
        return;
    }
}

console.log(j===m?"YES":"NO");
```

### Output
Input

6 4

11 1 13 21 3 7

11 3 7 1

Output

YES

# Time Complexity
O(N log N + M log M)

# Space Complexity
O(N + M)

## Approach 2: Hash Map (Optimal)

### Algorithm

1. Read both arrays.
2. Store the frequency of every element of array `A` in a hash map.
3. Traverse array `B`.
4. For each element, check whether it exists in the map with a positive frequency.
5. If not, print `NO`.
6. Otherwise, decrease its frequency.
7. If all elements are processed successfully, print `YES`.

```C
#include <stdio.h>
#include <stdlib.h>

#define SIZE 2000003

typedef struct Node
{
    long long key;
    int count;
    struct Node *next;
}Node;

Node *table[SIZE];

int hash(long long x)
{
    if(x<0)
        x=-x;
    return x%SIZE;
}

Node* find(Node *head,long long key)
{
    while(head)
    {
        if(head->key==key)
            return head;
        head=head->next;
    }
    return NULL;
}

int main()
{
    int n,m;
    scanf("%d%d",&n,&m);

    for(int i=0;i<n;i++)
    {
        long long x;
        scanf("%lld",&x);

        int h=hash(x);
        Node *node=find(table[h],x);

        if(node)
            node->count++;
        else
        {
            node=(Node*)malloc(sizeof(Node));
            node->key=x;
            node->count=1;
            node->next=table[h];
            table[h]=node;
        }
    }

    for(int i=0;i<m;i++)
    {
        long long x;
        scanf("%lld",&x);

        int h=hash(x);
        Node *node=find(table[h],x);

        if(node==NULL || node->count==0)
        {
            printf("NO");
            return 0;
        }

        node->count--;
    }

    printf("YES");

    return 0;
}
```
```cpp
#include <iostream>
#include <unordered_map>
using namespace std;

int main()
{
    int n,m;
    cin>>n>>m;

    unordered_map<long long,int> freq;

    for(int i=0;i<n;i++)
    {
        long long x;
        cin>>x;
        freq[x]++;
    }

    for(int i=0;i<m;i++)
    {
        long long x;
        cin>>x;

        if(freq[x]==0)
        {
            cout<<"NO";
            return 0;
        }

        freq[x]--;
    }

    cout<<"YES";

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
        int m=sc.nextInt();

        HashMap<Long,Integer> freq=new HashMap<>();

        for(int i=0;i<n;i++)
        {
            long x=sc.nextLong();
            freq.put(x,freq.getOrDefault(x,0)+1);
        }

        for(int i=0;i<m;i++)
        {
            long x=sc.nextLong();

            if(!freq.containsKey(x) || freq.get(x)==0)
            {
                System.out.print("NO");
                return;
            }

            freq.put(x,freq.get(x)-1);
        }

        System.out.print("YES");
    }
}
```
```Python
n,m=map(int,input().split())

from collections import Counter

freq=Counter(map(int,input().split()))

b=list(map(int,input().split()))

for x in b:
    if freq[x]==0:
        print("NO")
        exit()
    freq[x]-=1

print("YES")
```
```C#
using System;
using System.Collections.Generic;

class Program
{
    static void Main()
    {
        string[] first=Console.ReadLine().Split();

        int n=int.Parse(first[0]);
        int m=int.Parse(first[1]);

        Dictionary<long,int> freq=new Dictionary<long,int>();

        long[] a=Array.ConvertAll(Console.ReadLine().Split(),long.Parse);

        foreach(long x in a)
        {
            if(freq.ContainsKey(x))
                freq[x]++;
            else
                freq[x]=1;
        }

        long[] b=Array.ConvertAll(Console.ReadLine().Split(),long.Parse);

        foreach(long x in b)
        {
            if(!freq.ContainsKey(x) || freq[x]==0)
            {
                Console.Write("NO");
                return;
            }

            freq[x]--;
        }

        Console.Write("YES");
    }
}
```
```JavaScript
const input=require("fs").readFileSync(0,"utf8").trim().split(/\s+/).map(Number);

let idx=0;

const n=input[idx++];
const m=input[idx++];

const freq=new Map();

for(let i=0;i<n;i++)
{
    const x=input[idx++];
    freq.set(x,(freq.get(x)||0)+1);
}

for(let i=0;i<m;i++)
{
    const x=input[idx++];

    if(!freq.has(x) || freq.get(x)===0)
    {
        console.log("NO");
        return;
    }

    freq.set(x,freq.get(x)-1);
}

console.log("YES");
```

### Output
Input

6 4

11 1 13 21 3 7

11 3 7 1

Output

YES

# Time Complexity
O(N + M)

# Space Complexity
O(N)

</approaches>




