

# 🧹 Sweep Line Algorithm — Detailed Explanation

## 🧠 1. Intuition — What Problem It Solves

The **sweep line algorithm** helps handle problems involving **intervals** or **events** over time or space, such as:

- Counting overlaps (e.g., maximum number of meetings)
- Finding free/busy times
- Detecting intersections among geometric objects

### Key Idea
Instead of examining every interval pair (which is **O(n²)**),  
we process all **events** in **sorted order** and keep a **running count** of active intervals.

---

## ⚙️ 2. Core Concept — "Event-based Thinking"

Each interval `[L, R]` can be reduced to two **events**:

- **Start →** `+1` active interval  
- **End →** `-1` active interval

For **inclusive** intervals (where `[1,5]` and `[5,8]` intersect at `5`),  
we usually treat the end as `(R + 1, -1)` so we correctly handle overlaps.

### Steps

1. Collect all events as `(position, delta)`
2. Sort all events by `position`
3. Sweep through:
   - Add `delta` to a running counter
   - Keep track of the **maximum counter value**

That **maximum active count** is the result —  
it represents the **minimum number of groups**, **meeting rooms**, or **overlapping intervals** required.

---

## 📈 3. Example Walkthrough

**Input:**
```cpp
intervals = [[5,10],[6,8],[1,5],[2,3],[1,10]];
````

### Step 1: Build Events

```
(1, +1)
(2, +1)
(4, -1)  // end of [2,3] + 1
(6, +1)
(6, -1)  // end of [1,5] + 1
(7, -1)  // end of [6,8] + 1
(11, -1) // end of [5,10] + 1
(11, -1) // end of [1,10] + 1
```

### Step 2: Sort Events by Position

```
(1,+1), (2,+1), (4,-1), (6,+1), (6,-1), (7,-1), (11,-1), (11,-1)
```

### Step 3: Sweep

```
pos 1 → count = 1
pos 2 → count = 2
pos 4 → count = 1
pos 6 → count = 2
pos 7 → count = 1
pos 11 → count = 0
```

✅ **Maximum count = 3**,
meaning you need **3 groups** (or meeting rooms, etc.)

---

## ⏱️ 4. Time & Space Complexity

| Step          | Operation | Complexity     |
| ------------- | --------- | -------------- |
| Create events | 2 * n     | O(n)           |
| Sort events   | -         | O(n log n)     |
| Sweep through | -         | O(n)           |
| **Total**     | -         | **O(n log n)** |

**Space Complexity:**
We store `2n` events → **O(n)** space.

---

## 💻 5. C++ Implementation

```cpp
#include <bits/stdc++.h>
using namespace std;

int minGroups(vector<vector<int>>& intervals) {
    vector<pair<int,int>> events;
    
    // Step 1: Build events
    for (auto &it : intervals) {
        int start = it[0];
        int end = it[1] + 1;  // +1 because intervals are inclusive
        events.push_back({start, +1});
        events.push_back({end, -1});
    }

    // Step 2: Sort by position
    sort(events.begin(), events.end());

    // Step 3: Sweep and track overlaps
    int active = 0, maxActive = 0;
    for (auto &e : events) {
        active += e.second;
        maxActive = max(maxActive, active);
    }

    return maxActive;
}

int main() {
    vector<vector<int>> intervals = {{5,10},{6,8},{1,5},{2,3},{1,10}};
    cout << minGroups(intervals) << endl;  // Output: 3
}
```

---

## 🧩 6. Why It Works Mathematically

The sweep line converts discrete intervals into a **difference array**:

* At each **start**, increment count.
* At each **end + 1**, decrement count.

If you take a **prefix sum** of this difference array,
the value at each point tells you **how many intervals are active** at that time.

Hence, it’s effectively a **prefix sum on sorted boundaries**.

---

### Equivalent Problems

* Minimum Number of Meeting Rooms
* Counting Maximum Overlap
* CPU Scheduling
* Number of Concurrent Users on a Site

---

## 🧾 Summary

| Concept          | Meaning                                 |
| ---------------- | --------------------------------------- |
| Build Events     | Convert intervals into (+1, -1) markers |
| Sort             | Process in chronological order          |
| Sweep            | Maintain active interval count          |
| Result           | Maximum active count seen               |
| Time Complexity  | O(n log n)                              |
| Space Complexity | O(n)                                    |
| Common Use       | Interval overlap or grouping problems   |

---

## 💬 Quick Reminder

When you see an **interval-based problem**, always ask:

> “Can I treat each start/end as an event and just count how many are active at once?”

If yes → it’s a **Sweep Line Problem** 💡