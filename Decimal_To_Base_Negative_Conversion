# Negative Base Conversion — Simple Math Explanation

---

## 1. Allowed Digits
For any base (positive or negative), the digits must lie between:

0 to |base| − 1

Examples:
- Base −2 → allowed digits: 0, 1  
- Base −8 → allowed digits: 0–7  

So if remainder comes negative, it must be corrected.

---

## 2. Why can the remainder be negative?
When you divide by a **negative number**, the remainder may also come out negative:

Example:
-1 % -2 = -1

This remainder is **not allowed** because digits must be non-negative.

---

## 3. The Key Equation
Every step of conversion uses:

```
n = base × quotient + remainder
```

This must always stay true.

If the remainder is negative (like -1 or -3), we must adjust both sides so the equality stays correct.

---

## 4. The Fix (Core Idea)
If remainder < 0:

1. Add |base| to the remainder  
2. Add 1 to the quotient (or to n during the loop)

Why these two steps?

Because they keep the main equation valid.

---

## 5. The Mathematical Reason (Clear and Simple)

Suppose remainder comes out negative:

```
n = base*q + r     (r < 0)
```

We want a new remainder r′ that is positive.

Let:

```
r′ = r + |base|
q′ = q + 1
```

Now check if the equation still holds:

```
base*q′ + r′
= base*(q + 1) + (r + |base|)
= base*q + base + r + |base|
```

Since base is negative:

```
base + |base| = 0
```

So the expression becomes:

```
= base*q + r
= n     (same as original)
```

### ✔ This proves the fix is mathematically correct.

---

## 6. Why this works intuitively
- A negative remainder means you “fell short” of a full base unit.  
- Adding |base| to the remainder pushes it into the valid range.  
- But adding |base| is like adding a whole “base unit,” so you must increase the quotient by 1.

This restores perfect balance.

No trick. Just maintaining the identity:

```
n = base*q + r
```

---

## 7. Does it work for base −8, −10, −16?
YES.  
This math works for **any negative base**.

Example for base −8:

```
r = -3
r′ = -3 + 8 = 5
q′ = q + 1
```

Now 5 is a valid digit (0–7), and the equation stays correct.

---

## 8. Generic Code Template (Any Negative Base)

```cpp
string convertToNegativeBase(long long n, int base) {
    if (n == 0) return "0";

    string ans = "";
    int B = abs(base);

    while (n != 0) {
        long long rem = n % base;
        n = n / base;

        if (rem < 0) {
            rem += B;   // shift remainder into valid range
            n += 1;     // adjust quotient to keep equation true
        }

        ans = to_string(rem) + ans;
    }

    return ans;
}
```

---

## 9. Final Short Summary
- Negative bases can give negative remainders.
- Remainders must be between 0 and |base| − 1.
- Fix a negative remainder by:
  - adding |base| to remainder
  - adding 1 to quotient
- This keeps the main equation **n = base*q + remainder** correct.
