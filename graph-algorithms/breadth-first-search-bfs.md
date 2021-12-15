---
description: >-
  Traversing a graph by examining all nodes at the same distance from the
  original node before going to the next "level"
---

# Breadth First Search (BFS)

#### The Problem:

BFS solves an instance of the shortest paths problem where all edge weights are the same.  The shortest paths problem is finding the shortest path from vertex v to all other vertices in G, where distance is the sum of all edge weights on the path from v to u. The intuition behind bfs is to traverse a graph "level by level."  Since all edges are the same weight, all vertices in the current "level" will be the shortest distance from v (this can be proven by a simple proof by contradiction: assume v isn't the shortest, this means it would have been traversed earlier == contradiction).

Here is a basic iterative implementation of BFS:

```
def bfs(G, v):
    for all vertices in G:
        dist_to[u] = infinity
    queue = []
    queue.append(v)
    dist_to[v] = 0
    while queue:
        current = queue.pop(0)
        for all edges connectd to current:
            if dist_to[u] == infinity:
                queue.append(u)
                dist_to[u] = dist_to[current] + 1
```

In the code above we get a mapping dist\_to, where every key is mapped to a value, which is the shortest distance from v to this given vertex (which solves the shortest paths problem).  Another interesting observation is that the BFS implementation is the same as DFS, the only differences is BFS uses a queue and DFS uses a stack.
