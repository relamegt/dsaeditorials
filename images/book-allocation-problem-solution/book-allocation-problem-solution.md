# Book Allocation Problem - Solution

## Problem Statement

You are given an array `books` of size `N`, where `books[i]` represents the number of pages in the `i`th book. You are also given an integer `M` representing the number of students.

Allocate books to the students such that:

- Each student gets at least one book.
- Each book is allocated to exactly one student.
- The books allocated to a student must be contiguous.

Find and print the minimum possible value of the maximum number of pages assigned to any student. If allocation is not possible, print `-1`.

## Input Format

First line: Integer `N`

Second line: `N` space-separated integers representing the books array.

Third line: Integer `M`

## Output Format

Print a single integer representing the minimized maximum pages, or `-1` if allocation is not possible.

## Explanation

There are two approaches to solve this problem.

- **Approach 1:** Linear Search
- **Approach 2:** Binary Search (Optimal)

For example,

Input

4

12 34 67 90

2

Output

113

<approaches>
## Approach 1: Linear Search

### Algorithm

1. If `M > N`, print `-1`.
2. Find the maximum pages in a single book and the total pages.
3. Try every value from `maximum pages` to `total pages`.
4. For each value, allocate books greedily while keeping the pages assigned to a student within the limit.
5. The first valid value is the answer.

```C
#include <stdio.h>

int main()
{
    int n;
    scanf("%d",&n);

    long long books[n];
    long long maxi=0,sum=0;

    for(int i=0;i<n;i++)
    {
        scanf("%lld",&books[i]);
        if(books[i]>maxi)
            maxi=books[i];
        sum+=books[i];
    }

    int m;
    scanf("%d",&m);

    if(m>n)
    {
        printf("-1");
        return 0;
    }

    for(long long limit=maxi;limit<=sum;limit++)
    {
        int students=1;
        long long pages=0;

        for(int i=0;i<n;i++)
        {
            if(pages+books[i]<=limit)
                pages+=books[i];
            else
            {
                students++;
                pages=books[i];
            }
        }

        if(students<=m)
        {
            printf("%lld",limit);
            return 0;
        }
    }

    return 0;
}
```
```cpp
#include <iostream>
#include <vector>
using namespace std;

int main()
{
    int n;
    cin>>n;

    vector<long long> books(n);

    long long maxi=0,sum=0;

    for(int i=0;i<n;i++)
    {
        cin>>books[i];
        maxi=max(maxi,books[i]);
        sum+=books[i];
    }

    int m;
    cin>>m;

    if(m>n)
    {
        cout<<-1;
        return 0;
    }

    for(long long limit=maxi;limit<=sum;limit++)
    {
        int students=1;
        long long pages=0;

        for(long long x:books)
        {
            if(pages+x<=limit)
                pages+=x;
            else
            {
                students++;
                pages=x;
            }
        }

        if(students<=m)
        {
            cout<<limit;
            return 0;
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

        long[] books=new long[n];

        long maxi=0,sum=0;

        for(int i=0;i<n;i++)
        {
            books[i]=sc.nextLong();
            maxi=Math.max(maxi,books[i]);
            sum+=books[i];
        }

        int m=sc.nextInt();

        if(m>n)
        {
            System.out.print(-1);
            return;
        }

        for(long limit=maxi;limit<=sum;limit++)
        {
            int students=1;
            long pages=0;

            for(long x:books)
            {
                if(pages+x<=limit)
                    pages+=x;
                else
                {
                    students++;
                    pages=x;
                }
            }

            if(students<=m)
            {
                System.out.print(limit);
                return;
            }
        }
    }
}
```
```Python
n=int(input())

books=list(map(int,input().split()))

m=int(input())

if m>n:
    print(-1)
    exit()

low=max(books)
high=sum(books)

for limit in range(low,high+1):

    students=1
    pages=0

    for x in books:

        if pages+x<=limit:
            pages+=x
        else:
            students+=1
            pages=x

    if students<=m:
        print(limit)
        break
```
```C#
using System;

class Program
{
    static void Main()
    {
        int n=int.Parse(Console.ReadLine());

        long[] books=Array.ConvertAll(Console.ReadLine().Split(),long.Parse);

        int m=int.Parse(Console.ReadLine());

        if(m>n)
        {
            Console.Write(-1);
            return;
        }

        long low=0;
        long high=0;

        foreach(long x in books)
        {
            if(x>low)
                low=x;

            high+=x;
        }

        for(long limit=low;limit<=high;limit++)
        {
            int students=1;
            long pages=0;

            foreach(long x in books)
            {
                if(pages+x<=limit)
                    pages+=x;
                else
                {
                    students++;
                    pages=x;
                }
            }

            if(students<=m)
            {
                Console.Write(limit);
                return;
            }
        }
    }
}
```
```JavaScript
const input=require("fs").readFileSync(0,"utf8").trim().split(/\s+/).map(Number);

let idx=0;

const n=input[idx++];

const books=[];

let low=0;
let high=0;

for(let i=0;i<n;i++)
{
    books.push(input[idx]);
    low=Math.max(low,input[idx]);
    high+=input[idx];
    idx++;
}

const m=input[idx];

if(m>n)
{
    console.log(-1);
    return;
}

for(let limit=low;limit<=high;limit++)
{
    let students=1;
    let pages=0;

    for(const x of books)
    {
        if(pages+x<=limit)
            pages+=x;
        else
        {
            students++;
            pages=x;
        }
    }

    if(students<=m)
    {
        console.log(limit);
        return;
    }
}
```

