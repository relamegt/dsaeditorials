# Place Value & Face Value

In mathematics and arithmetic, every number is composed of digits. To understand the magnitude and structure of numbers, we must distinguish between two fundamental properties of digits: **Face Value** and **Place Value**. These concepts are the bedrock of the positional numeral system used in modern mathematics.

## Core Concepts

Every digit in a number has two values:

### Face Value

The **Face Value** of a digit is the actual value of the digit itself, regardless of its position in the number. It is constant and never changes.

- *Example*: In the number $5,472$, the face value of the digit $4$ is simply $4$.

### Place Value

The **Place Value** of a digit represents the value of the digit based on its position (or "place") within the number. It changes dynamically depending on where the digit is situated.

- *Formula*: $\text{Place Value} = \text{Face Value} \times \text{Value of the Place}$
- *Example*: In the number $5,472$, the digit $4$ is in the hundreds place, so its place value is $4 \times 100 = 400$.

## Visualizing Place Value and Face Value

To see how these values operate, let's look at the expanded notation of the number $5,472$:

![](https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/place-value-face-value/1785484523237-1.png)

By breaking down the number, we see that the sum of the place values of all digits yields the original number:

$$5000 + 400 + 70 + 2 = 5,472$$

## Numeral Systems: Indian vs. International

Different numeral systems group place values differently, which affects how numbers are written and read using commas.

### Indian Numeral System

In the Indian system, place values are grouped in periods of **Ones**, **Thousands**, **Lakhs**, and **Crores**. Commas are placed after the hundreds place, and then after every two digits.

- *Place values*: Ones, Tens, Hundreds, Thousands, Ten Thousands, Lakhs, Ten Lakhs, Crores, Ten Crores...
- *Example*: $12,34,567$ is read as "Twelve Lakh, Thirty-Four Thousand, Five Hundred Sixty-Seven."

### International Numeral System

In the International system, place values are grouped in periods of **Ones**, **Thousands**, **Millions**, and **Billions**. Commas are placed after every three digits from right to left.

- *Place values*: Ones, Tens, Hundreds, Thousands, Ten Thousands, Hundred Thousands, Millions, Ten Millions, Hundred Millions, Billions...
- *Example*: $1,234,567$ is read as "One Million, Two Hundred Thirty-Four Thousand, Five Hundred Sixty-Seven."

The following chart illustrates how place value categories correspond across the two systems:

![](https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/place-value-face-value/1785484547298-2.png)

---

## Place Value in Decimal Numbers

The positional system extends to the right of the decimal point, representing fractional parts of a unit. As we move right, each position is divided by 10:

- **Tenths** ($10^{-1}$ or $\frac{1}{10}$): The first digit to the right of the decimal.
- **Hundredths** ($10^{-2}$ or $\frac{1}{100}$): The second digit to the right of the decimal.
- **Thousandths** ($10^{-3}$ or $\frac{1}{1000}$): The third digit to the right of the decimal.

*Example*: In the decimal number $34.567$:

- The place value of $5$ is $5 \times 0.1 = 0.5$ (Tenths).
- The place value of $6$ is $6 \times 0.01 = 0.06$ (Hundredths).
- The place value of $7$ is $7 \times 0.001 = 0.007$ (Thousandths).

---

## Application Scenarios: String Parsing and Binary Representation

Place value principles are vital in software engineering, particularly in low-level data conversion and memory layouts:

- **Mohit** is writing a string-to-integer conversion function (analogous to the standard `atoi` library function). The algorithm parses a string of digits (e.g., `"5472"`) into its integer representation by scanning characters from left to right:

  
  $$\text{Result} = (\text{Previous Result} \times 10) + \text{Face Value of Digit}$$
  
  The engine processes `"5472"` step-by-step:

1. Character `'5'`: $\text{Result} = (0 \times 10) + 5 = 5$
2. Character `'4'`: $\text{Result} = (5 \times 10) + 4 = 54$
3. Character `'7'`: $\text{Result} = (54 \times 10) + 7 = 547$
4. Character `'2'`: $\text{Result} = (547 \times 10) + 2 = 5,472$

  
  By scaling the previous result by 10 at each step, Mohit's code dynamically shifts the place value of the parsed digits to construct the final integer.

