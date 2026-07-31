# Co-prime & Twin Prime Numbers

![](https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/co-prime-twin-prime-numbers/1785485027252-1.png)

In number theory and quantitative mathematics, prime numbers exhibit unique relationships when paired together or combined with composite numbers. Two of the most important relative classifications are **Co-prime Numbers** and **Twin Prime Numbers**.

---

## Core Definitions

### 1. Co-prime Numbers (Relatively Prime)

Two numbers $a$ and $b$ are said to be **Co-prime** (or relatively prime) if their Highest Common Factor (HCF) is $1$. In other words, they share no common divisors other than $1$.

- **Key Property**: The numbers in a co-prime pair do not have to be prime numbers themselves.
- *Example*: $(15, 28)$ is a co-prime set because the factors of $15$ are $\{1, 3, 5, 15\}$ and the factors of $28$ are $\{1, 2, 4, 7, 14, 28\}$, sharing only $1$.
- *Non-Examples*:
- $(14, 35)$ are both divisible by $7$ (not co-prime).
- $(18, 27)$ are both divisible by $9$ (not co-prime).
- $(21, 49)$ are both divisible by $7$ (not co-prime).

### 2. Composite Co-primes

A pair of numbers where both numbers are composite (non-prime), yet they share no common factors other than $1$.

- *Example*: $(8, 15)$. Both $8$ (factors: $1, 2, 4, 8$) and $15$ (factors: $1, 3, 5, 15$) are composite, but since their HCF is $1$, they form a composite co-prime set.

### 3. Twin Prime Numbers

**Twin Primes** are pairs of prime numbers that differ by exactly $2$.

- **Formula**: $(p, p+2)$ where both $p$ and $p+2$ are prime numbers.
- *Examples*: $(3, 5)$, $(5, 7)$, $(11, 13)$, $(17, 19)$, $(29, 31)$, $(41, 43)$, \ldots$
- *Non-Examples*: $(13, 17)$ or $(19, 23)$ because their difference is $4$.

---

## Infographic: Visualizing Co-primes and Twin Primes

The following diagram illustrates the distinct mathematical structures of co-prime and twin prime pairs:

---

## Quantitative Patterns and Arithmetic Problems

Solving quantitative questions involving these concepts requires applying divisor analysis and algebraic systems:

### 1. Finding Co-primes in a Range (Inclusion-Exclusion Principle)

*Problem*: If the first number is $45$, how many two-digit numbers (from $10$ to $99$) can serve as a co-prime second part?

1. Total two-digit numbers: $99 - 10 + 1 = 90$ numbers.
2. Prime factors of $45$: $3$ and $5$. Any number sharing these factors is not co-prime to $45$.
3. Count multiples of $3$ in range $[10, 99]$:

   $$\text{Multiples of } 3 = \lfloor 99/3 \rfloor - \lfloor 9/3 \rfloor = 33 - 3 = 30$$

1. Count multiples of $5$ in range $[10, 99]$:

   $$\text{Multiples of } 5 = \lfloor 99/5 \rfloor - \lfloor 9/5 \rfloor = 19 - 1 = 18$$

1. Count multiples of $15$ (both $3$ and $5$, to avoid double counting):

   $$\text{Multiples of } 15 = \lfloor 99/15 \rfloor - \lfloor 9/15 \rfloor = 6 - 0 = 6$$

1. Using the Principle of Inclusion-Exclusion, find numbers divisible by $3$ or $5$:

   $$\text{Divisible by } 3 \text{ or } 5 = 30 + 18 - 6 = 42$$

1. Calculate the co-prime count:

   $$\text{Co-prime to } 45 = 90 - 42 = 48$$

### 2. Product of Twin Primes from Sum

*Problem*: Two prime numbers forming a twin prime set have a sum of $60$. What is their product?

1. Let the twin primes be $p$ and $p+2$.
2. Write the sum equation:

   $$p + (p + 2) = 60 \implies 2p = 58 \implies p = 29$$

1. The twin prime pair is $(29, 31)$.
2. Compute the product:

   $$\text{Product} = 29 \times 31 = (30 - 1)(30 + 1) = 30^2 - 1 = 900 - 1 = 899$$

