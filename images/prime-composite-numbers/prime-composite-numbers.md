# Prime & Composite Numbers

In the study of integers and number systems, numbers are classified based on the number of positive divisors they possess. The two primary categories for integers greater than $1$ are **Prime Numbers** and **Composite Numbers**. These categories play a central role in number theory, arithmetic patterns, and cryptography.

---

## Core Definitions

Every integer greater than $1$ belongs to one of these two classifications:

### 1. Prime Numbers

A **Prime Number** is a positive integer greater than $1$ that has exactly two distinct positive divisors: $1$ and itself.

- *Examples*: $2, 3, 5, 7, 11, 13, 17, 19, 23, 29, 31, 37, 41, 43, 47, 53, 59, \ldots$
- *Pattern (Arrangement)*: If you have a prime number of items (like $17$ glass beads), they can only be arranged in a single row ($1 \times 17$) or in individual columns ($17 \times 1$).

### 2. Composite Numbers

A **Composite Number** is a positive integer greater than $1$ that has more than two distinct positive divisors.

- *Examples*: $4, 6, 8, 9, 10, 12, 14, 15, 16, 18, 20, 21, 22, 24, 25, 26, 27, 28, 30, \ldots$
- *Divisors*: For example, $10$ is a composite number because it is divisible by $1, 2, 5,$ and $10$.

### 3. Special Case: The Number 1

The number **$1$ is neither prime nor composite**. It has only one positive divisor ($1$ itself), violating the definition of both categories.

---

## Visualizing Prime and Composite Numbers

To see the distribution, we can map out numbers from 1 to 20:

![](https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/prime-composite-numbers/1785484902196-1.png)

---

## Key Mathematical Patterns and Properties

When analyzing prime and composite numbers, several important arithmetic patterns emerge:

### Smallest Odd Composite Number

While the smallest composite number is $4$ (which is even), the **smallest odd composite number is $9$**. 

- *Proof*: The odd numbers starting from $1$ are $1, 3, 5, 7, 9, \ldots$.
- $1$ is neither.
- $3, 5, 7$ are prime.
- $9$ is odd and has factors $1, 3,$ and $9$, making it the first odd composite number.

### Counting Primes in a Range

To count the number of primes in a range, we systematically identify and count the prime values.

- *Example (Range 40 to 60)*: There are exactly **$5$ prime numbers** between 40 and 60.
- The primes are: $41, 43, 47, 53,$ and $59$.

### Sum of Primes

Calculating the sum of primes up to a specific limit:

- *Example (Primes less than 20)*: The primes less than 20 are $2, 3, 5, 7, 11, 13, 17,$ and $19$.

  $$\text{Sum} = 2 + 3 + 5 + 7 + 11 + 13 + 17 + 19 = 77$$

### The Square Root Principle

Instead of dividing $N$ by every number up to $N-1$, you only need to test divisibility by prime numbers less than or equal to the square root of $N$ ($\sqrt{N}$). If no prime factors are found up to $\sqrt{N}$, then $N$ is prime.

#### Step-by-Step Test: Is 91 Prime or Composite?

1. Calculate $\sqrt{91}$: $\sqrt{91} \approx 9.54$.
2. List prime numbers $\le 9.54$: $\{2, 3, 5, 7\}$.
3. Test divisibility of 91 by these primes:

- $91 \div 2$ leaves a remainder.
- $91 \div 3$ leaves a remainder ($91 = 3 \times 30 + 1$).
- $91 \div 5$ leaves a remainder (ends in 1, not 0 or 5).
- $91 \div 7 = 13$ (divisible!).

1. **Conclusion**: Since 91 is divisible by $7$ ($7 \times 13 = 91$), **$91$ is a composite number**.

#### Step-by-Step Test: Is 143 Prime or Composite?

1. Calculate $\sqrt{143}$: $\sqrt{143} \approx 11.95$.
2. List prime numbers $\le 11.95$: $\{2, 3, 5, 7, 11\}$.
3. Test divisibility of 143 by these primes:

- $143$ is not divisible by $2, 3, 5,$ or $7$.
- $143 \div 11 = 13$ (divisible!).

1. **Conclusion**: Since 143 is divisible by $11$ ($11 \times 13 = 143$), **$143$ is a composite number**.

---

## Application Scenarios: Quantitative Problem Solving

Prime and composite properties are used to solve various logical reasoning and arrangement puzzles:

- **Mohit** is categorizing batches of products in a factory. He has two large shipments: one with $91$ units and another with $143$ units. He wants to know if they can be divided into smaller equal groups (other than groups of 1). By calculating the square roots ($\sqrt{91} \approx 9.54$ and $\sqrt{143} \approx 11.95$) and checking prime factors, he discovers that:
- The shipment of $91$ can be split into $7$ groups of $13$ items.
- The shipment of $143$ can be split into $11$ groups of $13$ items.

  Since both can be split into equal sub-groups, they are composite batches.

- **Akash** is playing a math puzzle game where he must find the closest prime number greater than $143$ to win a point. He tests $144$ (even, hence composite), $145$ (ends in 5, composite), $146$ (even, composite), $147$ (sum of digits $1+4+7=12$, divisible by 3, composite), and $148$ (even, composite). He then tests $149$ by dividing by primes up to $\sqrt{149} \approx 12.2$ (primes: $2, 3, 5, 7, 11$). Since $149$ is not divisible by any of these, he correctly identifies $149$ as the next prime number, winning the point.

---

## Comparison Summary Table

| Number under Test | $\le \sqrt{N}$ Primes to Check | Divisibility Result | Classification | Divisors |
| --- | --- | --- | --- | --- |
| **10** | $\{2, 3\}$ | Divisible by $2$ | Composite | $1, 2, 5, 10$ |
| **17** | $\{2, 3\}$ | Not divisible | Prime | $1, 17$ |
| **33** | $\{2, 3, 5\}$ | Divisible by $3$ | Composite | $1, 3, 11, 33$ |
| **51** | $\{2, 3, 5, 7\}$ | Divisible by $3$ | Composite | $1, 3, 17, 51$ |
| **91** | $\{2, 3, 5, 7\}$ | Divisible by $7$ | Composite | $1, 7, 13, 91$ |
| **143** | $\{2, 3, 5, 7, 11\}$ | Divisible by $11$ | Composite | $1, 11, 13, 143$ |

### ⚠️ Important: The Prime Distribution Gap

Unlike even and odd numbers, which alternate perfectly, the distribution of prime numbers is irregular. As numbers grow larger, the gap between consecutive prime numbers increases on average. This relationship is described by the **Prime Number Theorem**:

$$\pi(x) \approx \frac{x}{\ln(x)}$$

Where $\pi(x)$ represents the number of primes less than or equal to $x$. 
For software engineers using hash tables or random number generators, assuming primes are evenly spaced leads to uneven workload distribution and performance bottlenecks. Large gap offsets must be handled with step offsets when searching for the next prime capacity in memory allocation pools.

# Summary

Prime numbers possess exactly two divisors, while composite numbers have more than two. Checking if a number is prime is optimized by checking factors only up to $\sqrt{N}$. In computation, these prime/composite traits are fundamental for hash distribution structures and public-key cryptography algorithms (like RSA), where the difficulty of factoring large composite values into their prime components forms the basis of digital security.




