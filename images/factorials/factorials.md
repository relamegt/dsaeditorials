# Factorials

In mathematics and quantitative analysis, a **Factorial** is the product of all positive integers less than or equal to a given positive integer $n$. Factorials are represented by the exclamation mark symbol ($n!$) and serve as a cornerstone for permutations, combinations, and probability calculations.

---

## Core Definitions

### Factorial Expansion

For any positive integer $n$:
$$n! = n \times (n-1) \times (n-2) \times \dots \times 3 \times 2 \times 1$$

- *Example*: $5! = 5 \times 4 \times 3 \times 2 \times 1 = 120$.

### Special Case: Zero Factorial

By mathematical convention:
$$0! = 1$$
This definition ensures that algebraic formulas in combinatorics (such as $_nC_r$) behave consistently for edge cases.

---

## Infographic: Legendre's Formula & Trailing Zeros

The following diagram illustrates the two most important computational rules of factorials:

![](https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/factorials/1785485445536-1.png)

---

## Legendre's Formula: Exponent of a Prime in $n!$

To find the highest power of a prime number $p$ that divides $n!$ completely without remainder, we use **Legendre's Formula**:

$$E_p(n!) = \sum_{k=1}^{\infty} \left\lfloor \frac{n}{p^k} \right\rfloor = \left\lfloor \frac{n}{p} \right\rfloor + \left\lfloor \frac{n}{p^2} \right\rfloor + \left\lfloor \frac{n}{p^3} \right\rfloor + \dots$$

Where $\lfloor x \rfloor$ represents the Greatest Integer Function (rounds $x$ down to the nearest integer). The summation terminates when $p^k &gt; n$.

### Step-by-Step Exponent Calculations

#### 1. Find the Highest Power of 2 dividing $8!$

- Calculate the terms:
- $\lfloor 8/2^1 \rfloor = \lfloor 8/2 \rfloor = 4$
- $\lfloor 8/2^2 \rfloor = \lfloor 8/4 \rfloor = 2$
- $\lfloor 8/2^3 \rfloor = \lfloor 8/8 \rfloor = 1$
- Since $2^4 = 16 &gt; 8$, further terms are 0.
- Sum the values:

  $$E_2(8!) = 4 + 2 + 1 = 7$$

- **Conclusion**: The highest power of $2$ that divides $8!$ completely is $2^7$ (or $128$).

#### 2. Find the Highest Power of 3 dividing $40!$

- Calculate the terms:
- $\lfloor 40/3^1 \rfloor = \lfloor 40/3 \rfloor = 13$
- $\lfloor 40/3^2 \rfloor = \lfloor 40/9 \rfloor = 4$
- $\lfloor 40/3^3 \rfloor = \lfloor 40/27 \rfloor = 1$
- Sum the values:

  $$E_3(40!) = 13 + 4 + 1 = 18$$

- **Conclusion**: The highest power of $3$ that divides $40!$ completely is $3^{18}$.

#### 3. Find the Highest Power of 5 dividing $75!$

- Calculate the terms:
- $\lfloor 75/5^1 \rfloor = \lfloor 75/5 \rfloor = 15$
- $\lfloor 75/5^2 \rfloor = \lfloor 75/25 \rfloor = 3$
- Sum the values:

  $$E_5(75!) = 15 + 3 = 18$$

- **Conclusion**: The highest power of $5$ that divides $75!$ completely is $5^{18}$.

---

## Trailing Zeros in Factorials

A trailing zero is formed when a number is multiplied by $10$. The prime factors of $10$ are $2$ and $5$. 

- In any factorial $n!$, the prime factor $2$ appears far more frequently than the prime factor $5$.
- Therefore, the number of trailing zeros in $n!$ is determined entirely by the **highest power of 5** that divides $n!$.

$$\text{Trailing Zeros in } n! = E_5(n!) = \left\lfloor \frac{n}{5} \right\rfloor + \left\lfloor \frac{n}{25} \right\rfloor + \left\lfloor \frac{n}{125} \right\rfloor + \dots$$

### Examples: Counting Trailing Zeros

#### Trailing Zeros in $25!$

- Calculate the power of 5:

  $$\text{Zeros} = \lfloor 25/5 \rfloor + \lfloor 25/25 \rfloor = 5 + 1 = 6$$

- **Conclusion**: $25!$ ends with exactly $6$ trailing zeros.

#### Trailing Zeros in $50!$

- Calculate the power of 5:

  $$\text{Zeros} = \lfloor 50/5 \rfloor + \lfloor 50/25 \rfloor = 10 + 2 = 12$$

- **Conclusion**: $50!$ ends with exactly $12$ trailing zeros.

#### Trailing Zeros in $100!$

- Calculate the power of 5:

  $$\text{Zeros} = \lfloor 100/5 \rfloor + \lfloor 100/25 \rfloor = 20 + 4 = 24$$

- **Conclusion**: $100!$ ends with exactly $24$ trailing zeros.

---

## Prime Factors of Factorials

The prime factors of $n!$ are all prime numbers less than or equal to $n$.

### 1. Largest Prime Factor

