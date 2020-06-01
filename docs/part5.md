---
title: "Part 5 - Graphs"
permalink: /part5/
nav_order: 7
published: true
---

# Graphs

We can solve many algorithmic problems by representing the problem as a *graph* and use a suitable graph algorithm. A typical example of a graph is a network of roads, which comprises of cities and the roads between them. In such a graph, the problem could be for example finding the route from city *a* to city *a*.

## Graph terms

*Graph* is made from *nodes* (or *vertexes*) and the *edges* between them. Below is a graph with five nodes and seven edges. We mark the amount of nodes with the letter *n* and the amount of nodes with the letter *m*. In addition, we number the nodes with integers *1, 2,... ,n*.

We say that two nodes are *adjacent*, if there is an edge between them. The *neighbors* of a node are the nodes which are connected with an edge, and the *degree* of a node is the amount of neighbors. In our example, the node *2* has neighbors *1*, *4* and *5*, so its degree is 3.

![Graph 1](https://github.com/centria/algo-and-data/raw/master/assets/images/graph1.png)  
source: [**Tietorakenteet ja algoritmit**](https://github.com/pllk/tirakirja/raw/master/tirakirja.pdf)

A *path* in a graph is a sequence going along the edges from the starting node to the target node. Below we can see two possible paths from node *1* to node *5* in our example graph. The first path is 1 &#8594; 2 &#8594; 5 and another path is 1 &#8594; 3 &#8594; 4 &#8594; 5.

![Graph 2](https://github.com/centria/algo-and-data/raw/master/assets/images/graph2.png)  
source: [**Tietorakenteet ja algoritmit**](https://github.com/pllk/tirakirja/raw/master/tirakirja.pdf)


A path is a *cycle*, if the starting and the ending nodes are the same, it has at least one edge and it does not go through the same node or edge more than once. Beloe we have an example cycle 2 &#8594; 4 &#8594; 5 &#8594; 2. If there are no cycles in a graph, we call it *acyclic*.

![Graph 3](https://github.com/centria/algo-and-data/raw/master/assets/images/graph3.png)  
source: [**Tietorakenteet ja algoritmit**](https://github.com/pllk/tirakirja/raw/master/tirakirja.pdf)


A graph is *connected*, if it has at least one node, and there is an edge between every pair of nodes. For example, the graph above is connected, but the graph below is not, as for example there is no edge between nodes *1* and *2*.

![Graph 4](https://github.com/centria/algo-and-data/raw/master/assets/images/graph4.png)  
source: [**Tietorakenteet ja algoritmit**](https://github.com/pllk/tirakirja/raw/master/tirakirja.pdf)

A graph can always be presented as a set of *connected components*. Above, the connected components are {1,3} and {2,4,5}. A node with not incident edges is itself a component. A graph that is itself connected has exactly one component, consisting the whole graph.

 A graph is a *tree*, if it is both connected and acyclic, like below. In a tree, the amount of edges is always one less than the amount of nodes, and there is a *simple edge* between each pair of nodes.

![Graph 5](https://github.com/centria/algo-and-data/raw/master/assets/images/graph5.png)  
source: [**Tietorakenteet ja algoritmit**](https://github.com/pllk/tirakirja/raw/master/tirakirja.pdf)


In a *directed* graph each edge has a direction, along which we have to travense in the graph. The directions restrict our travel in the graph. Below is an example of a directed graph, where we can go from node *1* to node *5* with path 1 &#8594; 2 &#8594; 5, but there is no way to travel from node *5* to node *1*.

![Graph 6](https://github.com/centria/algo-and-data/raw/master/assets/images/graph6.png)  
source: [**Tietorakenteet ja algoritmit**](https://github.com/pllk/tirakirja/raw/master/tirakirja.pdf)

In a *weighted* graph each edge has an associated weight, which typically represents the length of the edge. As we traverse a path in a weighted graph, the length of the path is the sum of the edges.

![Graph 7](https://github.com/centria/algo-and-data/raw/master/assets/images/graph7.png)  
source: [**Tietorakenteet ja algoritmit**](https://github.com/pllk/tirakirja/raw/master/tirakirja.pdf)

In the example above, the path 1 &#8594; 2 &#8594; 5 has a weight of *5 + 8 = 13*, and path 1 &#8594; 3 &#8594; 4 &#8594; 5 has a weight of *2 + 4 + 3 = 9*.

## Graphs in programming

There are several ways to represent a graph in programming. Choosing the proper representation is dependant on how we want to handle the graph in our algorithms, as each representation has their benefits. Let's see three ways to represent a graph.

## Adjacency list

One common way to represent a graph is to create an *adjacency list* for each node. The list tells, into which nodes we can traverse along with nodes. In the picture below is a graph and the adjacency list representation. 

![Graph 8](https://github.com/centria/algo-and-data/raw/master/assets/images/graph8.png)  
source: [**Tietorakenteet ja algoritmit**](https://github.com/pllk/tirakirja/raw/master/tirakirja.pdf)

If we want to create an adjacency list in C#...


HERE WILL BE MORE.

## BFS and DFS












[**Exercises here**](https://centria.github.io/algo-and-data/exercises/#part-5---graphs)