### 3. Co-prime Factors with Product Constraints

*Problem*: Two numbers representing batch sizes are co-prime, both are less than $50$, and their product is $783$. What is the difference between them?

1. Find the prime factorization of $783$:

   $$783 = 9 \times 87 = 3^3 \times 29 = 27 \times 29$$

1. Since both factors must be less than $50$, the only possible factor pairs are $(27, 29)$.
2. Check co-primality: $HCF(27, 29) = 1$ (Valid).
3. Compute the difference:

   $$\text{Difference} = 29 - 27 = 2$$

### 4. Pairwise Co-prime Systems

*Problem*: Three numbers $(a, b, c)$ are pairwise co-prime. If $a \times b = 143$ and $b \times c = 187$, find the value of $a + b + c$.

1. Identify $b$ as the common factor of $a \times b$ and $b \times c$. Therefore, $b$ must be the HCF of $143$ and $187$.
2. Factor the values:

   $$143 = 11 \times 13$$
   $$187 = 11 \times 17$$

1. Since $HCF(143, 187) = 11$, we have $b = 11$.
2. Calculate $a$ and $c$:

   $$a = 143 / 11 = 13$$
   $$c = 187 / 11 = 17$$

1. Find the sum:

   $$a + b + c = 13 + 11 + 17 = 41$$

---

## Application Scenarios: Quantitative Reasoning

Co-prime and twin prime properties help in formulating logical arrangements and calendar periods:

- **Mohit** is designing a schedule for two factory machines that require periodic inspections. Machine A needs checkups every $15$ days, and Machine B every $28$ days. To ensure their inspection schedules do not constantly clash (which would cause logistics delays), Mohit notes that the cycles $(15, 28)$ are co-prime. This ensures they will only clash once every $15 \times 28 = 420$ days, maximizing operational uptime compared to using cycles like $14$ and $35$ which share a common factor of $7$ and clash every $70$ days.
- **Akash** is verifying prime-numbered day schedules for delivery fleets. He notes that twin prime days (like $11$ and $13$) provide a regular scheduling structure. He observes that for any twin prime pair greater than $(3, 5)$, the sum of the two days is always a multiple of $12$. He uses this algebraic shortcut to quickly check and validate large sum totals in fleet logs.

---

## Comparison Summary Table

| Category | Relationship Type | HCF Requirement | Example Pair | Key Mathematical Check |
| --- | --- | --- | --- | --- |
| **Co-prime** | Relative factors | $HCF(a, b) = 1$ | $(8, 15)$ | Shared divisor is only $1$ |
| **Twin Prime** | Distance spacing | $HCF(a, b) = 1$ | $(11, 13)$ | Both are prime and difference is $2$ |

### ⚠️ Important: The Twin Prime Sum Rule

For any twin primes $(p, p+2)$ other than the pair $(3, 5)$, their sum is always divisible by $12$:

$$\text{Sum} = p + (p+2) = 2(p+1)$$

#### Proof:

1. Every prime number greater than $3$ can be written in the form $6k - 1$ or $6k + 1$, where $k$ is a positive integer.
2. In a twin prime pair $(p, p+2)$ where $p &gt; 3$, the smaller prime $p$ must be of the form $6k - 1$, and the larger prime $p+2$ must be $6k + 1$.
3. Substitute these forms into the sum equation:

   $$\text{Sum} = (6k - 1) + (6k + 1) = 12k$$

1. Since $k$ is an integer, the sum is always a multiple of $12$.

This rule provides a powerful algebraic shortcut for simplifying series summations and identifying invalid prime pairs in multiple-choice questions.

# Summary

Co-prime numbers are pairs that share no common divisors other than $1$, regardless of whether the individual numbers are prime or composite. Twin primes are a specific subset of prime pairs that differ exactly by $2$. The algebraic relationships of these numbers, such as the divisibility of twin prime sums by $12$ or the factorization of pairwise co-prime systems, form the basis of efficient divisibility calculations and logical arrangement checks.




