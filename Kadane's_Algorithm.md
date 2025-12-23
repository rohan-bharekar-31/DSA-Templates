
# Kadane's Algorithm — Maximum Subarray Sum

## 🚀 Problem
Given an array of integers, find the maximum possible sum of a contiguous subarray.

---

## ✅ Kadane's Algorithm (C++ Implementation)

```cpp
int maximumSumSubArray(vector<int> arr) {
    int currMax = arr[0];
    int overallMax = arr[0];

    for (int i = 1; i < arr.size(); i++) {
        // Either extend previous subarray or start a new subarray
        currMax = max(arr[i], currMax + arr[i]);
        
        // Track the best answer found so far
        overallMax = max(overallMax, currMax);
    }
    return overallMax;
}
````

---

## 🧠 Logic

* `currMax` → best sum ending at current index
* `overallMax` → best sum found anywhere
* At each index, choose:

  * start fresh from `arr[i]`, **OR**
  * extend previous sum `currMax + arr[i]`

---

## 📈 Time Complexity

```
O(n)
```

## 📦 Space Complexity

```
O(1)
```

---

## ✨ Example

Array: `[−2, 1, −3, 4, −1, 2, 1, −5, 4]`
Result: `6`
Explanation: Subarray `[4, −1, 2, 1]` gives max sum = **6**

