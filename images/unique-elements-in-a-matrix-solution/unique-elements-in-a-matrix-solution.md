# Unique Elements in a Matrix - Solution

## Problem Statement

Given a matrix of size `N × M`, find all elements that appear exactly once in the entire matrix.

Print the unique elements in increasing order.

If no such element exists, print `-1`.

## Input Format

First line: Two integers `N` and `M`.

Next `N` lines: `M` space-separated integers representing the matrix.

## Output Format

Print all elements that occur exactly once in the matrix, in increasing order, as space-separated integers.

If there is no unique element, print `-1`.

## Explanation

There is one optimal approach to solve this problem.

For example,

Input

3 4

1 2 3 1

3 4 5 6

7 8 2 9

Output

4 5 6 7 8 9

## Algorithm

1. Read all matrix elements.
2. Store the frequency of every element using a map.
3. Store all distinct elements.
4. Sort the distinct elements.
5. Print only those whose frequency is exactly `1`.
6. If none exists, print `-1`.

```C
#include <stdio.h>
#include <stdlib.h>

typedef struct
{
    long long value;
    int freq;
} Node;

int cmp(const void *a,const void *b)
{
    long long x=((Node*)a)->value;
    long long y=((Node*)b)->value;

    if(x<y) return -1;
    if(x>y) return 1;
    return 0;
}

int main()
{
    int n,m;
    scanf("%d%d",&n,&m);

    int size=n*m;

    Node *arr=(Node*)malloc(size*sizeof(Node));
    int count=0;

    for(int i=0;i<n;i++)
    {
        for(int j=0;j<m;j++)
        {
            long long x;
            scanf("%lld",&x);

            int found=0;

            for(int k=0;k<count;k++)
            {
                if(arr[k].value==x)
                {
                    arr[k].freq++;
                    found=1;
                    break;
                }
            }

            if(!found)
            {
                arr[count].value=x;
                arr[count].freq=1;
                count++;
            }
        }
    }

    qsort(arr,count,sizeof(Node),cmp);

    int ok=0;

    for(int i=0;i<count;i++)
    {
        if(arr[i].freq==1)
        {
            printf("%lld ",arr[i].value);
            ok=1;
        }
    }

    if(!ok)
        printf("-1");

    free(arr);

    return 0;
}
```
```cpp
#include <iostream>
#include <map>
using namespace std;

int main()
{
    int n,m;
    cin>>n>>m;

    map<long long,int> freq;

    for(int i=0;i<n;i++)
    {
        for(int j=0;j<m;j++)
        {
            long long x;
            cin>>x;
            freq[x]++;
        }
    }

    bool found=false;

    for(auto x:freq)
    {
        if(x.second==1)
        {
            cout<<x.first<<" ";
            found=true;
        }
    }

    if(!found)
        cout<<-1;

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

        TreeMap<Long,Integer> map=new TreeMap<>();

        for(int i=0;i<n;i++)
        {
            for(int j=0;j<m;j++)
            {
                long x=sc.nextLong();
                map.put(x,map.getOrDefault(x,0)+1);
            }
        }

        boolean found=false;

        for(Map.Entry<Long,Integer> e:map.entrySet())
        {
            if(e.getValue()==1)
            {
                System.out.print(e.getKey()+" ");
                found=true;
            }
        }

        if(!found)
            System.out.print(-1);
    }
}
```
```Python
n,m=map(int,input().split())

freq={}

for _ in range(n):

    row=list(map(int,input().split()))

    for x in row:
        freq[x]=freq.get(x,0)+1

ans=[]

for x in sorted(freq):

    if freq[x]==1:
        ans.append(x)

if ans:
    print(*ans)
else:
    print(-1)
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

        SortedDictionary<long,int> map=new SortedDictionary<long,int>();

        for(int i=0;i<n;i++)
        {
            long[] row=Array.ConvertAll(Console.ReadLine().Split(),long.Parse);

            foreach(long x in row)
            {
                if(map.ContainsKey(x))
                    map[x]++;
                else
                    map[x]=1;
            }
        }

        bool found=false;

        foreach(var x in map)
        {
            if(x.Value==1)
            {
                Console.Write(x.Key+" ");
                found=true;
            }
        }

        if(!found)
            Console.Write(-1);
    }
}
```
```JavaScript
const input=require("fs").readFileSync(0,"utf8").trim().split(/\s+/).map(Number);

let idx=0;

const n=input[idx++];
const m=input[idx++];

const map=new Map();

for(let i=0;i<n*m;i++)
{
    const x=input[idx++];
    map.set(x,(map.get(x)||0)+1);
}

const ans=[...map.entries()]
.sort((a,b)=>a[0]-b[0])
.filter(x=>x[1]===1)
.map(x=>x[0]);

if(ans.length===0)
    console.log(-1);
else
    console.log(ans.join(" "));
```

### Output
Input

3 4

1 2 3 1

3 4 5 6

7 8 2 9

Output

4 5 6 7 8 9

# Time Complexity
O(N × M log(N × M))

# Space Complexity
O(N × M)




