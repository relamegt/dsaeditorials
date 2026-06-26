# Common Elements in All Rows of a Matrix - Solution

## Problem Statement

Given a matrix of size `N × M`, find all distinct elements that are present in every row of the matrix.

Print the common elements in increasing order.

If no such element exists, print `-1`.

## Input Format

First line: Two integers `N` and `M`.

Next `N` lines: `M` space-separated integers representing the matrix.

## Output Format

Print all distinct common elements in increasing order as space-separated integers.

If there is no common element, print `-1`.

## Explanation

There is one optimal approach to solve this problem.

For example,

Input

4 5

1 2 1 4 8

3 7 8 5 1

8 7 7 3 1

8 1 2 7 9

Output

1 8

## Algorithm

1. Read the matrix.
2. Store all distinct elements of the first row in a map with count `1`.
3. For every remaining row, use a set to avoid counting duplicate elements within the same row.
4. If an element exists in the map and has been seen in all previous rows, increment its count.
5. After processing all rows, print all elements whose count equals `N` in increasing order.
6. If no such element exists, print `-1`.

```C
#include <stdio.h>
#include <stdlib.h>

typedef struct
{
    long long value;
    int count;
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

    Node arr[1000000];
    int size=0;

    for(int j=0;j<m;j++)
    {
        long long x;
        scanf("%lld",&x);

        int found=0;

        for(int k=0;k<size;k++)
        {
            if(arr[k].value==x)
            {
                found=1;
                break;
            }
        }

        if(!found)
        {
            arr[size].value=x;
            arr[size].count=1;
            size++;
        }
    }

    for(int i=1;i<n;i++)
    {
        long long seen[1000];
        int seenSize=0;

        for(int j=0;j<m;j++)
        {
            long long x;
            scanf("%lld",&x);

            int ok=0;

            for(int t=0;t<seenSize;t++)
            {
                if(seen[t]==x)
                {
                    ok=1;
                    break;
                }
            }

            if(ok)
                continue;

            seen[seenSize++]=x;

            for(int k=0;k<size;k++)
            {
                if(arr[k].value==x && arr[k].count==i)
                {
                    arr[k].count++;
                    break;
                }
            }
        }
    }

    qsort(arr,size,sizeof(Node),cmp);

    int found=0;

    for(int i=0;i<size;i++)
    {
        if(arr[i].count==n)
        {
            printf("%lld ",arr[i].value);
            found=1;
        }
    }

    if(!found)
        printf("-1");

    return 0;
}
```
```cpp
#include <iostream>
#include <map>
#include <set>
using namespace std;

int main()
{
    int n,m;
    cin>>n>>m;

    map<long long,int> cnt;

    for(int j=0;j<m;j++)
    {
        long long x;
        cin>>x;
        cnt[x]=1;
    }

    for(int i=1;i<n;i++)
    {
        set<long long> seen;

        for(int j=0;j<m;j++)
        {
            long long x;
            cin>>x;

            if(seen.count(x))
                continue;

            seen.insert(x);

            if(cnt[x]==i)
                cnt[x]++;
        }
    }

    bool found=false;

    for(auto x:cnt)
    {
        if(x.second==n)
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

        for(int j=0;j<m;j++)
        {
            long x=sc.nextLong();
            map.put(x,1);
        }

        for(int i=1;i<n;i++)
        {
            HashSet<Long> seen=new HashSet<>();

            for(int j=0;j<m;j++)
            {
                long x=sc.nextLong();

                if(seen.contains(x))
                    continue;

                seen.add(x);

                if(map.getOrDefault(x,0)==i)
                    map.put(x,i+1);
            }
        }

        boolean found=false;

        for(Map.Entry<Long,Integer> e:map.entrySet())
        {
            if(e.getValue()==n)
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

count={}

first=set(map(int,input().split()))

for x in first:
    count[x]=1

for i in range(1,n):

    row=set(map(int,input().split()))

    for x in row:
        if count.get(x,0)==i:
            count[x]=i+1

ans=[]

for x in sorted(count):
    if count[x]==n:
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

        long[] row=Array.ConvertAll(Console.ReadLine().Split(),long.Parse);

        HashSet<long> firstSet=new HashSet<long>(row);

        foreach(long x in firstSet)
            map[x]=1;

        for(int i=1;i<n;i++)
        {
            HashSet<long> seen=new HashSet<long>();

            row=Array.ConvertAll(Console.ReadLine().Split(),long.Parse);

            foreach(long x in row)
            {
                if(seen.Contains(x))
                    continue;

                seen.Add(x);

                if(map.ContainsKey(x) && map[x]==i)
                    map[x]=i+1;
            }
        }

        bool found=false;

        foreach(var x in map)
        {
            if(x.Value==n)
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

let first=new Set();

for(let j=0;j<m;j++)
    first.add(input[idx++]);

for(const x of first)
    map.set(x,1);

for(let i=1;i<n;i++)
{
    let seen=new Set();

    for(let j=0;j<m;j++)
    {
        const x=input[idx++];

        if(seen.has(x))
            continue;

        seen.add(x);

        if((map.get(x)||0)===i)
            map.set(x,i+1);
    }
}

const ans=[];

for(const [k,v] of [...map.entries()].sort((a,b)=>a[0]-b[0]))
{
    if(v===n)
        ans.push(k);
}

if(ans.length)
    console.log(ans.join(" "));
else
    console.log(-1);
```

### Output
Input

4 5

1 2 1 4 8

3 7 8 5 1

8 7 7 3 1

8 1 2 7 9

Output

1 8

# Time Complexity
O(N × M)

# Space Complexity
O(M)




