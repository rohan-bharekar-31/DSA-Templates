## Binary Search on Real Numbers (Precision)

### Generic Template
```cpp
double lo = L, hi = R;
double tol = 1e-6;

while (hi - lo > tol) {
    double mid = (lo + hi) / 2.0;
    if (condition(mid))
        lo = mid;   // or hi = mid depending on monotonicity
    else
        hi = mid;
}

double ans = (lo + hi) / 2.0;
````

---

### Fixed-Iteration Version

```cpp
double lo = L, hi = R;

for (int i = 0; i < ITER; i++) {
    double mid = (lo + hi) / 2.0;
    if (condition(mid))
        lo = mid;
    else
        hi = mid;
}

double ans = (lo + hi) / 2.0;
```

---

### Number of Iterations Needed

Initial range = `R - L`
Required precision = `tol`

iterations = ceil( log2( (R - L) / tol ) )

---

### Why Stop When `hi - lo ≤ tol`? (Q & A)

**Q:** Why is `hi - lo ≤ tol` a correct stopping condition?
**A:** Because the true answer is guaranteed to lie in `[lo, hi]`, and the maximum possible error is the interval length.

* Binary search invariant: **true answer ∈ [lo, hi]**
* Each iteration halves the interval:
  [
  \frac{R-L}{2^k}
  ]
* When `hi - lo ≤ tol`, any value in the interval is within `tol` of the true answer.
* Returning `(lo + hi)/2` ensures:
  [
  |ans - true_answer| \le tol
  ]

---

### Iteration Rule of Thumb

* `tol = 1e-6` → ~30 iterations
* `tol = 1e-9` → ~35 iterations
* Full `double` safety → **60 iterations**

