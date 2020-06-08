---
title: "Part 6 - Shortest paths"
permalink: /part6/
nav_order: 8
published: true
---

# Shortest paths in graphs

Many of the problems related to graphs are about finding the *shortest path* from one node to another. For example, we could want to find out, what is the fastest route between two street addresses, or which is the cheapest way to fly from one city to another. In these and other applications it's important to find the shortest path efficiently.

We have used *breadth-first search (BFS)* to find the shortest paths. This is a good solution for finding the paths, whose amount of edges is the smallest. In this part, we concentrate on a more demanding situation, where the graph has been *weighted* and we want to find the paths, where the sum of the weights is the smallest. This time we cannot use BFS but we need more advanced techniques.

There are several algorithms to finding shortest paths in a weighted graph, and they have different attributes. In this part we shall look into *Bellman-Ford* and *Dijkstra's* algorithms, which search the the shortest path from given source-node to all the nodes in the graph. After these we will examine *Floyd-Warshall* algorithm, which searches all the shortest paths between all the nodes in the graph.

The most common situation in graph problems is to find the shortest path from node *a* to node *b*. Finding a single shortest path usually requires that we find other shortest paths before it, as well. Thus we concentrate to the most common problem from the beginning, where we have chosen a node as the source-node and we want to define for *each* node, how long is the shortest path from the source-node to that node, or what is the distance from the source.

