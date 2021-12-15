---
description: >-
  DFS is a method of searching a graph, keeping track of pre and post order
  numbers.
---

# Depth First Search (DFS)

Depth first search is useful to determine connected components of a graph.

#### Recursive Method

The recursive method uses the frames opened during recursion as a stack. It can also be easily modified to be pre or post order traversal.

The following code uses DFS to find reachable nodes from v on graph G.

```
#psuedo code for populating a map of false values
visited = {v: False for all vertices in G}
def explore(G, v):
""" G is a graph, v is a vertex in G."""
    visted[v] = True
    #visit v now if pre-order traversal
    previsit(v)
    for all u connected to v:
        if !visted[u]:
            explore(u)
    #vistit v now if post-order
    visit(v)
#after running, visted has True values for all
#vertices reachable from v
```

#### Analysis of above code:

![From DPV (CS170 textbook)](<../.gitbook/assets/Screen Shot 2021-09-30 at 1.50.58 PM (1).png>)

Another interesting fact is that the edges traversed by DFS forms a tree.

The following is the general DFS algorithm using the recursive explore(G, v):

```
def dfs(G):
    visited={}
    
    for all vertice in G:
        visted[v] = False
    
     for all vertices in G:
         if !visited:
             explore(G, v) 
```

Note: to see if a graph is connected, we can define the visit function in explore to fill in a dictionary mapping vertices to a connected component number, which starts at 0 and is incremented every time explore is called in dfs. If this dictionary has the same value for every key, the graph is connected.

![From DPV](<../.gitbook/assets/Screen Shot 2021-09-30 at 2.07.08 PM (1).png>)

During dfs we can also keep a clock to give each node a pre and post order number, and these numbers have a plethora of properties that will help us in various tasks. One such task is topological sort. The procedure for topological sort on a DAG (directed acyclic graph) is to run dfs and record the post order numbers. Using properties of post order numbers, we can show that the linearized (sorted) output is given by the post order numbers ini descending order. This can be concluded using the observation that all descendants of a particular vertex must have a lower post order number. This also implies that sinks have the lowest numbers, and sources have the highest.

Extra: Iterative DFS

```
def dfs(G, v):
    visited = {}
    for all verticies in G:
        vistied[vertex] = False
    stack = []
    stack.append(v)
    while stack:
        current = stack.pop()
        if !visited[current]:
            visit(current)
        for all edges connected to current:
            if !visited[u]:
                stack.append(u)
```
