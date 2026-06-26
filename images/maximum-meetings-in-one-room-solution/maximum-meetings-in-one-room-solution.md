# Maximum Meetings in one room - Solution

## Problem Statement

You are given `N` meetings, where the `i`th meeting starts at `start[i]` and ends at `end[i]`. Only one meeting can be performed in the room at any time.

Find the maximum number of meetings that can be accommodated in the room.

A meeting can be chosen only if its start time is **strictly greater** than the end time of the previously selected meeting.

## Input Format

First line: Integer `N`

Second line: `N` space-separated integers representing the start times

Third line: `N` space-separated integers representing the end times

## Output Format

Print a single integer representing the maximum number of meetings that can be accommodated.

## Explanation

There is one optimal approach to solve this problem.

For example,

Input

6

1 3 0 5 8 5

2 4 6 7 9 9

Output

4

## Algorithm

1. Store each meeting as a pair `(start, end)`.
2. Sort all meetings by their ending time.
3. Select the first meeting.
4. Traverse the remaining meetings.
5. If the current meeting starts strictly after the end time of the previously selected meeting, include it.
6. Print the total number of selected meetings.

```C
#include <stdio.h>
#include <stdlib.h>

typedef struct
{
    int start;
    int end;
} Meeting;

int cmp(const void *a,const void *b)
{
    Meeting *m1=(Meeting *)a;
    Meeting *m2=(Meeting *)b;

    if(m1->end==m2->end)
        return m1->start-m2->start;

    return m1->end-m2->end;
}

int main()
{
    int n;
    scanf("%d",&n);

    Meeting meetings[n];

    for(int i=0;i<n;i++)
        scanf("%d",&meetings[i].start);

    for(int i=0;i<n;i++)
        scanf("%d",&meetings[i].end);

    qsort(meetings,n,sizeof(Meeting),cmp);

    int count=1;
    int lastEnd=meetings[0].end;

    for(int i=1;i<n;i++)
    {
        if(meetings[i].start>lastEnd)
        {
            count++;
            lastEnd=meetings[i].end;
        }
    }

    printf("%d",count);

    return 0;
}
```
```cpp
#include <iostream>
#include <vector>
#include <algorithm>
using namespace std;

struct Meeting
{
    int start,end;
};

bool cmp(Meeting a,Meeting b)
{
    if(a.end==b.end)
        return a.start<b.start;

    return a.end<b.end;
}

int main()
{
    int n;
    cin>>n;

    vector<Meeting> meetings(n);

    for(int i=0;i<n;i++)
        cin>>meetings[i].start;

    for(int i=0;i<n;i++)
        cin>>meetings[i].end;

    sort(meetings.begin(),meetings.end(),cmp);

    int count=1;
    int lastEnd=meetings[0].end;

    for(int i=1;i<n;i++)
    {
        if(meetings[i].start>lastEnd)
        {
            count++;
            lastEnd=meetings[i].end;
        }
    }

    cout<<count;

    return 0;
}
```
```Java
import java.util.*;

public class Main
{
    static class Meeting
    {
        int start,end;

        Meeting(int s,int e)
        {
            start=s;
            end=e;
        }
    }

    public static void main(String[] args)
    {
        Scanner sc=new Scanner(System.in);

        int n=sc.nextInt();

        int[] start=new int[n];
        int[] end=new int[n];

        for(int i=0;i<n;i++)
            start[i]=sc.nextInt();

        for(int i=0;i<n;i++)
            end[i]=sc.nextInt();

        Meeting[] meetings=new Meeting[n];

        for(int i=0;i<n;i++)
            meetings[i]=new Meeting(start[i],end[i]);

        Arrays.sort(meetings,(a,b)->{
            if(a.end==b.end)
                return a.start-b.start;
            return a.end-b.end;
        });

        int count=1;
        int lastEnd=meetings[0].end;

        for(int i=1;i<n;i++)
        {
            if(meetings[i].start>lastEnd)
            {
                count++;
                lastEnd=meetings[i].end;
            }
        }

        System.out.print(count);
    }
}
```
```Python
n = int(input())

start = list(map(int, input().split()))

end = list(map(int, input().split()))

meetings = []

for i in range(n):
    meetings.append((end[i], start[i]))

meetings.sort()

count = 1
lastEnd = meetings[0][0]

for e, s in meetings[1:]:

    if s > lastEnd:
        count += 1
        lastEnd = e

print(count)
```
```C#
using System;
using System.Linq;

class Program
{
    static void Main()
    {
        int n=int.Parse(Console.ReadLine());

        int[] start=Array.ConvertAll(Console.ReadLine().Split(),int.Parse);
        int[] end=Array.ConvertAll(Console.ReadLine().Split(),int.Parse);

        var meetings=new (int start,int end)[n];

        for(int i=0;i<n;i++)
            meetings[i]=(start[i],end[i]);

        Array.Sort(meetings,(a,b)=>
        {
            if(a.end==b.end)
                return a.start.CompareTo(b.start);

            return a.end.CompareTo(b.end);
        });

        int count=1;
        int lastEnd=meetings[0].end;

        for(int i=1;i<n;i++)
        {
            if(meetings[i].start>lastEnd)
            {
                count++;
                lastEnd=meetings[i].end;
            }
        }

        Console.Write(count);
    }
}
```
```JavaScript
const input=require("fs").readFileSync(0,"utf8").trim().split(/\s+/).map(Number);

let idx=0;

const n=input[idx++];

const start=[];

for(let i=0;i<n;i++)
    start.push(input[idx++]);

const end=[];

for(let i=0;i<n;i++)
    end.push(input[idx++]);

const meetings=[];

for(let i=0;i<n;i++)
    meetings.push({start:start[i],end:end[i]});

meetings.sort((a,b)=>{
    if(a.end===b.end)
        return a.start-b.start;

    return a.end-b.end;
});

let count=1;
let lastEnd=meetings[0].end;

for(let i=1;i<n;i++)
{
    if(meetings[i].start>lastEnd)
    {
        count++;
        lastEnd=meetings[i].end;
    }
}

console.log(count);
```

### Output
Input

6

1 3 0 5 8 5

2 4 6 7 9 9

Output

4

# Time Complexity
O(N log N)

# Space Complexity
O(N)




