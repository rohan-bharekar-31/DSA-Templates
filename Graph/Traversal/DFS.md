
# Depth First Search (DFS)

## Algorithm Name
Depth First Search (DFS)

## Template (Adjacency List, Disconnected Graph)

```cpp
void dfsUtil(int node, vector<vector<int>>& adj, vector<bool>& visited) {
    visited[node] = true;

    for (int neighbor : adj[node]) {
        if (!visited[neighbor]) {
            dfsUtil(neighbor, adj, visited);
        }
    }
}

void dfs(int V, vector<vector<int>>& adj) {
    vector<bool> visited(V, false);

    for (int i = 0; i < V; i++) {
        if (!visited[i]) {
            dfsUtil(i, adj, visited);
        }
    }
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

