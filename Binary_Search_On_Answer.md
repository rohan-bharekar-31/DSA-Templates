

## 🌳 1. What is “Binary Search on Answer”?

This isn’t searching in a sorted array.
Instead, you’re searching for an **optimal answer (like min/max)** that satisfies some *condition* — e.g.:

> Minimum capacity so all packages can be shipped in D days
> Minimum speed so all bananas are eaten in H hours
> Maximum length of ribbon that can be cut into ≥ K pieces

We don’t have a sorted array, but we *can* define a monotonic condition:

```
If x works, then all values > x will also work  (for minimum)
If x works, then all values < x will also work  (for maximum)
```

So binary search applies on the **range of possible answers**.

---

## 🧩 2. The Two Fundamental Patterns

Let’s separate them cleanly — one for **finding minimum possible answer**, one for **maximum possible answer**.

---

### 🟢 CASE 1: Find **minimum** possible answer (like “minimum speed”)

We are searching for **the smallest `x` that satisfies condition(x) = True**.

#### ✅ Template (Top-Coder & LC-Style)

```cpp
int low = min_possible, high = max_possible;
while (low < high) {
    int mid = low + (high - low) / 2;
    if (condition(mid)) {
        // mid works -> try smaller
        high = mid;
    } else {
        // mid doesn't work -> go right
        low = mid + 1;
    }
}
return low; // or high (same here)
```

#### 🧠 Intuition / Derivation

* We want the **first True** in a sequence like
  `F F F F T T T`
* Invariant: answer is always in [low, high].
* When `condition(mid)` is true → you might still find smaller true → so move **left** (high = mid).
* When false → you must go **right** (low = mid + 1).
* Loop condition is `low < high` because:

  * You always shrink interval.
  * At the end `low == high`, both pointing to the first True.

🧩 Works best when:

* Condition is monotonic.
* You want **minimum satisfying** value.


### 🔴 CASE 2: Find **maximum** possible answer (like “maximum length”)

We are searching for **the largest `x` that satisfies condition(x) = True**.

#### ✅ Template

```cpp
int low = min_possible, high = max_possible;
while (low < high) {
    int mid = low + (high - low + 1) / 2; // notice +1 to prevent infinite loop
    if (condition(mid)) {
        // mid works -> try larger
        low = mid;
    } else {
        // mid doesn't work -> go left
        high = mid - 1;
    }
}
return low; // or high (same)
```

#### 🧠 Intuition / Derivation

* We want the **last True** in a sequence like
  `T T T T F F F`
* When `condition(mid)` is true → maybe we can do better → move **right** (low = mid).
* When false → go **left** (high = mid - 1).
* We use `(high - low + 1) / 2` because otherwise, when `low + 1 == high`,
  `mid = low` would never progress and cause infinite loop.

🧩 Works best when:

* You want **maximum feasible** value.

## 🚫 Infinite Loop Common Causes

1. **Using wrong mid formula** (for max case forget +1)
2. **Using <= in while condition** — then you must handle breaking carefully; not worth it.
3. **Not updating low/high correctly** — same value assignment repeats mid.
4. **Condition not monotonic** — binary search invalid.

---

