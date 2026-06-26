# Merge Intervals - Solution

## Problem Statement

Given `N` intervals, merge all overlapping intervals and print the resulting non-overlapping intervals in increasing order of start time.

Two intervals overlap if they share at least one common point.

## Input Format

First line: Integer `N`

Next `N` lines: Two space-separated integers `start` and `end` representing an interval.

## Output Format

Print the merged intervals, one per line, in the format:

`start end`

## Explanation

There are two approaches to solve this problem.

- **Approach 1:** Brute Force
- **Approach 2:** Sort and Merge (Optimal)

For example,

Input

4

1 3

2 6

8 10

15 18

Output

1 6

8 10

15 18

<approaches>
## Approach 1: Brute Force

### Algorithm

1. Sort all intervals based on their starting value.
2. Traverse every interval one by one.
3. For each interval, keep extending its ending value while the next interval overlaps.
4. Store the merged interval.
5. Repeat until all intervals are processed.

```C
#include <stdio.h>
#include <stdlib.h>

typedef struct
{
    int start;
    int end;
} Interval;

int cmp(const void *a,const void *b)
{
    return ((Interval *)a)->start-((Interval *)b)->start;
}

int main()
{
    int n;
    scanf("%d",&n);

    Interval arr[n];

    for(int i=0;i<n;i++)
        scanf("%d%d",&arr[i].start,&arr[i].end);

    qsort(arr,n,sizeof(Interval),cmp);

    for(int i=0;i<n;i++)
    {
        int start=arr[i].start;
        int end=arr[i].end;

        if(i>0 && start<=arr[i-1].end)
            continue;

        for(int j=i+1;j<n;j++)
        {
            if(arr[j].start<=end)
            {
                if(arr[j].end>end)
                    end=arr[j].end;
            }
            else
                break;
        }

        printf("%d %d",start,end);
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

    vector<pair<int,int>> intervals(n);

    for(int i=0;i<n;i++)
        cin>>intervals[i].first>>intervals[i].second;

    sort(intervals.begin(),intervals.end());

    for(int i=0;i<n;i++)
    {
        int start=intervals[i].first;
        int end=intervals[i].second;

        if(i>0 && start<=intervals[i-1].second)
            continue;

        for(int j=i+1;j<n;j++)
        {
            if(intervals[j].first<=end)
                end=max(end,intervals[j].second);
            else
                break;
        }

        cout<<start<<" "<<end<<"
";
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

        int[][] arr=new int[n][2];

        for(int i=0;i<n;i++)
        {
            arr[i][0]=sc.nextInt();
            arr[i][1]=sc.nextInt();
        }

        Arrays.sort(arr,(a,b)->a[0]-b[0]);

        for(int i=0;i<n;i++)
        {
            int start=arr[i][0];
            int end=arr[i][1];

            if(i>0 && start<=arr[i-1][1])
                continue;

            for(int j=i+1;j<n;j++)
            {
                if(arr[j][0]<=end)
                    end=Math.max(end,arr[j][1]);
                else
                    break;
            }

            System.out.println(start+" "+end);
        }
    }
}
```
```Python
n = int(input())

intervals = []

for _ in range(n):
    intervals.append(list(map(int, input().split())))

intervals.sort()

for i in range(n):

    start = intervals[i][0]
    end = intervals[i][1]

    if i > 0 and start <= intervals[i - 1][1]:
        continue

    for j in range(i + 1, n):

        if intervals[j][0] <= end:
            end = max(end, intervals[j][1])
        else:
            break

    print(start, end)
```
```C#
using System;
using System.Linq;

class Program
{
    static void Main()
    {
        int n=int.Parse(Console.ReadLine());

        int[][] arr=new int[n][];

        for(int i=0;i<n;i++)
            arr[i]=Array.ConvertAll(Console.ReadLine().Split(),int.Parse);

        arr=arr.OrderBy(x=>x[0]).ToArray();

        for(int i=0;i<n;i++)
        {
            int start=arr[i][0];
            int end=arr[i][1];

            if(i>0 && start<=arr[i-1][1])
                continue;

            for(int j=i+1;j<n;j++)
            {
                if(arr[j][0]<=end)
                    end=Math.Max(end,arr[j][1]);
                else
                    break;
            }

            Console.WriteLine(start+" "+end);
        }
    }
}
```
```JavaScript
const input=require("fs").readFileSync(0,"utf8").trim().split(/\s+/).map(Number);

let idx=0;

const n=input[idx++];

const intervals=[];

for(let i=0;i<n;i++)
    intervals.push([input[idx++],input[idx++]]);

intervals.sort((a,b)=>a[0]-b[0]);

for(let i=0;i<n;i++)
{
    let start=intervals[i][0];
    let end=intervals[i][1];

    if(i>0 && start<=intervals[i-1][1])
        continue;

    for(let j=i+1;j<n;j++)
    {
        if(intervals[j][0]<=end)
            end=Math.max(end,intervals[j][1]);
        else
            break;
    }

    console.log(start+" "+end);
}
```

### Output
Input

4

1 3

2 6

8 10

15 18

