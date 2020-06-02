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

# Graphs in programming

There are several ways to represent a graph in programming. Choosing the proper representation is dependant on how we want to handle the graph in our algorithms, as each representation has their benefits. Let's see three ways to represent a graph.

## Adjacency list

One common way to represent a graph is to create an *adjacency list* for each node. The list tells, into which nodes we can traverse along with nodes. In the picture below is a graph and the adjacency list representation. 

![Graph 8](https://github.com/centria/algo-and-data/raw/master/assets/images/graph8.png)  
source: [**Tietorakenteet ja algoritmit**](https://github.com/pllk/tirakirja/raw/master/tirakirja.pdf)

If we want to create an adjacency list in C# we can create a List

```cs
List<int>[] graph = new List<int>[n + 1];
```

And we can initialize our adjacency list with

```cs
for (int i = 1; i <= n; i++)
{
  graph[i] = new List<int>();
}
```

Add edges to the lists with

```cs
graph[1].Add(2);
graph[1].Add(3);
graph[1].Add(4);
graph[2].Add(4);
graph[2].Add(5);
graph[3].Add(4);
graph[4].Add(5);
```

Adjacency list is a quite often a useful way to create a graph, as we might for example want to find out, which ndos we can get to from a certain node, traversing the edges. For example, the following code goes through all the nodes, we can traverse to from node *x*:

```cs
foreach (int i in graph[xS])
{
  // Do something with the node i
}
```

If the graph is undirected, or we can move along the edges both ways, we can record the graph similarly, as long as we save each edge both ways. If the graph would we weighted, we can save both the node and the weight.

## Edge list

Another way of saving a graph is to create an *edge list*, which contains all the edges in the graph. In C#, we caon create a list

```cs
List<Edge> edges = new List<Edge>();
```

which contains the following kind of edges:

```cs
public class Edge
{
  public int beginning, end;

  public Edge(int beginning, int end)
  {
    this.beginning = beginning;
    this.end = end;
  }
}
```

The following code creates an edge list which corresponds with our example graph:

```cs
edges.Add(new Edge(1,2));
edges.Add(new Edge(1,3));
edges.Add(new Edge(1,4));
edges.Add(new Edge(2,4));
edges.Add(new Edge(2,5));
edges.Add(new Edge(3,4));
edges.Add(new Edge(4,5));
```

Edge list is a good representation for algorithms, where we want to go through as easily as possibly all the edges in a graph and there is no need to find out all the edges of a certain node.

## Adjacency matrix

![Graph 9](https://github.com/centria/algo-and-data/raw/master/assets/images/graph9.png)  
source: [**Tietorakenteet ja algoritmit**](https://github.com/pllk/tirakirja/raw/master/tirakirja.pdf)


*Adjacency matrix* is a two-dimensional array, which tells about all the edges, if they exist in a graph. The value in matrix row *a* in column *b* determines, if there is an edge from node *a* to *b*. Above you can see an example of an adjacency matrix. In the example, each value is either 0 (no edge) or 1 (edge exists).

In C#, we can do the adjacency matrix like follows:

```cs
int[,] graph = new int[n + 1, n + 1];
```

After which we can form the matrix like this:

```cs
graph[1, 2] = 1;
graph[1, 3] = 1;
graph[1, 4] = 1;
graph[2, 4] = 1;
graph[2, 5] = 1;
graph[3, 4] = 1;
graph[4, 5] = 1;
```

If the graph would be weighted, we could similarly define the weights as the values in the matrix. The advantage of adjacency matrix is that we can easily determine the existence of certain edge from the graph. This does how ever take up plenty of memory and it cannot ve used, if there are a large amount of nodes.


# Traversing a graph

Next we will get to know two essential algorithms, which traverse the nodes and edges of a graph. First we will examine *depth-first search (DFS)* which is a more general algorithm for traversing a graph, and then we will examine *breadth-first search (BFS)*, which is used for finding the shortest paths in the graph.

## DFS

*depth-first search (DFS)* is a general tool for handling graphs, with which we can determine multiple aspects of the structure of a graph. When we begin examining the graph with DFS, we first must deterine, from which node we begin (root node). The search continues to all the nodes in turn, which are accessible from the starting node via edges.

The DFS maintains information about each node, if they have been visited or not. When the search reaches a node it has not visited yet, it marks the node visited and begins to traverse the edges beginning from said node. With each edge the search advances to the parts of a graph, which are accessible via an edge. Once the search has gone through all the edges, it backs away the same route from whence it came to the edge.

![DFS](https://github.com/centria/algo-and-data/raw/master/assets/images/dfs.png)  
source: [**Tietorakenteet ja algoritmit**](https://github.com/pllk/tirakirja/raw/master/tirakirja.pdf)

In the picture above you can see an example of depth-first search in action. With each step, gray nodes are where the search has visited. In this example, the search starts from node *1*, from which it can access nodes *2* and *3*. The search will advance to node *2* first, from which it can again get to nodes *4* and *5*. After this the search does not find more edges from this part of the graph, so it will back away the same route, back to node *1*. The search will continue to node *3*, from which it cannot access more nodes. Now the search has visited all the nodes, it can acess from node *1*.

DFS is convenient to create recursively in the following manner:

```console
search(node)
  if visited[node]
    return
  visited[node] = true
  for neighbor in graph[node]
    search(neighbor)
```

The search begins, when we call the method *search* with the starting node as a parameter. With each call the method checks first, if we have visited the node it has been given, and return if so. Otherwise the method marks the node visited and recursively advances to all its neighbors. The search takes time *O(n+m)*, as we handle each node and edge at maximum once.

How could we use DFS? Here are a few examples for usage:

### Finding a path

With DFS we can find a path from node *a* to node *b*, if such a path exists. This is done by starting the search from node *a* and returning, when we get to node *b*. If there are several paths, DFS will find one of them, depending on the handling order of the nodes.

## Connections and components

An undirected graph is connected, if all the nodes are connected to each other. We can examine the connections of a graph by starting our search from any node and examining, if the search reaches all the nodes of the graph. In addition, we can find all the connected components of the graph by going through the nodes and beginning a new search, whenever we come across an unvisited node. Each search thus forms one component.

## Finding cycles

If an undirected graph contains a cycle, we notice this with DFS, if we come to a visited node via another route (than the one we have used to get there earlier). Thus we can find a cycle from the graph, if such exists.

## BFS

*breadth-first search (BFS)*, alike DFS, goes through all the nodes, it can access with edges from the given root node. The difference comes from the order they are accessed with. BFS traverses the nodes by *levels* so, that it handles the nodes in the order in which they were first encountered during the search.

Even though we could use BFS as a general tool for traversing a graph like DFS, we usually use it when we are interested in the *shortest paths*. With breath-first search we determine the length of the shortest path, or the *distance* from the rootnode to each node we encounter during the search. In this example, we assume that the length of the path is determined by the amount of edges, i.e. the shortest path is the one with least edges along the way.

![BFS](https://github.com/centria/algo-and-data/raw/master/assets/images/bfs.png)  
source: [**Tietorakenteet ja algoritmit**](https://github.com/pllk/tirakirja/raw/master/tirakirja.pdf)

Above you can see an example of BFS in action, when we start our search from node *1*. First we handle node *1*, from which we can access nodes *2* and *3*. This means, that the shortest paths to nodes *2* and *3* are 1 &#8594; 2 and 1 &#8594; 3, and the distance to these nodes is 1. Then we handle the node *2*, from which we can access new nodes, *4* and 5*. This lead to shortest paths to *4* and 5* being 1 &#8594; 2 &#8594; 4 and 1 &#8594; 2 &#8594; 5, and the distance to these nodes is 2. Finally, we handle nodes 3, 4 and 5 in this order, from which we cannot access any more nodes.


One usual way to implement breadth-first search is to use a *queue* (In C#, [**Queue**](https://docs.microsoft.com/en-us/dotnet/api/system.collections.generic.queue-1?view=netcore-3.1)). With a queue we can traverse the nodes in the order we have found them with BFS. We assumme, that the *queue* has a method *enqueue*, which adds an element to the end, and a method *dequeue*, which returns and removes the first element from the queue. The following code implements BFS beginning from the root-node *root*:

```console
queue.enqueue(root)
visited[root] = true
distance[root] = 0
while queue is not empty
  node = queue.dequeue()
  for neighbor in graph[node]
    if visited[neighbor]
      continue
    queue.enqueue(neighbor)
    visited[neighbor] = true
    distance[neighbor] = distance[node] +1
```

First we add the root-node to the queue and mark we have visited it, and the distance to the root is 0. after this we begin to handle the nodes in the order as they are in the queue. We will handle a node by going through its neighbors. If we have not visited a neighbor before, we add it to the queue and update the arrays. The search takes *O(n+m)* time, as we handle each node and edge at maximum once.

## Example: Labyrinth

We are in a labyrinth and we want to get from square *A* to square *B*. With each turn, we can move one step up, down, left or right. Can we get from *A* to *B*, and if we can, what is the shortest possible route? In the example below, the shortest path from *A* to *B* is formed with 9 steps. The left side illustrates the labyrinth, and the right side the same situation as a graph.

![Labyrinth](https://github.com/centria/algo-and-data/raw/master/assets/images/labyrinth.png)  
source: [**Tietorakenteet ja algoritmit**](https://github.com/pllk/tirakirja/raw/master/tirakirja.pdf)

Notice, that we do not have to separately change the labyrinth into a graph, but we can do the search on *implicit graph*. This means, that we do the search to the labyrinth in its own presentation form. In practice, the labyrinth is handly to save as a two-dimensional array, which tells which squares are walls. Then we can do for example a BFS like follows:

```console
search(y, x)
  if y < 0 or x < 0 or y >= n or x >= n
    return
  if wall[y,x] or visited [y,x]
    return
  visited[y,x] = true
  search(y+1, x)
  search(y-1, x)
  search(y, x+1)
  search(y, x-1)
```

We begin our search from a coordinate *y,x*. Our first check is to determine we keep inside our grid, and the second one to make sure we have not come to a wall or visited the node already. Then we search all the neighboring nodes recursively, in order up, down, right, left.







[**Exercises here**](https://centria.github.io/algo-and-data/exercises/#part-5---graphs)