- **Akash** is designing a low-level network protocol that uses hexadecimal (base-16) memory addresses. He needs to decode the address `0x2A` into decimal.

  Akash applies the place value rules using a base of 16 instead of 10:
  
  $$\text{Value} = (2 \times 16^1) + (A \times 16^0)$$
  
  Since the face value of the hex digit $A$ is $10$:
  
  $$\text{Value} = (2 \times 16) + (10 \times 1) = 32 + 10 = 42$$
  
  Understanding non-decimal place values allows Akash to write code that maps binary patterns to concrete physical addresses.

---

## Mathematical Calculations and Proofs

Many competitive math problems require computing differences or sums of place and face values.

### Difference of Place Values

Consider finding the difference between the place values of the two $7$s in the number $7,472$:

1. Identify the first $7$: It is in the thousands place, so its place value is:

   $$\text{Place Value}_1 = 7 \times 1000 = 7000$$

1. Identify the second $7$: It is in the tens place, so its place value is:

   $$\text{Place Value}_2 = 7 \times 10 = 70$$

1. Compute the difference:

   $$\text{Difference} = 7000 - 70 = 6930$$

### Sum of Place Value and Face Value

Consider finding the sum of the place value and face value of the digit $4$ in the number $5,472$:

1. Face value of $4$: $4$
2. Place value of $4$: $4 \times 100 = 400$
3. Compute the sum:

   $$\text{Sum} = 400 + 4 = 404$$

---

## Positional Comparison Chart

| Value Position (Relative to decimal) | Power of 10 | Place Name (International) | Place Name (Indian) | Numeric Value |
| --- | --- | --- | --- | --- |
| $10^6$ | $10^6$ | Million | Ten Lakh | $1,000,000$ |
| $10^5$ | $10^5$ | Hundred Thousand | Lakh | $100,000$ |
| $10^4$ | $10^4$ | Ten Thousand | Ten Thousand | $10,000$ |
| $10^3$ | $10^3$ | Thousand | Thousand | $1,000$ |
| $10^2$ | $10^2$ | Hundred | Hundred | $100$ |
| $10^1$ | $10^1$ | Ten | Ten | $10$ |
| $10^0$ | $10^0$ | One | One | $1$ |
| $10^{-1}$ | $10^{-1}$ | Tenth | Tenth | $0.1$ |
| $10^{-2}$ | $10^{-2}$ | Hundredth | Hundredth | $0.01$ |

### ⚠️ Important: Positional Shifting and Integer Overflow

In computer memory, integers are stored in fixed-size data structures (such as 32-bit or 64-bit registers). When we parse numbers or perform base-shifting (like multiplying by 10 to shift place values), we risk triggering an **Integer Overflow**.

For example, a signed 32-bit integer has a maximum value of:

$$\text{MAX\_INT} = 2,147,483,647$$

If we are parsing a string representing a large number and attempt to shift the place value of the digits past this limit:

- **Left-hand side**: Suppose the parsed result reaches $2,147,483,64$.
- **Next shift**: The next step calculates $(2,147,483,64 \times 10) + 8 = 2,147,483,648$.
- **Result**: Because $2,147,483,648 &gt; \text{MAX\_INT}$, the value overflows, wrapping around to the negative range (yielding $-2,147,483,648$ due to two's complement representation).
- **Conclusion**: Software developers must write range boundary checks during place-value summation loops to prevent memory wrap-around errors, which are common vectors for buffer exploits and financial calculation glitches.

# Summary

Place Value and Face Value are the core concepts that define the value of digits in a positional numeral system. The Face value represents the digit itself, while the Place value scales that digit by its positional power of 10 (or another base, such as 16 in hex or 2 in binary). Different numeral systems, like the Indian and International systems, use varying group sizing (periods) to denote larger values. In computational engineering, these base-10 shifts form the algorithmic structure for number parsers and data deserialization routines, where developers must balance calculations against register constraints to avoid integer overflow errors.




