---
description: Kruskal's algorithm used for solving the minimum spanning tree problem.
---

# Kruskal's Algorithm

#### Description of the algorithm:

Kruskal's algorithm is a greedy algorithm in which we sort the edges by weight and add edges in ascending order, making sure that adding the particular edge doesn't form a cycle. The reason it works is because of the cut property.

![From DPV](<../.gitbook/assets/Screen Shot 2021-10-02 at 7.14.07 PM.png>)

#### Implementation:

Kruskal's algorithm can be implemented using the union find data structure. This data structure has a few important methods. Find(v) is a method that returns some label representing the disjoint set that v is in.  What the label is doesn't matter, what matters is that two vertices in the same set return the same label.  The other method is union(v, u), which combines the set containing u into the set with v.

```
def kruskal(G, w):
    for all vertices:
        make a singleton set with u
    X = {}
    sort edges by weight
    for all edges, in order:
        if find(u) != find(v):
            add edge(u, v) to X
            union(u, v)
    
```
