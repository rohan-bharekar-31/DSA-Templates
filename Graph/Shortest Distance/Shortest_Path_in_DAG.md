
#  Shortest Path in DAG

### Algorithm Name

**DAG Shortest Path (Topological Order + Relaxation)**

---

### Generic C++ Template

```cpp
class DAGShortestPath {
    void topoDFS(int u, vector<int>& vis, vector<vector<pair<int,int>>>& adj, stack<int>& st) {
        vis[u] = 1;
        for (auto &edge : adj[u]) {
            int v = edge.first;
            if (!vis[v]) {
                topoDFS(v, vis, adj, st);
            }
        }
        st.push(u);
    }

public:
    vector<int> shortestPath(int V, vector<vector<pair<int,int>>>& adj,int src) {
        // Step 1: Topological Sort
        vector<int> vis(V, 0);
        stack<int> st;
        for (int i = 0; i < V; i++) {
            if (!vis[i]) {
                topoDFS(i, vis, adj, st);
            }
        }

        // Step 2: Initialize distances
        vector<int> dist(V, 1e9);
        dist[src] = 0;

        // Step 3: Relax edges in topo order
        while (!st.empty()) {
            int u = st.top();
            st.pop();

            if (dist[u] == 1e9) continue;

            for (auto &edge : adj[u]) {
                int v = edge.first;
                int wt = edge.second;
                if (dist[v] > dist[u] + wt) {
                    dist[v] = dist[u] + wt;
                }
            }
        }

        return dist;
    }
};
```



---

### Key Properties (mental note)

* Works **only for DAG**
* Handles **negative weights**
* Faster than Dijkstra
* Order matters → topo order

---

### Complexity

```
Time  : O(V + E)
Space : O(V + E)
```

---

### One-line memory hook

> **DAG shortest path = DP on topo order**

