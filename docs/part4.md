---
title: "Part 4 - List and trees"
permalink: /part4/
nav_order: 6
published: true
---

# Data structures

Data structures are a way of storing information. In this part, we will be looking into couple of examples of data structures. First, we shall examine the *list*, which we have already used in our code. Another data structure of interest, is a *tree*.

# List

*List* is a data structure which resembles an array. It cointains a number of elements, which are one after another in certain order. For example \[3,7,2,5\] is a list of four elements. We want to implement the list in such a manner, that we can access an element in the list based on its index, and we want to be able to add and remove elements.

In this part, we will be looking at two different lists, an *array list* and a *linked list*. The first is based on an array, where the information is stored. Latter is based on nodes, which are connected to one another.

## Array list

*Array list* is a list, where the information is stored in an array. The [**List**](https://docs.microsoft.com/en-us/dotnet/api/system.collections.generic.list-1.capacity?view=netcore-3.1#System_Collections_Generic_List_1_Capacity) of C# is a derivative of *ArrayList*. Since all the elements in an array list are stored after one another in the memory, we can access any information from the list in *O(1)*. The challenge is that the array is *of fixed capacity*, and if we want to change the capacity, we have to reserve a new array, and copy the content into that.

## Changes in the end

Let's first look into an array list, where both the additions and removals are done at the end. We will store the list as an array, so that a certain amount of elements from the beginning of the array are in use, and the rest are reserved for additional elements. For this, we can add a new element in *O(1)* time, if there is space, as all we have to do is use the next free place from the array capacity.

![ArrayList Add 1](https://github.com/centria/algo-and-data/raw/master/assets/images/arraylist1.png)  
source: [**Tietorakenteet ja algoritmit**](https://github.com/pllk/tirakirja/raw/master/tirakirja.pdf)

Above, we have the list \[3,7,2,5\] stored in an array, and we add 6 to the end. We will use one of the free capacity places from the array. This is an *O(1)* operation.

![ArrayList Add 2](https://github.com/centria/algo-and-data/raw/master/assets/images/arraylist2.png)  
source: [**Tietorakenteet ja algoritmit**](https://github.com/pllk/tirakirja/raw/master/tirakirja.pdf)

Above, we have the list \[3,7,2,5,6,1,2,8\] and want to add one more. We cannot fit anymore, so we have to increase the capacity by creating a new, larger array, and copy the information from the original there. This takes *O(n)*, because we have to go through the process of copying the whole array, before we can add the new element.

We have created a list, where adding an element takes either *O(1)* or *O(n)*, depending on whether the element fits into the current capacity, or do we have to reserve a new array. For the list to be useful, the slow *O(n)* operation should not be frequent. Turns out, we can achieve this, as long as we reserve the new array always greatly larger than previously. A very common solution is to *double up the capacity* every time we need to reserve a new array. Doing this, adding an element takes *on average* only *O(1)* time.

Why is it *O(1)* on average? Let's see a situation, where the list has *n* elements and the array has become full, so the elements have to be copied to a new array. We know, that the previous time elements were copied, was done when there was *n/2* elements, so there has been an *efficient addition of n/2 elements* since then. Thus copying *n* elements time complexity can be divided to the previous *n/2* elements, and the additional complexity for adding an element is constant. The increase of the array capacity to the total is thus relatively small.

We can remove an element from the end always in *O(1)* time, as this does not require increase in capacity. This can lead to a situation, where after several removals there is too much capacity in the array, taking memory space. We can use the same idea as with addition: if after removal there's only one *quarter* of the array in use, *halve* the array capacity. This way we can keep our removal also *on average* at *O(1)*.

![ArrayList Remove](https://github.com/centria/algo-and-data/raw/master/assets/images/arraylist3.png)  
source: [**Tietorakenteet ja algoritmit**](https://github.com/pllk/tirakirja/raw/master/tirakirja.pdf)

Why not reserve the whole capacity in the beginning? This would end up reserving quite a lot of memory. An algorithm could be handling multiple lists at a time, and we want to have the lists in the same scale as the amount of content in the list.

## Changes in the beginning and the end

Quite similarly we could create an array list, which allows efficient element removal both from the beginning and the end of the list. To achieve this, we will have to change the recording method of the list so, that it can start and end anywhere in the array, and the content of the list can continue from the end of the array to the beginning, if needed.

![ArrayList Another](https://github.com/centria/algo-and-data/raw/master/assets/images/arraylist4.png)  
source: [**Tietorakenteet ja algoritmit**](https://github.com/pllk/tirakirja/raw/master/tirakirja.pdf)

The image shows an example of the new way of saving our list. The arrow to the right shows the beginning of the list, and the arrow to the left points at the end of the list. When we want to add an element to the beginning, we move left from the left-pointing arrow, and when we want to add to the the end, we move right from the right-pointing arrow. We do the reverse, when we want to remove an element from the list.

If the arrows would be next to each other in this arrangement, it can mean two things: The list is either empty, or all of the capacity is in use:

![ArrayList Another Full](https://github.com/centria/algo-and-data/raw/master/assets/images/arraylist5.png)  
source: [**Tietorakenteet ja algoritmit**](https://github.com/pllk/tirakirja/raw/master/tirakirja.pdf)

As we keep track of the amount of elements in our list, we can determine, which of the situations is at hand. If the array is full and we want to add another element, we once again need to reserve a larger array and transfer the content of the array. We can do this similarly as in the previous version and for example double the capacity, giving us *on average* an operation time of *O(1)*.

## Linked list

*Linked list* comprises of *nodes*, which each contain one element of the list. A linked list can be linked to one direction or both directions, i.e. *singly linked list* or a *doubly linked list*. In a singly linked list, each node has a reference to the next one, and in doubly linked list, a node has a reference to both the next and the previous one.

![Linked list 1](https://github.com/centria/algo-and-data/raw/master/assets/images/linkedlist1.png)  
source: [**Tietorakenteet ja algoritmit**](https://github.com/pllk/tirakirja/raw/master/tirakirja.pdf)

The image aboce shows the example list \[3,7,2,5\] as singly and doubly linked. In both cases we have the reference information for the beginning and the end. In a singly linked list we can iterate the list from the beginning to the end, whereas in a doubly linked list, we can go both ways.

The doubly linked list is a more reasonable way of doing a linked list, and from now on when we discuss linked lists, we always use *doubly linked list*. This is also how the class [**LinkedList**](https://docs.microsoft.com/en-us/dotnet/api/system.collections.generic.linkedlist-1?view=netcore-3.1) is done in C#.

## Linked structures

In every coding language there are ways of creating a linked list, and often they are built-in. Let's anyways have a look, how we could implement a linked list.

```cs
public class Node
{
  public int value;
  public Node next;
  public Node previous;

  public Node(int value, Node next, Node previous)
  {
    this.value = value;
    this.next = next;
    this.previous = previous;
  }
}
```

The property *value* stores the value of the node, *next* refers to the next node, and the *previous* refers to the previous node. If there is no previous or next node, the reference is set to *null*. For example the next code creates a Node, with a value of *5* and it references nowhere:

```cs
Node n = new Node(5, null, null);
```

The following code illustrates how we can use this to create a linked list:

```cs
Node n1 = new Node(3, null, null);
Node n2 = new Node(7, null, n1);
Node n3 = new Node(2, null, n2);
Node n4 = new Node(5, null, n3);

n1.next = n2;
n2.next = n3;
n3.next = n4;
```

We end up doing it a bit clumsily. If we would initialize the Nodes as for example *null* before we assign any values in them, the references to *next* would all point to *null*. If we did point to the next and the previous before initializing the nodes, we would get an error, as we would be pointing to something that does not exist yet. 

After this we could go through our linked list from the beginning to the end:

```cs
Node n = n1;
while (n != null)
{
  Console.WriteLine(n.value);
  n = n.next;
}
```

A more reasonable way could be implementing our own methods for adding nodes to the linked list, and removing them. This way we can avoid the troublesome errors caused by null references. This will be left as an exercise.

## List operations

The advantage of a linked list is that we can add and remove elements in *O(1)* time from any point of the list. When we want to add an element to the list, we first create a new node and change the references of the neighbouring nodes so, that they reference to the new node. Similarly, if we want to remove a node, we change the references, so that the node is skipped.

![Linked list 2](https://github.com/centria/algo-and-data/raw/master/assets/images/linkedlist2.png)  
source: [**Tietorakenteet ja algoritmit**](https://github.com/pllk/tirakirja/raw/master/tirakirja.pdf)

The image illustrates an example of the usage of a linked list. We start with a list of  \[3,7,2,5\]. Then we add the element 4 to the middle, for which we first create a node and then change the references from the elements 7 and 2 so, that 4 comes between them. After this we remove the element 2, so we combine the elements 4 and 5 to each other.

We can access the first and the last nodes of efficiently, as we have a reference to them in the memory. However, if we want to access any other part of the list, we have to start from either end and move *jump by jump*, following the references in the nodes. Thus to access the element in the middle of the list takes *O(n)*. We have to access the nodes through their refence links, as the nodes can be scattered anywhere in the memory and we have no straight access, where which node is stored.

# Tree

In computer science, a *tree* is a widely used data structure. Like the linked list, it is based on *nodes* which are linked to one another in a specific way. There are several tree structures, but we are going to look at *binary tree* and its derivative, *binary search tree*.

Unlike the natural trees you can find from the nature, these trees have their roots at the top, and leafs at the bottom.

## Binary tree

A binary tree is made out of *n* nodes. At the top of the tree is a node, which is called a *root*. Since we are looking at a binary tree (*bi* = duality, a pair), each node can have two *children*, left and right, and all the nodes (excluding the root) can have exactly one parent. The *leafs* of the tree are the nodes without any children.

The structure of a binary tree is recursive: Each node works as a root for a *subtree*, which is also a binary tree. The subtree of a node *x* contains the node *x* itself, and all the nodes we can access by going downwards from said node. We can also think that every child of a node is (a possibly empty) binary tree.

![Binary tree 1](https://github.com/centria/algo-and-data/raw/master/assets/images/binarytree1.png)  
source: [**Tietorakenteet ja algoritmit**](https://github.com/pllk/tirakirja/raw/master/tirakirja.pdf)

In the picture above we have a binary tree with 8 nodes. Node 1 is the root, and ndoes 4, 5, 6 and 8 are its leafs. Node 3's left child is 5, right child is 6, and parent is 1. The subtree of node 3 contains nodes 3, 5, 6, 7 and 8.

The *depth* of the root of the binary tree is *0* and the depth of all the other nodes is one greater than that of their parent. The *height* of a binary tree is the greatest depth in the tree, or the greatest amount of steps from the root to the lowest leaf. In our picture above, the height is 3, as the depth of nodes 7 and 8 is 3.

![Binary tree 2](https://github.com/centria/algo-and-data/raw/master/assets/images/binarytree2.png)  
source: [**Tietorakenteet ja algoritmit**](https://github.com/pllk/tirakirja/raw/master/tirakirja.pdf)

If the height of the binary tree is *h*, it has at least *h+1* nodes, when it is just a list of nodes, and at most *2^(h+1) -1* nodes, when all the levels have all the possible nodes. The picture above shows these examples, when the height is *2*.

## Binary tree operations

We can implement the binary tree as a linked structure, so that each node is an object, which has a reference to the left and the right child, and possible other fields, like the value of the node. If the node does not have a left or right child, that reference is *null*.

Recursion is a natural way to create many of the operations regarding a binary tree. For example, the next method calculates, how many nodes does the tree given as a parameter have:

```console
countNodes(node)
  if node == null
    return 0
  return 1 + countNodes(node.left) +
           + countNodes(node.right)
```

The parameter for the method is the node, which acts as the root of the tree. If the tree is empty, there are no nodes. Otherwise there is the root node and the nodes from left and right subtrees. We can count the nodes from the subtrees by calling the method again recursively.

The following function is used to find out the height of the tree. Notice, that if the tree is empty, we say it's height is *-1*, as having only a root would be 0.

```console
height(node)
  if node == null
    return -1
  return 1 + max(height(node.left), height(node.right))
```

## Tree traversals

We can go through the nodes of a binary tree from the root recursively. There are three common ways of traversing the nodes:

* *Pre-order*: First handle the root, then the left subtree, then the right subtree

* *In-order*: First handle the left subtree, then the root, then the right subtree

* *Post-order*: First handle the left subtree, then the right subtree, then the root


![Binary tree 1](https://github.com/centria/algo-and-data/raw/master/assets/images/binarytree1.png)  
source: [**Tietorakenteet ja algoritmit**](https://github.com/pllk/tirakirja/raw/master/tirakirja.pdf)

In the example we used already above, we have a *pre-order* of \[1,2,4,3,5,6,7,8\], *in-order* of \[4,2,1,5,3,7,6,8\] and *post-order* of \[4,2,5,7,8,6,3,1\]. We can traverse all the nodes of a binary tree in these orders using recursion. For example, the following method prints the nodes of the tree with in-order, when given the root as a parameter:

```console
printNode(node)
  if node == null
    return
  printNode(node.left)
  print(node.value)
  printNode(node.right)
```


## Binary search tree

![Binary search tree 1](https://github.com/centria/algo-and-data/raw/master/assets/images/bst1.png)  
source: [**Tietorakenteet ja algoritmit**](https://github.com/pllk/tirakirja/raw/master/tirakirja.pdf)

*Binary search tree* is a binary tree, where each node represents an objects in a set. The nodes are ordered in such a manner, that for each node, all the nodes in the subtree are smaller than the node itself, and similarly on the right side, all the nodes in the subtree are of greater value. Because of this, we can easily find a ndoe from the tree by beginning our search from the root.

In the example above, we have a binary search tree representing the set {2,3,5,7,8,9}, where the root is 5. On the left subtree are the objects smaller than 5, or the set {2,3}. On the right subtree are the objects with greater values than 5, i.e. the set {7,8,9}. Notice, that this is one of the many ways to create a binary search tree for said set, and we could choose any of the nodes to be the root.

## Binary search tree operations

Next we shall look into the operations for handling nodes in a binary search tree. We will notice, that we implement all the operations in time *O(h)*, where *h* is the height of the tree.

## Looking for nodes

When we want to search the object *x* from our set, we start from the root of the tree and go downwards. When where are at the node *a*, there are three options. If *a = x*, we have found the object we were looking for. If *a > x*, we continue our search to the left child, an similarly if *a < x*, we continue to the right child. If the node does not have a child where we should move to, we can conlcude the 

![Binary search tree 2](https://github.com/centria/algo-and-data/raw/master/assets/images/bst2.png)  
source: [**Tietorakenteet ja algoritmit**](https://github.com/pllk/tirakirja/raw/master/tirakirja.pdf)

set does not contain the object *x*.

The picture above shows, how we can find the object *7* from the set {2,3,5,7,8,9}. The root is at *5*, so the 7 has to be on the right subtree. This subtree has its root at 8, so now we know that 7 has to be to the left of 8, where it indeed can be found.

## Adding a node

When we want to add an object *x* to the set, we first want to search for x to see it does not exist already. When we then get to a node which does not have a child in the corresponding location where we should be moving to, we create a new node for *x* and add it to the location as a child.

![Binary search tree 3](https://github.com/centria/algo-and-data/raw/master/assets/images/bst3.png)  
source: [**Tietorakenteet ja algoritmit**](https://github.com/pllk/tirakirja/raw/master/tirakirja.pdf)

In the picture above we are adding *4* to the set of {2,3,5,7,8,9}. We first search for 4 in the tree and end up in node with object value of 3, and has no right child. Thus we create a new node for 4, and set is as the right child of 3.

## Smallest / largest object

When we want to find the smallest object, we start from the root and move to the left child on each step. When the node does not have a left child, we have found the smallest object. Similarly, if we want to find the greatest object, we start from the root, and always move to the right.

## Next larger / Previous smaller

When we want to find the smallest object which is larger than *x*, we start from the tree. When we are at a node *a*, we go to the left child, if *a > x* and to the right child, if *a <= x*. We continue this, until we cannot go further. The last object is the smallest object greater than *x* of all the objects we traversed through. When we want to find the largest object, which is smaller than *x*, we do the opposite in our operations.

## Removing a node

If we want to remove the object *x* from our set, we first have to find the node of *x* as usual. If the node does not have children or only has one child, it is easy just to remove the node and keep the structure of the tree otherwise intact. If, however, the node has two children, it gets more complicated. This time we need to find object *y*, which is the smallest node of those larger than *x*, and swap *x* and *y* in the tree. After this we can easily remove the node where object *x* now resides, as it cannot have two children (if the node would have a left child, *y* would not be the smallest node greater than *x*).

![Binary search tree 4](https://github.com/centria/algo-and-data/raw/master/assets/images/bst4.png)  
source: [**Tietorakenteet ja algoritmit**](https://github.com/pllk/tirakirja/raw/master/tirakirja.pdf)

In the picture above we remove 5 from the set {2,3,5,7,8,9}. The node is at the root of the tree and has two children, so we have to look for the smallest object greater than 5, which is 7. Then we swap together the values 5 and 7, after which we can remove the 5 with ease.

## Efficiency of operations

The operations for binary search tree take *O(h)* time, where *h* is the height of the tree, so the efficiency of the operations is dependant on the height of the tree. In other words, the effectiveness of the operations depends on how well we build our tree. 

![Binary search tree 5](https://github.com/centria/algo-and-data/raw/master/assets/images/bst5.png)  
source: [**Tietorakenteet ja algoritmit**](https://github.com/pllk/tirakirja/raw/master/tirakirja.pdf)

In the example above, you can see two binary trees for set {1,2,3,4,5}. The height of the left tree is 2, whereas the height of the right tree is 4.

For a binary tree to work efficiently, we don't want the height to become too large. More specificly, our target is to have the nodes split evenly between both sides of the tree and the height would be *O(log n)*. This situation is called a *balanced* tree. If we manage to do this, all the operations can be done in *O(log n)*. 

There are multiple ways to balance a binary search tree. They are, how ever, well beyond the scope of this small course. It is crucial to know, however, that the selection of the root is, even though free, not recommended to be done at random, but with careful thought.


[**Exercises here**](https://centria.github.io/algo-and-data/exercises/#part-4---list-and-trees)