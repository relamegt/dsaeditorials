# Modulus & Greatest Integer Function

In quantitative mathematics and algebraic analysis, the **Modulus Function** and the **Greatest Integer Function** are two primary operators used to manipulate and model real-number inputs. They are fundamental in studying domain boundaries, solving inequalities, and determining integer values in continuous systems.

## Modulus Function

The Modulus Function, denoted by $|x|$ (and also called the absolute value function), returns the non-negative magnitude of a real number. Geometrically, it represents the distance of a number from zero on the number line.

### Algebraic Definition

For any real number $x$:
$$|x| = \begin{cases} x, & \text{if } x \ge 0 \\ -x, & \text{if } x &lt; 0 \end{cases}$$

### Examples and Arithmetic

- **Sum of Absolute Values**: Evaluate $|-7.4| + |-2.1|$.
- The modulus removes the negative sign: $|-7.4| = 7.4$ and $|-2.1| = 2.1$.
- Summing the values: $7.4 + 2.1 = 9.5$.
- **Difference of Modulus Terms**: Evaluate $|5 - 12| - |-3|$.
- Simplify inside the modulus first: $|-7| - |-3|$.
- Evaluate the modulus terms: $7 - 3 = 4$.

## Greatest Integer Function

The Greatest Integer Function, denoted by $[x]$ (or $\lfloor x \rfloor$), outputs the greatest integer that is less than or equal to $x$. It is commonly referred to as the **Floor Function**.

### Algebraic Definition

For any real number $x$, $[x] = n$ if and only if $n \le x \lt n+1$, where $n$ is an integer.

### Behavior with Positive vs. Negative Values

- **For Positive Decimals**: It simply truncates the decimal part (rounds down toward zero).
- $[7.9] = 7$ (since $7 \le 7.9 \lt 8$).
- $[\pi] = [3.14159] = 3$ and $[e] = [2.71828] = 2$.
- Sum: $[\pi] + [e] = 3 + 2 = 5$.
- **For Negative Decimals**: It rounds down to the next lower (more negative) integer (away from zero).
- $[-2.1] = -3$ (since $-3 \le -2.1 \lt -2$).
- $[-4.8] = -5$ (since $-5 \le -4.8 \lt -4$).
- Sum of Positive and Negative Floors: $[7.9] + [-2.1] = 7 + (-3) = 4$.

## Function Visualizations

The following graph maps out the visual behaviors of both functions, highlighting absolute reflection and step-wise integer rounding:

![](https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/modulus-greatest-integer-function/1785485609694-1.png)

## Solving Modulus Equations and Inequalities

Many algebraic problems involve finding the values of $x$ that satisfy modulus constraints.

### 1. Basic Modulus Equations

Solve the equation: $|x - 3| = 5$.

- The modulus equation splits into two possible cases:
- **Case 1**: $x - 3 = 5 \implies x = 8$
- **Case 2**: $x - 3 = -5 \implies x = -2$
- The integer solutions are $x \in \{-2, 8\}$.

### 2. Quadratic Modulus Equations

Find the number of integer solutions for: $|x^2 - 4| = 5$.

- Split the equation into two cases:
- **Case 1**: $x^2 - 4 = 5 \implies x^2 = 9 \implies x = \pm 3$ (yielding 2 integer solutions: $-3$ and $3$).
- **Case 2**: $x^2 - 4 = -5 \implies x^2 = -1$ (no real or integer solutions exist because a squared real number cannot be negative).
- The total number of integer solutions is $2$.

### 3. Modulus Inequalities

Solve the inequality: $|2x + 1| \le 7$.

- Solve by rewriting the inequality within negative and positive limits:

  $$-7 \le 2x + 1 \le 7$$

- Subtract 1 from all parts:

  $$-8 \le 2x \le 6$$

- Divide by 2:

  $$-4 \le x \le 3$$

- The solution set is the closed interval $[-4, 3]$.

## Solving Greatest Integer Equations

Greatest integer equations yield intervals rather than single points, since many real numbers share the same floor value.

### 1. Fractional Floor Equations

Find the sum of all integers $x$ that satisfy: $[x/2] = 3$.

- Apply the definition of the greatest integer function:

  $$3 \le \frac{x}{2} \lt 4$$

- Multiply the entire inequality by 2:

  $$6 \le x \lt 8$$

- The integers in this range are $6$ and $7$.
- Summing these integers:

  $$\text{Sum} = 6 + 7 = 13$$

### 2. Quadratic Floor Equations

Find the complete real solution set for: $[x]^2 - 5[x] + 6 = 0$.

- Let $y = [x]$. Substitute $y$ into the equation:

  $$y^2 - 5y + 6 = 0 \implies (y-2)(y-3) = 0 \implies y = 2 \text{ or } y = 3$$

- Translate back to $[x]$:

  $$[x] = 2 \implies 2 \le x \lt 3$$
  $$[x] = 3 \implies 3 \le x \lt 4$$

- Combine both intervals:

  $$x \in [2, 4)$$

## Application Scenarios: Logical Problem Solving

Modulus and Greatest Integer properties help in analyzing constraints and coordinate limits:

- **Mohit** is modeling coordinate boundaries for a layout grid. The allowable region is bounded by the inequality $|2x + 1| \le 7$. By simplifying the inequality, he finds that the layout is restricted to the range $-4 \le x \le 3$, which allows him to confirm there are exactly $8$ valid integer coordinate positions along this axis.
- **Akash** is solving an allocation puzzle where batch sizes must meet the constraint $[x/2] = 3$. He calculates that only batches of $6$ or $7$ units are mathematically valid. By adding these configurations together, he determines that the total potential items across these patterns sum to $13$.

## Comparison Summary Table

| Input Value ($x$) | Modulus ($ | x | $) | Greatest Integer ($[x]$) | Mathematical Role |
| --- | --- | --- | --- | --- | --- |
| **7.9** | $7.9$ | $7$ | Truncates positive decimals to lower integer |
| **3.14** ($\pi$) | $3.14$ | $3$ | Constant mapping for positive bounds |
| **-2.1** | $2.1$ | $-3$ | Rounds negative decimals down to more negative integer |
| **-4.8** | $4.8$ | $-5$ | Defines negative coordinate boundaries |
| **-7.0** | $7.0$ | $-7$ | Integer inputs remain unchanged in floor function |

### ⚠️ Important: The Floor Inequality Rule

When solving inequalities involving the greatest integer function, remember that $[x] \ge n \implies x \ge n$, but $[x] \le n \implies x \lt n+1$, where $n$ is an integer. Assuming that $[x] \le n$ simplifies directly to $x \le n$ is a common error that neglects the decimal range between $n$ and $n+1$. Always verify the boundaries by checking decimal values at the endpoints of your interval solutions.

# Summary

The Modulus function reflects negative numbers to their absolute positive values, representing magnitude. The Greatest Integer function rounds real numbers down to the nearest integer, creating step-wise intervals. Solving equations with these operators requires splitting modulus constraints into positive and negative cases, and translating floor outputs into continuous range intervals. These algebraic rules form the basis for solving coordinate limit puzzles, finding integer solutions in fractional inequalities, and mapping intervals in quantitative aptitude test patterns.




