---
description: Another algorithm for solving the minimum spanning tree problem.
---

# Prim's Algorithm

#### Description:

Prim's algorithm also follows from the meta algorithm, where we have some set X that grows one edge per iteration. The actual implementation of Prim's is almost the same as Dijkstra's, the only difference is that the priority queue is filled by edge weights rather than path weights. Again it works because of the cut property, as we are only adding one edge at a time that connects a set S to V - S.

```
def prims(G, w):
    for all vertices in G:
        cost[u] = infinity
        prev[u] = nil
    cost(any node picked at random) = 0
    H = makequeue(V)
    while H:
        current = deleteMin(H)
        for all edges connected to current:
            if cost[u] > w(u, current):
                cost[u] = w(u, current)
                prev[u] = current
                decreaseKey(H, u)
```
