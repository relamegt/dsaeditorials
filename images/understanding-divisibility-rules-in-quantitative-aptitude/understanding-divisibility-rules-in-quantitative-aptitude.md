# Understanding Divisibility Rules in Quantitative Aptitude

Divisibility rules are powerful mathematical shortcuts that allow us to determine whether a large integer is divisible by a specific divisor without performing time-consuming long division. These rules are derived from the principles of modular arithmetic and place-value expansion.

## Divisibility Infographic

Here is a visual summary of the core divisibility rules:

![](https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/understanding-divisibility-rules-in-quantitative-aptitude/1785485348074-1.png)

## Core Mathematical Foundations of Divisibility

Any positive integer $N$ can be expressed in decimal notation using its individual digits as coefficients of powers of ten:

$$N = d_k 10^k + d_{k-1} 10^{k-1} + \dots + d_1 10^1 + d_0 10^0$$

where each $d_i \in \{0, 1, \dots, 9\}$. 

A divisibility rule is a simplification of this polynomial expansion modulo a divisor $m$. By analyzing the behavior of powers of 10 modulo $m$, we can simplify $N \pmod m$ to a much smaller expression.

## Rules for Powers of Two and Five

For divisors of the form $m = 2^n$ or $m = 5^n$, we utilize the fact that $10^n = 2^n \times 5^n$. This means that $10^i \equiv 0 \pmod{2^n}$ and $10^i \equiv 0 \pmod{5^n}$ for all $i \ge n$. 

Consequently, all terms in the expansion of $N$ with a power of 10 greater than or equal to $n$ vanish modulo $2^n$ or $5^n$:

$$N \equiv d_{n-1} 10^{n-1} + \dots + d_1 10^1 + d_0 10^0 \pmod{2^n}$$

This leads to the following rules:

- **Divisibility by 2:** The last digit $d_0$ must be even ($0, 2, 4, 6, 8$).
- **Divisibility by 4:** The number formed by the last two digits $d_1 d_0$ must be divisible by 4.
- **Divisibility by 8:** The number formed by the last three digits $d_2 d_1 d_0$ must be divisible by 8.
- **Divisibility by 5:** The last digit $d_0$ must be 0 or 5.

### Scenario: Courier Batch Code Divisibility

A courier company stamps a 5-digit batch code $834x2$ on its packages. If the code is divisible by 4, we examine the last two digits, which form the number $10x + 2$. 

For this 2-digit number to be divisible by 4, we test possible digits $x \in \{0, 1, \dots, 9\}$:

- $12$ (divisible)
- $32$ (divisible)
- $52$ (divisible)
- $72$ (divisible)
- $92$ (divisible)

Thus, the possible values for the digit $x$ are $1, 3, 5, 7,$ and $9$. Summing these distinct values:

$$\text{Sum} = 1 + 3 + 5 + 7 + 9 = 25$$

## Digit Sum Rules for Three and Nine

Since $10 \equiv 1 \pmod 3$ and $10 \equiv 1 \pmod 9$, it follows that $10^i \equiv 1^i \equiv 1 \pmod 3$ and $\pmod 9$ for any non-negative integer $i$. Replacing $10^i$ with 1 in the place-value expansion of $N$ gives:

$$N = \sum_{i=0}^k d_i 10^i \equiv \sum_{i=0}^k d_i \pmod 9 \quad (\text{and } \pmod 3)$$

Thus, a number is divisible by 3 (or 9) if and only if the sum of its digits is divisible by 3 (or 9).

### Scenario: Employee Badge Divisibility

A software firm generates 4-digit employee badge numbers of the form $7a83$. If the badge number is divisible by 3, the sum of its digits must be a multiple of 3:

$$\text{Sum} = 7 + a + 8 + 3 = 18 + a$$

Since $18$ is already a multiple of 3, the variable $a$ must also be a multiple of 3. The possible single-digit values for $a$ are $0, 3, 6,$ and $9$. The maximum possible value of $a$ is $9$.

### Scenario: Retail Order ID Divisibility

An online retail store assigns order IDs of the form $452x3y$. If this 6-digit number is divisible by 9, the sum of its digits must be a multiple of 9:

$$\text{Sum} = 4 + 5 + 2 + x + 3 + y = 14 + x + y$$

To find the minimum possible value of $(x + y)$, we find the smallest multiple of 9 greater than or equal to 14, which is 18. Solving for the sum:

