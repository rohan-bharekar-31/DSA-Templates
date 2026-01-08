
# Shortest Path using Floyd–Warshall

### Algorithm Name

**Floyd–Warshall Algorithm**

---

### Generic C++ Template

```cpp
class FloydWarshall {
public:
    void shortestPaths(vector<vector<int>> &dist) {
        int n = dist.size();
        const int INF = 1e9;

        // Relax paths via each node k
        for (int k = 0; k < n; k++) {
            for (int i = 0; i < n; i++) {
                for (int j = 0; j < n; j++) {
                    if (dist[i][k] < INF && dist[k][j] < INF) {
                        dist[i][j] = min(
                            dist[i][j],
                            dist[i][k] + dist[k][j]
                        );
                    }
                }
            }
        }
    }
};
```

---

### Key Properties (mental note)

* All-pairs shortest path
* Handles **negative edges**
* No negative cycle allowed
* Works for directed & undirected graphs
* Adjacency matrix based
* DP on intermediate nodes

---

### Complexity

```
Time  : O(N³)
Space : O(1)
```

---

### Invariant (VERY important 🔥)

After the **k-th iteration**:

> All shortest paths using **only nodes {0…k} as intermediates** are correct.

---

### One-line memory hook

> **Floyd–Warshall = allow one more intermediate node each step**

---

