# Modular Arithmetic - Quick Revision Notes 🚀

## 🔴 THE CRITICAL BUG

### The Problem
```cpp
❌ result = (a - b) % MOD;  // Can be NEGATIVE in C++!
```

### The Fix (MEMORIZE THIS!)
```cpp
✅ result = ((a - b) % MOD + MOD) % MOD;
// OR if a, b already reduced:
✅ result = (a - b + MOD) % MOD;
```

---

## 🎯 Why It Breaks

### Key Issue: Stored Value ≠ Actual Value
```cpp
// When storing with modulo:
numInt = (numInt * 10 + digit) % MOD;
preX[i] = numInt;  // Stores REMAINDER, not actual value!

// Example:
Actual: 2711785629
Stored: 2711785629 % 1000000007 = 711785615  ⚠️
```

### The Calculation Goes Wrong
```cpp
// Mathematical: 2711785629 > 2×10^9 ✓
// After modulo: 711785615 < 999999993 ❌ ORDER REVERSED!

n1 = 711785615
n2_times_pow = 999999993
diff = 711785615 - 999999993 = -288214378  ❌ NEGATIVE!
```

---

## 💡 Why Adding MOD Works

### Mathematical Property
```
-288214378 and 711785629 are EQUIVALENT in modulo arithmetic
Difference = 711785629 - (-288214378) = 1000000007 = MOD
```

### Step-by-Step
```cpp
diff = -288214378
diff + MOD = -288214378 + 1000000007 = 711785629  ✓
result % MOD = 711785629 % 1000000007 = 711785629  ✓
```

---

## 🧠 Key Insights

| Concept | Explanation |
|---------|-------------|
| **Modulo ≠ Order** | `A > B` doesn't mean `A % MOD > B % MOD` |
| **Why 1×MOD?** | After `(a % MOD - b % MOD)`, range is `[-MOD+1, MOD-1]`<br>Adding 1×MOD always makes it positive |
| **Why not 2×MOD?** | Works but wasteful. `(a + k×MOD) % MOD = a % MOD` for any k |
| **Double modulo?** | First reduces range, `+MOD` makes positive, final ensures `[0, MOD-1]` |

---

## 📝 Standard Templates

```cpp
const long long MOD = 1e9 + 7;

// Addition (safe)
(a + b) % MOD

// Subtraction (CRITICAL!)
((a - b) % MOD + MOD) % MOD

// Multiplication (prevent overflow)
(1LL * a * b) % MOD

// Power
long long power(long long a, long long b) {
    long long res = 1;
    while (b > 0) {
        if (b & 1) res = (res * a) % MOD;
        a = (a * a) % MOD;
        b >>= 1;
    }
    return res;
}
```

---

## 🚨 Common Mistakes

```cpp
❌ result = (a - b) % MOD;              // Negative!
❌ if (a % MOD > b % MOD) { }           // Wrong assumption
❌ result = (a * b) % MOD;              // Overflow!
❌ Thinking preX[i] = actual value      // It's the remainder!

✅ result = (a - b + MOD) % MOD;
✅ Don't compare after modulo
✅ result = (1LL * a * b) % MOD;
✅ preX[i] = actual_value % MOD
```

---

## 🎓 The Clock Analogy

```
Modulo = Clock with numbers 0 to MOD-1
-3 on a 12-hour clock = 9 (go backward 3 = forward 9)
-3 + 12 = 9  ✓

In C++: -3 % 12 = -3 (stays negative!)
Fix: (-3 + 12) % 12 = 9  ✓
```

---

## ✅ Pre-Contest Checklist

- [ ] Is there subtraction with modulo? → Add `+ MOD`
- [ ] Is there multiplication? → Use `1LL *` to prevent overflow
- [ ] Am I comparing values after modulo? → DON'T!
- [ ] Do I assume stored value = actual value? → It's the remainder!

---

## 🔥 THE GOLDEN RULE

**SUBTRACTION IN MODULO = ALWAYS ADD MOD**
```cpp
((a - b) % MOD + MOD) % MOD
```

**Write this formula on paper before EVERY contest!** 📌

---

## 📊 Quick Reference: When Things Go Wrong

**Symptom:** Getting negative output or wrong answer  
**Diagnosis:** Check for `(a - b) % MOD` without `+ MOD`  
**Cure:** Replace with `((a - b) % MOD + MOD) % MOD`

**Symptom:** Large numbers giving weird results  
**Diagnosis:** Integer overflow in multiplication  
**Cure:** Use `1LL * a * b` before `% MOD`

**Symptom:** Logic seems right but answer wrong  
**Diagnosis:** Assuming order preserved after modulo  
**Cure:** Never compare `a % MOD` with `b % MOD` to infer `a` vs `b`

---

## 💾 Copy-Paste Ready Code

```cpp
// Safe modulo operations
#define MOD 1000000007
#define add(a,b) ((a + b) % MOD)
#define sub(a,b) (((a - b) % MOD + MOD) % MOD)
#define mul(a,b) ((1LL * a * b) % MOD)
```

---

**Remember:** Modulo bugs don't crash—they silently give wrong answers. Always be paranoid about subtraction! 🛡️