### Output
Input

4

12 34 67 90

2

Output

113

# Time Complexity
O(N × TotalPages)

# Space Complexity
O(1)

## Approach 2: Binary Search (Optimal)

### Algorithm

1. If `M > N`, print `-1`.
2. Set `low` as the maximum pages in a single book and `high` as the total number of pages.
3. While `low <= high`:

- Compute `mid` as the maximum pages allowed for a student.
- Allocate books greedily.
- If the number of students required is less than or equal to `M`, store the answer and search for a smaller value.
- Otherwise, search for a larger value.

```C
#include <stdio.h>

int main()
{
    int n;
    scanf("%d",&n);

    long long books[n];
    long long low=0;
    long long high=0;

    for(int i=0;i<n;i++)
    {
        scanf("%lld",&books[i]);

        if(books[i]>low)
            low=books[i];

        high+=books[i];
    }

    int m;
    scanf("%d",&m);

    if(m>n)
    {
        printf("-1");
        return 0;
    }

    long long ans=high;

    while(low<=high)
    {
        long long mid=low+(high-low)/2;

        int students=1;
        long long pages=0;

        for(int i=0;i<n;i++)
        {
            if(pages+books[i]<=mid)
                pages+=books[i];
            else
            {
                students++;
                pages=books[i];
            }
        }

        if(students<=m)
        {
            ans=mid;
            high=mid-1;
        }
        else
        {
            low=mid+1;
        }
    }

    printf("%lld",ans);

    return 0;
}
```
```cpp
#include <iostream>
#include <vector>
using namespace std;

int main()
{
    int n;
    cin>>n;

    vector<long long> books(n);

    long long low=0;
    long long high=0;

    for(int i=0;i<n;i++)
    {
        cin>>books[i];
        low=max(low,books[i]);
        high+=books[i];
    }

    int m;
    cin>>m;

    if(m>n)
    {
        cout<<-1;
        return 0;
    }

    long long ans=high;

    while(low<=high)
    {
        long long mid=low+(high-low)/2;

        int students=1;
        long long pages=0;

        for(long long x:books)
        {
            if(pages+x<=mid)
                pages+=x;
            else
            {
                students++;
                pages=x;
            }
        }

        if(students<=m)
        {
            ans=mid;
            high=mid-1;
        }
        else
        {
            low=mid+1;
        }
    }

    cout<<ans;

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

        long[] books=new long[n];

        long low=0;
        long high=0;

        for(int i=0;i<n;i++)
        {
            books[i]=sc.nextLong();
            low=Math.max(low,books[i]);
            high+=books[i];
        }

        int m=sc.nextInt();

        if(m>n)
        {
            System.out.print(-1);
            return;
        }

        long ans=high;

        while(low<=high)
        {
            long mid=low+(high-low)/2;

            int students=1;
            long pages=0;

            for(long x:books)
            {
                if(pages+x<=mid)
                    pages+=x;
                else
                {
                    students++;
                    pages=x;
                }
            }

            if(students<=m)
            {
                ans=mid;
                high=mid-1;
            }
            else
            {
                low=mid+1;
            }
        }

        System.out.print(ans);
    }
}
```
```Python
n=int(input())

books=list(map(int,input().split()))

m=int(input())

if m>n:
    print(-1)
    exit()

low=max(books)
high=sum(books)

ans=high

while low<=high:

    mid=low+(high-low)//2

    students=1
    pages=0

    for x in books:

        if pages+x<=mid:
            pages+=x
        else:
            students+=1
            pages=x

    if students<=m:
        ans=mid
        high=mid-1
    else:
        low=mid+1

print(ans)
```
```C#
using System;

class Program
{
    static void Main()
    {
        int n=int.Parse(Console.ReadLine());

        long[] books=Array.ConvertAll(Console.ReadLine().Split(),long.Parse);

        int m=int.Parse(Console.ReadLine());

        if(m>n)
        {
            Console.Write(-1);
            return;
        }

        long low=0;
        long high=0;

        foreach(long x in books)
        {
            if(x>low)
                low=x;

            high+=x;
        }

        long ans=high;

        while(low<=high)
        {
            long mid=low+(high-low)/2;

            int students=1;
            long pages=0;

            foreach(long x in books)
            {
                if(pages+x<=mid)
                    pages+=x;
                else
                {
                    students++;
                    pages=x;
                }
            }

            if(students<=m)
            {
                ans=mid;
                high=mid-1;
            }
            else
            {
                low=mid+1;
            }
        }

        Console.Write(ans);
    }
}
```
```JavaScript
const input=require("fs").readFileSync(0,"utf8").trim().split(/\s+/).map(Number);

let idx=0;

const n=input[idx++];

const books=[];

let low=0;
let high=0;

for(let i=0;i<n;i++)
{
    books.push(input[idx]);
    low=Math.max(low,input[idx]);
    high+=input[idx];
    idx++;
}

const m=input[idx];

if(m>n)
{
    console.log(-1);
    return;
}

let ans=high;

while(low<=high)
{
    const mid=low+Math.floor((high-low)/2);

    let students=1;
    let pages=0;

    for(const x of books)
    {
        if(pages+x<=mid)
            pages+=x;
        else
        {
            students++;
            pages=x;
        }
    }

    if(students<=m)
    {
        ans=mid;
        high=mid-1;
    }
    else
    {
        low=mid+1;
    }
}

console.log(ans);
```

### Output
Input

4

12 34 67 90

2

Output

113

# Time Complexity
O(N × log(TotalPages))

# Space Complexity
O(1)

</approaches>