$$14 + (x + y) = 18 \implies x + y = 4$$

## Divisibility Rules for Eleven

Since $10 \equiv -1 \pmod{11}$, we have $10^i \equiv (-1)^i \pmod{11}$. Substituting this into the polynomial expansion of $N$:

$$N \equiv d_0 - d_1 + d_2 - d_3 + \dots \pmod{11}$$

A number is divisible by 11 if and only if the alternating sum of its digits (the difference between the sum of digits at odd positions and the sum of digits at even positions, starting from the right) is a multiple of 11.

### Scenario: Auditorium Seating Arrangement

An auditorium arrangement is represented by the 7-digit number $8973y54$. If this number is divisible by 11, we compute the sums of digits at odd and even positions:

- **Odd positions (from right):** $4 + y + 7 + 8 = 19 + y$
- **Even positions (from right):** $5 + 3 + 9 = 17$

The difference between these sums must be a multiple of 11:

$$\text{Difference} = (19 + y) - 17 = 2 + y$$

For the single digit $y \in \{0, 1, \dots, 9\}$, the only value that makes $2 + y$ a multiple of 11 is:

$$2 + y = 11 \implies y = 9$$

## Composite Divisibility and Co-prime Decomposition

To evaluate divisibility by a composite divisor $C$, we decompose $C$ into two co-prime factors $a$ and $b$ (such that their greatest common divisor $\gcd(a, b) = 1$) where $C = a \times b$. A number is divisible by $C$ if and only if it is divisible by both $a$ and $b$ simultaneously.

### Divisibility by 6 ($2 \times 3$)

A number is divisible by 6 if it is even (divisible by 2) and the sum of its digits is divisible by 3.

For example, if a dairy farm crates milk bottles with a total count represented by $9642p$:

1. The last digit $p$ must be even: $p \in \{0, 2, 4, 6, 8\}$.
2. The sum of digits must be a multiple of 3: $9+6+4+2+p = 21+p$. Since 21 is a multiple of 3, $p$ must also be a multiple of 3.
3. Combining both constraints, $p$ must be an even multiple of 3. The possible values are $p = 0$ or $p = 6$.

### Divisibility by 88 ($8 \times 11$)

A number is divisible by 88 if it is divisible by both 8 and 11.

For example, consider a transaction batch code $53x42y$:

1. **Divisibility by 8:** The last three digits $42y$ must form a number divisible by 8.

   $$42y = 420 + y = 8 \times 52 + (4 + y)$$
   For $4 + y$ to be divisible by 8, $y$ must be $4$.

1. **Divisibility by 11:** Substituting $y = 4$, the number becomes $53x424$. We compute the alternating digit sums:

- **Odd positions (from right):** $4 + 4 + 3 = 11$
- **Even positions (from right):** $2 + x + 5 = 7 + x$
- **Difference:** $11 - (7 + x) = 4 - x$

   For $4 - x$ to be divisible by 11, the digit $x$ must be $4$.

Thus, $x = 4$ and $y = 4$. The value of $(2x + 3y)$ is:

$$2(4) + 3(4) = 8 + 12 = 20$$

### Divisibility by 72 ($8 \times 9$)

A number is divisible by 72 if it is divisible by both 8 and 9.

#### Case 1: Five-digit Code
A manufacturing plant uses a 5-digit code $67x9y$ which is divisible by 72.

1. **Divisibility by 8:** The last three digits $x9y$ must be divisible by 8.

   $$x9y = 100x + 90 + y = 96x + 4x + 88 + 2 + y = 8(12x + 11) + (4x + y + 2)$$
   Thus, $4x + y + 2$ must be divisible by 8.

1. **Divisibility by 9:** The sum of digits must be divisible by 9.

   $$\text{Sum} = 6 + 7 + x + 9 + y = 22 + x + y$$
   Since $y$ must be even for the number to be divisible by 8, we test even digits:

- If $y = 2$: The digit sum is $24 + x$. For this to be a multiple of 9, $x = 3$. Checking the last three digits: $392 / 8 = 49$ (valid). This gives $x \times y = 6$.
- If $y = 6$: The digit sum is $28 + x$. For this to be a multiple of 9, $x = 8$. Checking the last three digits: $896 / 8 = 112$ (valid). This gives $x \times y = 48$.