![Weighted graph 1](https://github.com/centria/algo-and-data/raw/master/assets/images/weighted1.png)  
source: [**Tietorakenteet ja algoritmit**](https://github.com/pllk/tirakirja/raw/master/tirakirja.pdf)

In the picture above is an example of a graph, where the node *1* is the chosen source node, and next to each node is marked the distance to them in red. For example, to node *5* the distance is 9, since the shortest path from node *1* to node *5* is 1 &#8594; 3 &#8594; 5, whose distance is *2 + 7 = 9*. We will use this graph as our example, when we examine the next two algorithms for searching the shorest paths.

# Bellman-Ford algorithm

*The Bellman-Ford algorithm* searches the shortest paths from a given source-node to all the nodes in the graph. The algorithm forms an array, which describes for a node the distance from the source-node. The algorithm works in any graph, as long as there is no negative cycle, i.e. a cycle whose sum of weights is negative.

The Bellman-Ford maintains an *approximation* of the distances of the nodes, so that in the beginning the distance to the source-node is *0* and the distance to all the other nodes is *infinite*. After this the algorithm starts to improve the distance by looking for edges in the graph, through which it could shorten the distance. With each step the algorithm searches an edge *a &#8594; b*, with which we can get to node *b* with a shorter distance from node *a* than previously. When none of the estimates can be improved, the algorithm ends and all the distances correspond to the real shortest path distances.

![Weighted graph 2](https://github.com/centria/algo-and-data/raw/master/assets/images/weighted2.png)  
source: [**Tietorakenteet ja algoritmit**](https://github.com/pllk/tirakirja/raw/master/tirakirja.pdf)

The picture above shows an example of Bellman-Ford in action, with the source-node of *1*. Next to each node, the distance to them has been marked with red: In the beginning, the distance for node *1* is *0* and the distance to all the other nodes is *infinity*. Each change of distance can be seen in the picture as a separate step. First, we improve the distance to node *2* by going through the edge *1 &#8594; 2*, and get the distance of 8. Then we improve the distance to node *3* with edge *1 &#8594; 3*, getting the new distance of 2. We continue similarly, until we cannot improve any distance and all the distances correspond with the shortest path distances.

Bellman-Ford is convenient to store as an *edge list*, where we have stored the *source* and *target* nodes for all the edges, as well as weight. We will implement the algorithm so, that it consists of *repetition of relaxations*, where each repetition goes through all the edges of the graph and tries to improve the distance approximation with them. We can implement the algorithm like so:

```console
while true
  change = false
  for edge in edges
    current = distance[edge.end]
    new = distance[edge.source]+edge.weight
    if new < current
      distance[edge.end] = new
      change = true
  if not change
    break
```

With each repetition the algorithm goes through the edges of the graph and examines each edge, what is the current distance to the target node and what is the new distance, if we go to the node through the edge. If the new distance is smaller, we update that to be the distance of the node. In the variable *change* we store the information of has something changed during the repetition, and if not, we end the algorithm.

## Analysing the algorithm

We have described and implemented the Bellman-Ford algorithm, but how can we be sure, that it finds the shortest path, and how fast does it work? We have to make two observations to answer these questions.

Our first observation is, that if *n1 &#8594; n2 &#8594; ... &#8594; nk* is the shortest path from node *n1* to node *nk*, also path *n1 &#8594; n2* is the shortest path from *n1* to *n2*, and *n1 &#8594; n2 &#8594; n3* is the shortest path from *n1* to *n3*, and so on. Thus the beginning of each shortest path is also the shortest path to the corresponding nodes. If this wasn't true, we could improve our shortest path from node *n1* to *nk* by improving some beginning of the path, which would cause a contradiction.

Our second observation is, that in a graph of *n* nodes, the shortest path to a node can include a maximum of *n-1* edges, when we assume that there is no negative cycle in the graph. If the path would include *n* or more edges, some node would be on the path several times. This is not possible, as there would be no reason to go through the same node multiple times, when we want to achieve the shortest path.

Let's see what happens in the repetitions of the algorithm. After the first one, we have found the shortest paths with maximum of one edge. After the second one we have found the shortest paths with a maximum of two edges. This continues, until after *n-1* repetitions we have found the shortest paths, with a maximum of *n-1* edges. As any of the shortest edges cannot have more edges, we have gone through all the shortest paths. To execute our algorithm, we require a maximum of *n-1* repetitions, which all go through the edges of the graph in time *O(m)*. Thus the algorithm finds the shortest paths in time *O(nm)*.

![Negative graph 1](https://github.com/centria/algo-and-data/raw/master/assets/images/negative1.png)  
source: [**Tietorakenteet ja algoritmit**](https://github.com/pllk/tirakirja/raw/master/tirakirja.pdf)

What happens, if the graph has a negative cycle? In the picture above, we have a negative cycle *2 &#8594; 4 &#8594; 5 &#8594; 2*, whose weight is *-2*. In this situation the Bellman-Ford algorithm will continue forever, as we can shorten the paths going through the cycle infinately. The problem actually lies in the definition: a shortest path is not a reasonable statement, if the path includes a negative cycle. We can use Bellman-Ford to detect negative cycles in a graph: If a distance could be improved after *n-1* repetitions, the graph has a negative cycle.


# Dijkstra's algorithm

*Dijkstra's algorithm* is an enhanced version of the Bellman-Ford, whose functionality relies on the assumption that there are no negative edges in the graph. Alike to Bellman-Ford, Dijkstra's algorithm maintains approximation of distances from source-node to other nodes. The difference is how Dijkstra's algorithm improves the distances.

In Dijkstra's algorithm nodes are in two classes: visited and non-visited. In the beginning, all the nodes are non-visited. With each step the algorithm finds a node that has not been visited, and whose distance estimation is the smallest. Then the algorithm goes through all the edges originating from said node and tries to improve distances with them. After this node has been visited and the distance for it does not change, we have found out its final distance.

![Dijkstra 1](https://github.com/centria/algo-and-data/raw/master/assets/images/dijkstra1.png)  
source: [**Tietorakenteet ja algoritmit**](https://github.com/pllk/tirakirja/raw/master/tirakirja.pdf)

In the example above we see an example of Dijkstra's algorithm in action. The gray color of a node means it has been visited. At first we begin with node *1*, as its distance of *0* is the smallest. Now we have left nodes *2*, *3*, *4* and *5*, of which we choose node *3*, as its distance of *2* is the smallest. After this we choose to visit node *2*, whose distance is *6*. We continue this until we have visited all the nodes in the graph.

With Dijkstra's algorithm we search *n* times a non-visited node, whose distance approcimation is the smallest. As we want to have the algorithm as efficient as possible, we have to be able to find the nodes fast. Implementing Dijkstra's algorithm is most convenient with an adjacency matrix or adjacency list.

```console
Dijkstra(graph, source):
  
  for each node in graph
    dist[node] = infinity	
    previous[node] = undefined	
  
  dist[source] = 0
  
  Q = the set of all nodes in graph
  
  while Q is not empty
    n = node in Q with smallest dist[]
    remove n from Q
    
    for each neighbor of n
      alt = dist[n] + dist_between(n, neighbor)
      if alt < dist[neighbor]	
        dist[neighbor] = alt
        previous[neighbor] = n
	
  return previous[]
```

In our algorithm, we initialize all the distances to be infinite, and have the previous node of the known shortest path to be undefined (or *null*). Then we create a *set Q*, where all the nodes are put. We go through our *Q* until it is empty, with each repetition removing the nodes with shortest possible paths. In the for-each-loop we visit the neighbors of *n*. If the *alt* is less than the distance of the neighbor, the distance for said neighbor is updated. This is called *relaxation*. Continue going through the loops until *Q* is empty.

## Analysing the algorithm

Dijkstra's algorithm is a *greedy algorithm*, as at each step it searches non-visited node whose distance is smallest, after which the distance of said node does not change. How can we be sure, that we have found the correct distance? 

We can think of this matter from another perspective: If the distance could be still improved, the graph should have at least one another non-visited node, via which we could form a shorter path. As we know that all the other paths available are greater or equal than the one we are visiting and the distance for those nodes cannot become shorter, as there are no negative edges in the graph. For this reason we can safely choose to visit the node with the smallest distance and fix its distance.

So the Dijkstra algorithm works correctly, if there are no negative edges in the graph, but how fast is it? First the algorithm goes through the edges and nodes of the graph, taking *O(m + n)* time. The main part of the algorithm goes through the set of all the nodes in *O(n)*, and for each node *n* a maximum of *O(m)* edges, creating a time complexity of *O(m^2)*. As we know, this is not very fast. 


There is another way to do create the algorithm, and that is with a *priority queue* (also known as *heap*). Unfortunately, that has not been implemented in C#, but let's look at that as well:

```console
heap.push((0,source))
while not heap.empty()
  node = heap.pop()[1]
  if visited[node]
    continue
  visited[node] = true
  for edge in graph[node]
    current = distance[edge.end]
    new = distance[node]+edge.weight
    if new < current
      distance[edge.end] = new
      heap.push((new,edge.end))
```

This example uses an adjacency list. Notice, that in the heap there can be *multiple* distances for a node in the heap, as we add a new node to the heap each time the distance improves. We will visit each node only once, as every time we get a new node from the heap for visiting, we first make sure that we have not visited said node earlier.

This implementation first goes through all the nodes and edges in time *O(n+m)*. The heap requires operations, and at worst case for each edge we have to add another element to the heap, which takes *O(m log m)*. On the other hand, we will eventually remove all the nodes from the heap, taking also *O(m log m)*. Thus the complete time complexity for this implementation is *O(n + m log m)*.

What happens, if the graph does have a negative edge? Then the Dijkstra's algorithm doesn't necessarily work correctly. In the example below, the greedy algorithm takes the upper path and decides that shortest distance from *1* to *5* is *8*. However, the actually shortest distance would be the path below, whose distance is only *6*.

![Negative graph 2](https://github.com/centria/algo-and-data/raw/master/assets/images/negative2.png)  
source: [**Tietorakenteet ja algoritmit**](https://github.com/pllk/tirakirja/raw/master/tirakirja.pdf)

## Example: Trip planner

Now we have all the information required to create a *trip planner*, or a system, with which we can find different transportation routes in a city. We can model the city as a graph, whose nodes are locations in the city and the edges are possible connections between the locations. The trip planner should give the *fastest* route from location *a* to location *b*.

Creating a trip planner has one extra challenge: transportation have timetables, which limit their use. For example a bus could move every 10 minutes. We have to take our arrival times into account when planning our trips. We can achieve this by saving the edges of the graph in form "*the trip begins at time* x *and ends at time* y".

As all the trips take a positive amount of time, we can search the routes with Dijkstra's algorithm. We will implement the algorithm so, that to each location we define the *earliest* time, when we can get to a certain location. In the beginning we know, that we are at our starting position when we begin our trip. Then we visit another location, go through the connections starting from there, into which we can get to by keeping an optimal timetable. We can make our search significantly more efficient if we only take into consideration from each bus line only the first start, which we can make. This is justified, as in no situation could it be a better idea to wait for the later start.

![Trip planner 1](https://github.com/centria/algo-and-data/raw/master/assets/images/trip1.png)  
source: [**Tietorakenteet ja algoritmit**](https://github.com/pllk/tirakirja/raw/master/tirakirja.pdf)


The picture above shows an example, where we want to move from location *1* to location *3*, and we begin our trip at *13:15*. From *1* to *2* there is a connection every 10 minutes, whose duration is 7 minutes, and from *1* to *3* there is a connection every 30 minutes, whose duration is 10 minutes. Thus we can get to location *2* at *13.27* and to location 3 at *13:40*.

Then, from *2* goes another connection to *3* every 5 minutes, with duration of *2* minutes. With this we can get to location *3* at *13:32*, so the fastest route goes through location *2*.

In reality, this could be enhanced in multiple ways. For example when we find any route to our end-point of the route, we could ignore the other locations, where we will reach later than to that end-point.

# Floyd-Warshall algorithm

Let's next look into a problem, where we want find the shortest paths *from all* nodes *into all* nodes. One way to solve this would be to run Bellman-Ford or Dijkstra's algorithm for each node of the graph. We can however solve this more directly by searching all the paths *simultaneosly* with the *Floyd-Warshall* algorithm.


The *Floyd-Warshall algorithm* forms a *n * n* sized *distance matrix*, where at row *a* column *b* is the shortest path distance from the node *a* to node *b*. The algorithm first initializes the matrix so, that it only contains the distances which can be traveled using a single edge, and all the others are marked with infinity. Then the algorithm takes *n* repetitions, numbered *1, 2, ..., n*. At a repetition *k* the algorithm searches for paths, which can go through the node *k* (called *intermediate node*) as a and possibly other nodes from *1, 2, ..., k-1* to be intermediate nodes. If such a path improves the distance, we update the new values to the matrix. In the end each node has been an intermediate node, and we have found all the shortest paths.

![Floyd-Warshall](https://github.com/centria/algo-and-data/raw/master/assets/images/floyd-warshall.png)  
source: [**Tietorakenteet ja algoritmit**](https://github.com/pllk/tirakirja/raw/master/tirakirja.pdf)

In the picture above, we have an example of Floyd-Warshall in action. On the first repetition we search for paths, where *1* would be gone through. There are no such paths, as *1* cannot be reached from any other node, so the matrix does not change. On repetition *2* we notice, that we can reach node *4* from *1* by using *2* as an intermediate node, giving us the distance of *8*. Similarly we can get through *2* to node *4* from node *3*, getting the distance of *5*. We continue this way, until after repetition *4* we have reached all the distances and the matrix is complete.

The nice side of Floyd-Marshall algorithm is, that it is very easy to implement. We only need to create three inner for-loops, which create the updates of the matrix. For the following example, the variable *k* determines which repetition we're at, i.e. which node is the intermediate node. With each repetition we go through all the node pairs *(i,j)* and try to improve the distance between them by going through the node *k*.

```console
for k = 1 to n
  for i = 1 to n
    for j = 1 to n
      distance[i,j] = min(distance[i,j], distance[i,k]+distance[k,j])
```

The time complexity is clearly *O(n^3)*, as it comprises of three for-loops inside one another.

## Analysing the algorithm

Why does the Floyd-Marshall work? We can understand the algorithm by looking at it "in reverse" recursively. When the graph has a shortest path from node 
*a* to node *b*, what kind can this path be?

One possibility is, that the path is only an edge from node *a* to node *b*. Thus the distance has been marked to the matrix in the beginning. In other cases the the path have one or more nodes to go through. Let's assume *x* is a node to go through, whose mark is the largest. We now have two subtasks: We first have to go from node *a* to node *x* and then from node *x* to node *b* so, that on both sides the mark of the node to go through is smaller than *x*. We can handle this recursively.

Floyd-Warshall algorithm forms paths in every step, where can be nodes *1,2,...,i*. When we want to find the shortest path between *a* and *b*, we have two options: If the node *i* can be gone through, we combine the shortest path from *a to i* and the shortest path from *i to b*. If *i* cannot be gone through, we have handled that path already earlier. At the end of the algorithm, nodes *1,2,...,n* can be gone through, so any node of the graph can be a intermediate node.

# Comparing the algorithms

We have now gone through multiple algorithms for finding shortest paths and we can form a general picture of the subject. Here's a recap of our algorithms, their efficiency and properties:

| Algorithm            | Time complexity | Properties         |
|:---------------------|:----------------|:-------------------|
| Breadth-first search | O(n+m)          | No weighted graphs |
| Bellman-Ford         | O(nm)           |                    |
| Dijkstra's           | O(n + m log n)  | No negative edges  |
| Floyd-Warshall       | O(n^3)          | Finds all paths    |

In practice, BFS and Dijkstra's algorithms are most commonly used algorithms: if the edges do not have weights, use BFS, otherwise Dijkstra's algorithm. The limitation for Dijkstra's algorithm is that the graph cannot have negative edges, but this limitation usually does not matter in practical probles, as usually the weights of the edges cannot be negative. For example, obviously the length of a road cannot be negative, nor can the timetable of a bus. If a graph must have negative arches, then we can use the Bellman-Ford.

How does Floyd-Warshall compare to other algorithms, then? This depends if the graph is *dense* or *sparse*. In a spare graph there are few edges and *m ~n*, where as in a dense graph there are many edges and *m ~ n^2*. Floyd-Warshall is at its best with a dense graph, as its time complexity is not dependant on the amount of edges. For example, if we search all the shortest paths by running Dijkstra's algorithm *n* times, in a sparse graph it will take *O(n^2 log n)*, but in a dense graph it will be already *O(n^3 log n)*. In other words, with a sparse graph it is faster than Floyd-Warshall, but in a dense graph it is worse. On the other hand, the constants of Floyd-Warshall are very small due to its simple structure, and thus work surprisingly fast in practice.

[**Exercises here**](https://centria.github.io/algo-and-data/exercises/#part-6---shortest-paths)