
# Shortest Path using Dijkstra

### Algorithm Name

**Dijkstra’s Algorithm (Priority Queue / Min-Heap)**

---

### Generic C++ Template

```cpp
class Dijkstra {
public:
    vector<int> shortestPath(int V, vector<vector<pair<int,int>>>& adj, int src) {
        // Step 1: Initialize distance array
        vector<int> dist(V, 1e9);
        dist[src] = 0;

        // Step 2: Min-heap {distance, node}
        priority_queue< pair<int,int>, vector<pair<int,int>>, greater<pair<int,int>>> pq;

        pq.push({0, src});

        // Step 3: Process nodes in increasing distance order
        while (!pq.empty()) {
            auto [d, u] = pq.top();
            pq.pop();

            // Skip outdated entry
            if (d > dist[u]) continue;

            // Step 4: Relax adjacent edges
            for (auto &edge : adj[u]) {
                int v = edge.first;
                int wt = edge.second;

                if (dist[v] > dist[u] + wt) {
                    dist[v] = dist[u] + wt;
                    pq.push({dist[v], v});
                }
            }
        }

        return dist;
    }
};
```

---

### Key Properties (mental note)

* Works for **directed & undirected graphs**
* **Does NOT handle negative weights**
* Greedy → always expands **minimum distance node**
* Priority Queue ensures correct order
* Visited array **not mandatory** (distance check is enough)

---

### Complexity

```
Time  : O(E log V)
Space : O(V + E)
```

---

### One-line memory hook

> **Dijkstra = greedy relaxation using min-heap**

---

