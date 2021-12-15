---
description: >-
  Solving the shortest paths problem for graphs with unequal nonnegative edge
  weights.
---

# Dijkstra's Algorithm

#### The Problem:

BFS solves the shortest paths problems for that case where all edges are the same length.  But what about the case when there are different edge weights.  Dijkstra's solves this problem as long as all edges are nonnegative.

#### The Algorithm:

The intuition behind dijsktra's is essentially "best-first search."  We traverse the graph by keeping some note of the smallest path to some edge that hasn't been visited yet.  This works because if we consider some vertex v we are visiting, the previous vertex in the path u must be the shortest path to u.  If there was a shorter path to some vertex w that is connected to v, it also would have already been considered by the algorithm, and it would have been the previous to v.  But it isn't, so this is a contradiction.  The way we keep track of the next shortest path is be using a priority queue, a min-heap for example.  Then, the implementation is essentially the same as BFS but with a heap instead of a queue.

This is the code, not that prev marks the previous vertex of u on the path from v to u.  This is so we know the shortest path from v to u if wee needed that information.

```
def dijkstra(G, v):
    for all verticies in G:
        dist_to[u] = infinity
        prev[u] = nil
    min_heap = createMinHeap(verticies of G, sorted by dist_to)
    while min_heap:
        current = min_heap.removeMin()
        for all edges connected to current:
            if dist_to[u] > dist_to[current] + length(current, u):
                dist_to[u] = dist[current] + length(current)
                prev[u] = current
                #reshape heap based on new dist
                min_heap.decreaseKey(u, dist_to[u])
    
```

The bottleneck of Dijsktra's is the data structure we use for the priority queue.  There are many different data structures that solve the heap problem, including the binary heap, array based heap, and fibonacci heap.