*Problem*: What is the largest prime number that divides $10!$?

- Since $10! = 10 \times 9 \times 8 \times 7 \times 6 \times 5 \times 4 \times 3 \times 2 \times 1$, its factors are composed of prime numbers $\le 10$.
- The prime numbers less than or equal to $10$ are $\{2, 3, 5, 7\}$.
- The largest prime in this set is $7$.

### 2. Sum of Prime Factors

*Problem*: What is the sum of all prime factors of $5!$?

- $5! = 120 = 2^3 \times 3 \times 5$.
- The prime factors are $\{2, 3, 5\}$.
- Summing these prime values:

  $$\text{Sum} = 2 + 3 + 5 = 10$$

---

## Divisibility of Factorial Expressions

### Factoring Expressions

*Problem*: What is the highest power of $17$ that divides the expression $(15! + 16!)$?

1. Simplify the expression by factoring out $15!$:

   $$15! + 16! = 15! \times (1 + 16) = 15! \times 17$$

1. Determine divisibility by $17$:

- $17$ is a prime number.
- Since $15!$ is the product of numbers from $1$ to $15$, it contains no factor of $17$ (as $17 &gt; 15$).
- Therefore, the prime $17$ appears exactly once in the product expression $15! \times 17^1$.

1. **Conclusion**: The highest power of $17$ that divides $(15! + 16!)$ is $1$.

### Exponents of Composite Divisors

*Problem*: What is the highest power of $12$ that divides $50!$?

1. Decompose the composite divisor $12$ into its prime powers:

   $$12 = 2^2 \times 3^1$$

1. Use Legendre's formula to find the power of the prime base $3$ in $50!$:

   $$E_3(50!) = \lfloor 50/3 \rfloor + \lfloor 50/9 \rfloor + \lfloor 50/27 \rfloor = 16 + 5 + 1 = 22$$

1. Use Legendre's formula to find the power of the prime base $2$ in $50!$:

   $$E_2(50!) = \lfloor 50/2 \rfloor + \lfloor 50/4 \rfloor + \lfloor 50/8 \rfloor + \lfloor 50/16 \rfloor + \lfloor 50/32 \rfloor = 25 + 12 + 6 + 3 + 1 = 47$$

1. Since we require the power of $2^2$ (which is $4$):

   $$\text{Power of } 4 = \left\lfloor \frac{47}{2} \right\rfloor = 23$$

1. Combine the constraints. Each factor of $12$ requires one $3^1$ and one $4^1$. The number of factors is limited by the smaller available power:

   $$\text{Highest Power of } 12 = \min(22, 23) = 22$$

1. **Conclusion**: The highest power of $12$ that divides $50!$ is $22$.

---

## Application Scenarios: Quantitative Reasoning

Factorial and exponent patterns are frequently applied to sorting and grouping problems:

- **Mohit** is organizing an artisanal chocolate box. He has a total of $8!$ chocolates. He wants to pack them into smaller nested gift boxes containing pairs of chocolates. He uses Legendre's formula to check the exponent of $2$ in $8!$, which is $7$. This tells him he can pack them into nested pairs up to $7$ levels deep without any leftover chocolates in the groupings.
- **Akash** is auditing a warehouse batch inventory system represented by the coordinate sum $15! + 16!$. He needs to verify if the total units can be divided evenly into $17$ shipping zones. By factoring the equation into $15! \times 17$, he quickly confirms that the total is a multiple of $17$, verifying the distribution structure is mathematically consistent.

---

## Comparison Summary Table

| Number ($n!$) | Exponent of 2 | Exponent of 3 | Exponent of 5 | Trailing Zeros ($E_5$) |
| --- | --- | --- | --- | --- |
| **5!** (120) | $3$ | $1$ | $1$ | $1$ |
| **8!** (40,320) | $7$ | $2$ | $1$ | $1$ |
| **10!** (3,628,800) | $8$ | $4$ | $2$ | $2$ |
| **25!** | $22$ | $10$ | $6$ | $6$ |
| **50!** | $47$ | $22$ | $12$ | $12$ |
| **100!** | $97$ | $48$ | $24$ | $24$ |

### ⚠️ Important: The Composite Divisor Trap

When finding the highest power of a composite number $C$ that divides $n!$:

> Never simply use Legendre's formula directly on the composite number $C$. For instance, trying to find the power of $12$ in $50!$ by calculating $\lfloor 50/12 \rfloor + \lfloor 50/144 \rfloor$ will yield an incorrect result.

> You must **always** decompose the composite number into its prime factors, calculate the exponents of those prime factors separately using Legendre's formula, and find the limiting factor based on the required ratios.

# Summary

Factorial calculations involve finding products of consecutive integers up to $n$. Exponents of prime factors within factorials are determined using Legendre's formula, which divides the integer recursively by powers of the prime. Trailing zeros represent the number of times $10$ divides $n!$, which matches the power of the limiting prime factor $5$. When dealing with composite base divisors, decomposing the divisor into co-prime prime-power components determines the maximum division limit. These concepts are fundamental for counting divisors, simplifying factorial summations, and evaluating digit products in quantitative aptitude test patterns.




