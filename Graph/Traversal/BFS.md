
# Breadth First Search (BFS)

## Algorithm Name
Breadth First Search (BFS)

## Template (Adjacency List, Disconnected Graph)

```cpp
void bfs(int V, vector<vector<int>>& adj) {
    vector<bool> visited(V, false);
    queue<int> q;

    for (int i = 0; i < V; i++) {
        if (!visited[i]) {
            visited[i] = true;
            q.push(i);

            while (!q.empty()) {
                int node = q.front();
                q.pop();

                for (int neighbor : adj[node]) {
                    if (!visited[neighbor]) {
                        visited[neighbor] = true;
                        q.push(neighbor);
                    }
                }
            }
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


