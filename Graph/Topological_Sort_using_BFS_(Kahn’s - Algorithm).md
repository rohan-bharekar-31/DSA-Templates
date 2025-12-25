
# Topological Sort (BFS – Kahn’s Algorithm)

## Algorithm Name

Topological Sort using BFS (Kahn’s Algorithm / Indegree-based)

## Template (Adjacency List, Disconnected Graph)

```cpp
vector<int> topoSort(int V, vector<vector<int>>& adj) {
    vector<int> indegree(V, 0);

    // Step 1: Calculate indegree of each node
    for (int u = 0; u < V; u++) {
        for (int v : adj[u]) {
            indegree[v]++;
        }
    }

    // Step 2: Push all nodes with indegree 0
    queue<int> q;
    for (int i = 0; i < V; i++) {
        if (indegree[i] == 0) {
            q.push(i);
        }
    }

    // Step 3: BFS
    vector<int> topo;
    while (!q.empty()) {
        int node = q.front();
        q.pop();
        topo.push_back(node);

        for (int neighbor : adj[node]) {
            indegree[neighbor]--;
            if (indegree[neighbor] == 0) {
                q.push(neighbor);
            }
        }
    }

    return topo;
}
```

## Time Complexity

```
O(V + E)
```

## Space Complexity

```
O(V)
```

---

### ⚠️ Important Notes (for quick recall)

* Works **only for Directed Graph**
* If `topo.size() < V` → **cycle exists**
* Uses **BFS + indegree**
* Multiple valid topological orders possible

