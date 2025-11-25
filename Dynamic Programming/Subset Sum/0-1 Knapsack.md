

# 📘 **DP Pattern: Subset Sum / 0-1 Knapsack (Boolean DP)**

This pattern checks **whether a target can be achieved** by choosing or skipping elements.
It is one of the most fundamental DP templates.

---

## 🔍 **How to Identify This Pattern**

Use this pattern when:

* You choose **take / not take** for each element
* Each element is used **at most once**
* The question asks:

  * *Is it possible…?*
  * *Can we form this sum / value?*
  * *Is there a subset…?*

Common terms that signal this pattern:

* “subset”
* “possible or not”
* “choose or skip”
* “partition”
* “difference”
* “target sum”

---

## 🧠 **Memoization Thinking Pattern**

1. **What varies?**
   → Usually: `index`, `target`

2. **What are the choices?**
   → `take` or `not take`

3. **Stopping conditions?**
   → sum reached, array exhausted

4. **Is subproblem repeated?**
   → Yes → use DP memoization

---

## ⭐ **Memoization Template (Core Pattern)**

```cpp
bool f(int index, int target, vector<int>& arr, vector<vector<int>>& dp) {

    // Base cases
    if (target == 0) return true;
    if (index == 0) return (arr[0] == target);

    if (dp[index][target] != -1)
        return dp[index][target];

    bool notTake = f(index - 1, target, arr, dp);

    bool take = false;
    if (arr[index] <= target)
        take = f(index - 1, target - arr[index], arr, dp);

    return dp[index][target] = take || notTake;
}
```

### **Driver Function**

```cpp
bool subsetSum(vector<int>& arr, int target) {
    int n = arr.size();
    vector<vector<int>> dp(n, vector<int>(target + 1, -1));
    return f(n - 1, target, arr, dp);
}
```

---

## 🎯 **Common Problems Solved with This Template**

### ✔ Subset Sum Problem

### ✔ Partition Equal Subset Sum

### ✔ Count Subsets with Sum K (boolean → counting modification)

### ✔ Minimum Subset Sum Difference

### ✔ Target Sum (convert to subset-sum)

### ✔ Number of subsets with given difference K

### ✔ 0-1 Knapsack (value-based variation)

---

## 🔗 **Important LeetCode Problems (Must Practice)**

| Problem                                             | Link                                                                                                                                                                   |
| --------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Subset Sum / Partition Equal Subset Sum**         | [https://leetcode.com/problems/partition-equal-subset-sum/](https://leetcode.com/problems/partition-equal-subset-sum/)                                                 |
| **Target Sum**                                      | [https://leetcode.com/problems/target-sum/](https://leetcode.com/problems/target-sum/)                                                                                 |
| **Last Stone Weight II (subset difference)**        | [https://leetcode.com/problems/last-stone-weight-ii/](https://leetcode.com/problems/last-stone-weight-ii/)                                                             |
| **0-1 Knapsack variant (On LC: extra constraints)** | Not direct, but appears in many contest problems                                                                                                                       |
| **Combination Sum IV (variation)**                  | [https://leetcode.com/problems/combination-sum-iv/](https://leetcode.com/problems/combination-sum-iv/)                                                                 |
| **Count subsets (related variant)**                 | (On GFG, classical DP): [https://www.geeksforgeeks.org/problems/subset-sum-problem-1611555638/](https://www.geeksforgeeks.org/problems/subset-sum-problem-1611555638/) |

---