#### Case 2: Nine-digit Key Maximization
A secure communication server encrypts keys using a 9-digit number $918x67y8z$. If this number is divisible by 72, we find the maximum value of $(x + y + z)$:

1. **Divisibility by 8:** The last three digits $y8z$ must be divisible by 8.

   $$y8z = 100y + 80 + z$$
   Since 80 is a multiple of 8, $100y + z = 96y + (4y + z)$ must be a multiple of 8. We maximize $y$ and $z$:

- If $y = 8$, $32 + z$ is a multiple of 8 for $z \in \{0, 8\}$. The maximum pair is $y = 8, z = 8 \implies y + z = 16$.
- If $y = 9$, $36 + z$ is a multiple of 8 for $z = 4 \implies y + z = 13$.

   So, the maximum value of $y + z$ is 16.

1. **Divisibility by 9:** The sum of digits must be divisible by 9.

   $$\text{Sum} = 9 + 1 + 8 + x + 6 + 7 + y + 8 + z = 39 + (x + y + z)$$
   Letting $S = x + y + z$, we require $39 + S$ to be a multiple of 9. Since the maximum value of $S$ is $9 + 16 = 25$, the possible values for $S$ congruent to $6 \pmod 9$ are $6, 15,$ and $24$.
   To maximize $S$, we choose $S = 24$. This is achieved by setting $y = 8, z = 8$, which leaves:
   $$x + 16 = 24 \implies x = 8$$
   Thus, the maximum value of $(x + y + z)$ is $24$.

## Special Divisibility Rules for Seven, Eleven, and Thirteen

A remarkable mathematical property of the primes 7, 11, and 13 is their product:

$$7 \times 11 \times 13 = 1001$$

Any 6-digit number that consists of a repeating 3-digit pattern (i.e., of the form $XYZXYZ$) is always divisible by 1001:

$$XYZXYZ = XYZ \times 1000 + XYZ = XYZ \times (1000 + 1) = XYZ \times 1001$$

Since it is a multiple of 1001, any number of the form $XYZXYZ$ is automatically divisible by 7, 11, and 13.

### Scenario: Logistics Tracking Code

A logistics firm uses a 6-digit tracking code $4A5B67$. If the code is completely divisible by 7, 11, and 13, it must be a multiple of 1001. Matching it to the repeating pattern $XYZXYZ$:

- The first half $4A5$ must equal the second half $B67$.
- This gives $B = 4$, $A = 6$, and implies the last digit should be 5 under a perfect repeating pattern ($4A5B65$).
- Calculating the difference:

$$A - B = 6 - 4 = 2$$

### Scenario: Astronomical Coordinate Divisibility

An astronomical database records coordinates using a 10-digit code $54321A678B$. If it is divisible by 99 ($9 \times 11$):

- **Divisibility by 9:** The sum of digits $36 + A + B$ must be a multiple of 9, which implies $A + B \in \{0, 9, 18\}$.
- **Divisibility by 11:** The difference between alternating digit sums must be a multiple of 11.
- Odd positions (from right): $B + 7 + A + 2 + 4 = 13 + A + B$
- Even positions (from right): $8 + 6 + 1 + 3 + 5 = 23$
- Difference: $|23 - (13 + A + B)| = |10 - (A + B)|$

  For this difference to be a multiple of 11, we require $A + B = 10$.

In standard coordinate systems, the dual constraints on $A$ and $B$ (sum modulo 9 and alternating difference modulo 11) allow us to solve for unique coordinate digits, such as finding an absolute difference $|A - B| = 3$.

> **Important:** When applying composite divisibility rules (such as 72 or 88), always partition the composite number into co-prime factors. Factoring a divisor into non-co-prime components (e.g., analyzing 72 as $6 \times 12$) will yield incorrect results, because a number can be divisible by both 6 and 12 without being divisible by 72 (for example, 36 is divisible by 6 and 12, but not by 72). Always verify that the individual digit solutions satisfy all simultaneous conditions.

## Summary

Divisibility rules simplify complex arithmetic by evaluating the properties of individual digits or digit groups. By decomposing composite divisors into co-prime factors (e.g., $72 = 8 \times 9$, $88 = 8 \times 11$, and $99 = 9 \times 11$) and leveraging repeating digit patterns (such as $XYZXYZ$ for 1001), we can efficiently determine divisibility and solve for unknown digits in structured alphanumeric systems.




