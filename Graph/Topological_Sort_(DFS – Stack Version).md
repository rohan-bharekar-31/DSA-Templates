
# Topological Sort (DFS – Stack Version)

## Algorithm Name
Topological Sort using DFS (Stack-based / Post-order DFS)

## Template (Adjacency List, Disconnected Graph)

```cpp
void dfs(int node, vector<int>& visited, vector<vector<int>>& adj, stack<int>& st) {
    visited[node] = 1;

    for (int neighbor : adj[node]) {
        if (!visited[neighbor]) {
            dfs(neighbor, visited, adj, st);
        }
    }

    // push after visiting all neighbors (post-order)
    st.push(node);
}

vector<int> topoSort(int V, vector<vector<int>>& adj) {
    vector<int> visited(V, 0);
    stack<int> st;

    for (int i = 0; i < V; i++) {
        if (!visited[i]) {
            dfs(i, visited, adj, st);
        }
    }

    vector<int> topo;
    while (!st.empty()) {
        topo.push_back(st.top());
        st.pop();
    }

    return topo;
}
````

## Time Complexity

```
O(V + E)
```

## Space Complexity

```
O(V)
```

