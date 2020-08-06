---
title: Minimum Spanning Tree
description: Using Kruskals Algorithm to find minimum spanning tree.
date: 2020-08-06
---

## What is a spanning tree ?

A <ins class="sub-ins-2">spanning</ins> tree is a subset of Graph G, which <ins class="sub-ins-2">connects</ins> all the vertices with <ins class="sub-ins-2">minimum</ins> possible number of edges connected. A spanning tree cannot have <ins class="sub-ins-2">cycles</ins> and it cannot be disconnected as well.

## And what is a minimum spanning tree ?

A <ins class="sub-ins-2">minimum</ins> <ins class="sub-ins-2">spanning</ins> tree (MST) or minimum weight spanning tree is a subset of a (connected, edge-weighted, undirected) Graph G that connects all the vertices together.

Minimum spanning tree can't form any <ins class="sub-ins-2">cycles</ins> and they also have to take care of the total edge weight. The total edge weight has to be <ins class="sub-ins-2">minimum</ins> in the case of minimum spanning tree.

That is, it is a spanning tree whose sum of edge weights is as small as possible.

### How Kruskals algorithm works:

Kruskals algorithm falls under the class of greedy algorithms. A greedy algorithm basically finds the optimal choice at each step as it attempts to find the overall optimal way to solve the entire problem.

We start from the edges with the lowest weight and keep adding edges until we reach the goal of finding a route through each of these vertices.

The steps for implementing Kruskal's algorithm are as follows:

- Sort all the edges from low weight to high
- Take the edge with the lowest weight and add it to the spanning tree. If adding the edge created a cycle, then reject this edge.
- Keep adding edges until we reach all vertices.

---

Now, let us visualize Kruskal's algorithm using a diagramatic representation:

![krushkal](./assets/krushkal.png)

- Kruskals algorithm allows us to select the edge with the minimum weight.
- So we select the minimum weighted edge i.e., the edge with weight 2 in the diagram.
- As we can see we have two edges with weight '2', we select any one.

![krushkal](./assets/2.png)

- Since the other '2' is now the next minimum we select that edge.

![krushkal](./assets/3.png)

- We have the edge having weight '3' as the next minimum, so we select it.

![krushkal](./assets/4.png)

- We have another edge having weight '3' as the next minimum, so we select it.

![krushkal](./assets/5.png)

- Now as we can see including the third '3' gives us a cycle, so we exclude it and don't consider in making the minimum spanning tree.

![krushkal](./assets/6.png)

- Out of the any two '4' we can select any one of them, and we also observe that including the second '4' will lead us to a cycle and hence we ignore the second '4'.

And now we have connstructed a Minimum Spanning Tree using Krushkal's algorithm with a total weight of (4 + 3 + 3 + 2 + 2) = 13 which is the mininmum possible.