Output

1 6

8 10

15 18

# Time Complexity
O(N²) (after sorting)

# Space Complexity
O(1) (excluding sorting space)

## Approach 2: Sort and Merge (Optimal)

### Algorithm

1. Sort all intervals based on their starting value.
2. Add the first interval to the answer.
3. Traverse the remaining intervals.
4. If the current interval overlaps with the last merged interval, update the ending value.
5. Otherwise, add the current interval as a new merged interval.
6. Print all merged intervals.

```C
#include <stdio.h>
#include <stdlib.h>

typedef struct
{
    int start;
    int end;
} Interval;

int cmp(const void *a,const void *b)
{
    return ((Interval *)a)->start-((Interval *)b)->start;
}

int main()
{
    int n;
    scanf("%d",&n);

    Interval arr[n];

    for(int i=0;i<n;i++)
        scanf("%d%d",&arr[i].start,&arr[i].end);

    qsort(arr,n,sizeof(Interval),cmp);

    Interval ans[n];
    int size=0;

    ans[size++]=arr[0];

    for(int i=1;i<n;i++)
    {
        if(arr[i].start<=ans[size-1].end)
        {
            if(arr[i].end>ans[size-1].end)
                ans[size-1].end=arr[i].end;
        }
        else
        {
            ans[size++]=arr[i];
        }
    }

    for(int i=0;i<size;i++)
        printf("%d %d",ans[i].start,ans[i].end);

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

    vector<pair<int,int>> intervals(n);

    for(int i=0;i<n;i++)
        cin>>intervals[i].first>>intervals[i].second;

    sort(intervals.begin(),intervals.end());

    vector<pair<int,int>> ans;

    ans.push_back(intervals[0]);

    for(int i=1;i<n;i++)
    {
        if(intervals[i].first<=ans.back().second)
        {
            ans.back().second=max(ans.back().second,intervals[i].second);
        }
        else
        {
            ans.push_back(intervals[i]);
        }
    }

    for(auto interval:ans)
        cout<<interval.first<<" "<<interval.second<<"
";

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

        int[][] arr=new int[n][2];

        for(int i=0;i<n;i++)
        {
            arr[i][0]=sc.nextInt();
            arr[i][1]=sc.nextInt();
        }

        Arrays.sort(arr,(a,b)->a[0]-b[0]);

        List<int[]> ans=new ArrayList<>();

        ans.add(new int[]{arr[0][0],arr[0][1]});

        for(int i=1;i<n;i++)
        {
            int[] last=ans.get(ans.size()-1);

            if(arr[i][0]<=last[1])
            {
                last[1]=Math.max(last[1],arr[i][1]);
            }
            else
            {
                ans.add(new int[]{arr[i][0],arr[i][1]});
            }
        }

        for(int[] interval:ans)
            System.out.println(interval[0]+" "+interval[1]);
    }
}
```
```Python
n = int(input())

intervals = []

for _ in range(n):
    intervals.append(list(map(int, input().split())))

intervals.sort()

ans = [intervals[0]]

for start, end in intervals[1:]:

    if start <= ans[-1][1]:
        ans[-1][1] = max(ans[-1][1], end)
    else:
        ans.append([start, end])

for interval in ans:
    print(interval[0], interval[1])
```
```C#
using System;
using System.Collections.Generic;
using System.Linq;

class Program
{
    static void Main()
    {
        int n=int.Parse(Console.ReadLine());

        int[][] arr=new int[n][];

        for(int i=0;i<n;i++)
            arr[i]=Array.ConvertAll(Console.ReadLine().Split(),int.Parse);

        arr=arr.OrderBy(x=>x[0]).ToArray();

        List<int[]> ans=new List<int[]>();

        ans.Add(new int[]{arr[0][0],arr[0][1]});

        for(int i=1;i<n;i++)
        {
            int[] last=ans[ans.Count-1];

            if(arr[i][0]<=last[1])
            {
                last[1]=Math.Max(last[1],arr[i][1]);
            }
            else
            {
                ans.Add(new int[]{arr[i][0],arr[i][1]});
            }
        }

        foreach(var interval in ans)
            Console.WriteLine(interval[0]+" "+interval[1]);
    }
}
```
```JavaScript
const input=require("fs").readFileSync(0,"utf8").trim().split(/\s+/).map(Number);

let idx=0;

const n=input[idx++];

const intervals=[];

for(let i=0;i<n;i++)
    intervals.push([input[idx++],input[idx++]]);

intervals.sort((a,b)=>a[0]-b[0]);

const ans=[intervals[0]];

for(let i=1;i<n;i++)
{
    const last=ans[ans.length-1];

    if(intervals[i][0]<=last[1])
    {
        last[1]=Math.max(last[1],intervals[i][1]);
    }
    else
    {
        ans.push(intervals[i]);
    }
}

for(const interval of ans)
    console.log(interval[0]+" "+interval[1]);
```

### Output
Input

4

1 3

2 6

8 10

15 18

Output

1 6

8 10

15 18

# Time Complexity
O(N log N)

# Space Complexity
O(N)

</approaches>




