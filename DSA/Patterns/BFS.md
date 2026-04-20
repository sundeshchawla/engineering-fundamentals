https://cp-algorithms.com/graph/breadth-first-search.html

BFS uses a queue

Think of fire spreading across jumgle

Think of putting each vertice in the queue and maintaing a boolean queue for visited true/false.

once all nodes/vertices are visited queue would be empty.


used for graph traversal and to find shortest paths.


Complexity O(n+m)


# Pattern: BFS (Breadth-First Search)

## Core Idea
Use a queue. Visit nodes level by level (or layer by layer in a grid).
Guarantees shortest path in an unweighted graph/grid.

## When to reach for BFS
- Level-order traversal of a tree
- Shortest path in unweighted graph/grid
- "Minimum steps to reach X" problems
- Multi-source BFS (multiple starting points simultaneously)

## C++ Template — Tree BFS
```cpp
queue<TreeNode*> q;
q.push(root);
while (!q.empty()) {
    int sz = q.size();          // snapshot level size
    while (sz--) {
        auto node = q.front(); q.pop();
        // process node
        if (node->left)  q.push(node->left);
        if (node->right) q.push(node->right);
    }
}
```

## C++ Template — Grid BFS
```cpp
queue<pair<int,int>> q;
q.push({startR, startC});
visited[startR][startC] = true;
int dirs[4][2] = {{0,1},{0,-1},{1,0},{-1,0}};
while (!q.empty()) {
    auto [r, c] = q.front(); q.pop();
    for (auto& d : dirs) {
        int nr = r+d[0], nc = c+d[1];
        if (nr>=0 && nr<rows && nc>=0 && nc<cols && !visited[nr][nc]) {
            visited[nr][nc] = true;
            q.push({nr, nc});
        }
    }
}
```

## Complexity
- Time: O(V + E) for graphs, O(M×N) for grids
- Space: O(W) where W = max width of tree, or O(M×N) worst case for grid

## Problems solved
- [ ] 102. Binary Tree Level Order Traversal
- [ ] 200. Number of Islands (BFS)

## Confidence
 🟡   ← fill after session