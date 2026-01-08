
# Shortest Path using Bellman–Ford

### Algorithm Name

**Bellman–Ford Algorithm**

---

### Generic C++ Template

```cpp
class BellmanFord {
public:
    vector<int> shortestPath(int V, vector<vector<int>>& edges, int src) {
        // Step 1: Initialize distance array
        vector<int> dist(V, 1e9);
        dist[src] = 0;

        // Step 2: Relax all edges V-1 times
        for (int i = 1; i <= V - 1; i++) {
            bool updated = false;

            for (auto &e : edges) {
                int u = e[0];
                int v = e[1];
                int wt = e[2];

                if (dist[u] != 1e9 && dist[u] + wt < dist[v]) {
                    dist[v] = dist[u] + wt;
                    updated = true;
                }
            }

            // Optimization: stop early if no update
            if (!updated) break;
        }

        // Step 3: Check for negative cycle
        for (auto &e : edges) {
            int u = e[0];
            int v = e[1];
            int wt = e[2];

            if (dist[u] != 1e9 && dist[u] + wt < dist[v]) {
                // Negative cycle detected
                return {}; // or throw / mark cycle
            }
        }

        return dist;
    }
};
```

---

### Key Properties (mental note)

* Works for **directed & undirected graphs**
* **Handles negative weights**
* **Detects negative cycles**
* No greediness → global relaxation
* Based on **DP on number of edges**
* Graph represented as **edge list**

---

### Complexity

```
Time  : O(V × E)
Space : O(V)
```

---

### Invariant (VERY important 🔥)

After the **k-th iteration**:

> All shortest paths using **≤ k edges** are correctly computed.

---

### One-line memory hook

> **Bellman–Ford = relax all edges until distances stabilize**

---
