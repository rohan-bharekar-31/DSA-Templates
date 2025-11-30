
# 📘 **DP Pattern: Longest Common Subsequence (LCS Family)**

This pattern appears in many string-DP problems.
If two strings are involved and the question asks for similarity, matching, or operations → think **LCS pattern**.

---

# 🔍 **How to Identify This Pattern**

Use this DP when:

✔ The problem has **two strings**
✔ You compare characters between string1[i] and string2[j]
✔ Choices depend on whether characters **match or don’t match**
✔ You want to **maximize** length / score
✔ The question mentions:

* “Longest…”
* “Common…”
* “Subsequence”
* “Minimum operations to convert…”
* “Insert/Delete operations…”
* “Matching characters…”

This pattern is the parent of many problems such as LCS, LPS, Edit Distance, LCSubstring, SCS, etc.

---

# 🧠 **Memoization Thinking Pattern**

**What varies?**
→ Two indices: `i` and `j`

**What are the choices?**

* If match → take + move diagonally `(i-1, j-1)`
* If mismatch → try both moves `(i-1, j)` and `(i, j-1)`

**Stopping condition?**
→ If either string ends (`i == 0 || j == 0`)

**Do subproblems repeat?**
→ Yes (overlapping subproblems) → memoize.

---

# ⭐ **Memoization Template — LCS Core Pattern**

```cpp
int solve(int i, int j, string &s1, string &s2, vector<vector<int>> &dp) {

    // Base case
    if (i == 0 || j == 0)
        return 0;

    if (dp[i][j] != -1)
        return dp[i][j];

    // Characters match
    if (s1[i-1] == s2[j-1]) {
        return dp[i][j] = 1 + solve(i-1, j-1, s1, s2, dp);
    }

    // Characters don't match
    int move1 = solve(i-1, j, s1, s2, dp);
    int move2 = solve(i, j-1, s1, s2, dp);

    return dp[i][j] = max(move1, move2);
}
```

### **Driver Function**

```cpp
int longestCommonSubsequence(string s1, string s2) {
    int n1 = s1.size(), n2 = s2.size();
    vector<vector<int>> dp(n1+1, vector<int>(n2+1, -1));
    return solve(n1, n2, s1, s2, dp);
}
```

This is the **core template** for ALL LCS-based problems.

---

# 🎯 **Common Problems Solved with This Pattern**

### **Direct LCS**

* Longest Common Subsequence (base problem)

### **LCS Transformations**

* Longest Common Substring (change recurrence)
* Print LCS (traceback from dp table)
* Shortest Common Supersequence
  `|SCS| = n1 + n2 - LCS`
* Longest Palindromic Subsequence
  → LCS(s, reverse(s))

### **String Edit Problems**

* Minimum Insertions to Palindrome
  → n – LPS
* Minimum Deletions to Make Strings Equal
  → n1 + n2 - 2 * LCS
* Minimum Insert/Delete to convert A → B

### **Matching Problems**

* Max number of uncrossed lines
  → same as LCS
* Delete operations for two strings
  → n1 + n2 - 2 * LCS

---

# 🔗 **Important LeetCode Problems (Must Practice)**

| Problem                                       | Link                                                                                                                                               |
| --------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Longest Common Subsequence**                | [https://leetcode.com/problems/longest-common-subsequence/](https://leetcode.com/problems/longest-common-subsequence/)                             |
| **Longest Palindromic Subsequence (LPS)**     | [https://leetcode.com/problems/longest-palindromic-subsequence/](https://leetcode.com/problems/longest-palindromic-subsequence/)                   |
| **Uncrossed Lines (LCS disguised)**           | [https://leetcode.com/problems/uncrossed-lines/](https://leetcode.com/problems/uncrossed-lines/)                                                   |
| **Minimum ASCII Delete Sum**                  | [https://leetcode.com/problems/minimum-ascii-delete-sum-for-two-strings/](https://leetcode.com/problems/minimum-ascii-delete-sum-for-two-strings/) |
| **Delete Operation for Two Strings**          | [https://leetcode.com/problems/delete-operation-for-two-strings/](https://leetcode.com/problems/delete-operation-for-two-strings/)                 |
| **Shortest Common Supersequence**             | [https://leetcode.com/problems/shortest-common-supersequence/](https://leetcode.com/problems/shortest-common-supersequence/)                       |
| **Edit Distance (related but more advanced)** | [https://leetcode.com/problems/edit-distance/](https://leetcode.com/problems/edit-distance/)                                                       |

---


