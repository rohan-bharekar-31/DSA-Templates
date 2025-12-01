# upper_bound vs lower_bound

| Aspect | lower_bound | upper_bound |
|--------|-------------|-------------|
| **Definition** | Finds first element ≥ target | Finds first element > target |
| **Return Value** | Iterator to first element ≥ target | Iterator to first element > target |
| **Behavior with Duplicates** | Points to the **first occurrence** of target (if duplicates exist) | Points to the **element after the last occurrence** of target (if duplicates exist) |
| **Use Case** | Find insertion point to maintain sorted order | Find range of duplicates (upper_bound - lower_bound = count) |
| **Example with `[1,2,2,4,4,4,5]` and target = 4** | Returns iterator to index **3** (first 4) | Returns iterator to index **6** (first element > 4) |
