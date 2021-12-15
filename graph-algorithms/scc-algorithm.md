---
description: This is the algorithm for finding strongly connected components
---

# SCC Algorithm

#### Defining the problem:

The problem here is to take a graph G, and return disjoint sets of strongly connected components.  A strongly connected component is defined as a subset of vertices where all pairs of vertices u and v have an path from u to v and a path from v to u. We want to find a new graph, where every node is a meta node of all the nodes in a strongly connected component. Additionally, a key aspect of this graph is that it will be a DAG.

This leads to an interesting conclusion: all directed graphs have a DAG of SCC's.

#### The Algorithm:

To find a linear algorithm, we must first define a few properties of directed graphs:

Property 1 - if explore is called on u, all reachable nodes will be visited

Property 2 - The node with the highest post-order number must be in the source SCC

Property 3 - If C and C' are strongly connected components, and there is an edge from a node in C to a node in C' , then the highest post number in C is bigger than the highest post number in C' .

What follows from these properties is that we can find a source SCC using dfs.  However, we wanted to find sinks.  The solution to this is to realize that sources in G are sinks in the reverse of G.  This means we can use the following algorithm to make a DAG od SCCs:

1. Run DFS on the reverse of G
2. Use the post order numbers from step 1 to run explore on a sink in G to find the connected component. Remove this component and repeat on the next post order number that hasn't already been removed

