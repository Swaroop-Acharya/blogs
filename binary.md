# Understanding Signed and Unsigned Integers in Binary

## What is a Bit?
- A **bit** is the smallest unit of data in a computer and can be either `0` or `1`.
- A group of 8 bits forms a **byte**.
- With `n` bits, we can represent `2ⁿ` unique values.

---

## Unsigned Integers

Unsigned integers represent only **non-negative numbers**.

### Range Formula:
0 to (2^n -1)

### Examples:
| Bits | Binary Range         | Decimal Range        |
|------|----------------------|----------------------|
| 4    | 0000 to 1111         | 0 to 15              |
| 8    | 00000000 to 11111111 | 0 to 255             |
| 16   | 0000000000000000     | 0 to 65,535          |

---

## Signed Integers (Two's Complement)

Signed integers represent both **negative and positive numbers**, using a technique called **two’s complement**.

### Range Formula:
-2ⁿ⁻¹ to (2ⁿ⁻¹ - 1)


### Examples:
| Bits | Decimal Range       | Total Values |
|------|----------------------|---------------|
| 4    | -8 to +7             | 16            |
| 8    | -128 to +127         | 256           |
| 16   | -32,768 to +32,767   | 65,536        |

### How Two's Complement Works (Example: -4 in 8 bits)
1. Take the binary of +4 → `00000100`
2. Invert the bits → `11111011`
3. Add 1 → `11111100`
4. Final binary of -4 → `11111100`

---

## Summary Table

| Type       | Formula                | Values Represented            |
|------------|------------------------|-------------------------------|
| Unsigned   | 0 to 2ⁿ − 1            | Only positive values including 0 |
| Signed     | −2ⁿ⁻¹ to 2ⁿ⁻¹ − 1      | Negative and positive values |

---

## Why Bit Width Matters

The number of bits determines:
- How many total values can be represented
- What the min and max values are
- Whether the number is interpreted as signed or unsigned

The **same binary pattern** can mean different things depending on whether it's signed or unsigned.

---

## Key Takeaway

- Use unsigned when you **don’t need negative numbers** (e.g., array indexes, counts).
- Use signed when you need **both positive and negative values**.
