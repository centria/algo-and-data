---
title: "Exercises"
permalink: /exercises/
nav_order: 99
published: true
---

# Exercises

* Each student is to create a git repository and send a link to that repository to the teacher before the first deadline, via email, or in Slack private message. **DO NOT SHARE YOUR REPOSITORIES WITH EACH OTHER**, even though they can be left public.

* Submission of the exercises is done by having the solutions as a code (or pseudocode) in the repository. *All the exercises are supposed to be done in C#, but you can get some points for pseudocode solution.*

* The exercises need to be **clearly marked**. Create a separate class (and file) for all the exercises in one part, so you can try them out in a single Main.
  * [**Example for structure can be found here**](https://github.com/HeikkiHei/algo-examples), and you can use it as a template if you want.

* Each part has separate deadline, before the next part's lesson, *unless stated otherwise*. 

  * Public holidays or other force majeure sitations can move deadlines, and these will be informed in here.

* Submissions are done *by pushing to your personal repository*. The first submission requires submitting the link to the teacher.

* Answers will be gone through at the beginning of the next lesson, after deadline. 
  * After the last deadline, as there is no lesson, **all** the answers will be published here.

* If some parts are combined together, the *first* deadline will be the one to follow, and the rest of the deadlines are moved earlier, accordingly. The changes will be updated here in advance.

## Grading

* Each C# exercise is worth 2 or 4 points (2, unless stated otherwise). To get all the points, **you must solve the problem in C#**.
* To get half of the points, you can show your work and idea in *pseudocode* instead of C#. This way, even though your code does not work, but you know how the algorithm should work, you can still get points.
* In larger exercises (worth 4 points), you can get 1 to 3 points, even if you miss some part of C# code, but can show that you understand the problem and can produce the pseudocode, even if the code itself would be too difficult.
* The main idea is not to learn how to code, you should have learnt that already. Now it's time to activate your brain and design algorithms.

## Part 1 - Introduction

* Deadline **12.5.2020 at 23:59**
* All the exercises are meant to be written in C#
  * You can get points for pseudocode, if you properly show your work.

### Exercise 1

* Create a class **Numbers**, which calculates the sum of the numbers in an integer. For example, with 4075, the sum is 4 + 0 + 7 + 5 = 16. Use the following method:
  * **int Sum(int x)**, returns the sum of the numbers in *x*.

For example:

```cs
Numbers num = new Numbers();
Console.WriteLine(num.Sum(4075)); // 16
Console.WriteLine(num.Sum(3)); // 3
Console.WriteLine(num.Sum(999999999)); // 81
```

### Exercise 2

A *substring* is a string, that is part of another string. For example, in string *aybabtu* some substrings are *bab* and *abtu*.

* With C#, create a class **Substrings**, which has the following method:
  * **int Calculate(string a, string b)**, which calculates how many times a substring *b* can be found from the string *a*. For example:

```cs
int Calculate(string a, string b)
```

* All the characters are from a to z (non-capital)

The code should work as follows:

```cs
Substrings subs = new Substrings();
Console.WriteLine(subs.Calculate("aybabtu", "bab")); // 1
Console.WriteLine(subs.Calculate("aaaaa", "aa")); // 4
Console.WriteLine(subs.Calculate("monkey", "banana")); // 0
```

### Exercise 3

As a parameter, give the program an array with integers. With each step, form a new array, where each element is the sum of two elements that were next to each other in the previous array. Eventually, you will have an array with only one element. For example, with \[1,2,3,2\] should first turn into \[3,5,5\], this into \[8,10\] and finally into \[18\].

* Create a class called **Tables**, which has the following method:
  * **int Calculate(int[] t)**, which returns the value of the last element (an integer, not the whole array).

The class should work as follows.

```cs
Tables t = new Tables();
Console.WriteLine(t.Calculate(new int[] {1,2,3,2})); // 18
Console.WriteLine(t.Calculate(new int[] {5})); // 5
Console.WriteLine(t.Calculate(new int[] {4,2,9,1,9,2,5})); // 323
```

HINT! You might want to try recursion. You can do this without it as well, but this is a good chance to try it out!

### Exercise 4

*This exercise is worth 4 points.*

An integer is a lucky number, if every number in it is either 3 or 7. For example, 3, 7, 33, 37, 73, 77, and 733737 are lucky numbers. Your assigment is to calculate lucky numbers between a...b.

* Create a class **LuckyNumbers**, with the following method:
  * **int Calculate(int a, int b)**, which returns the amount of lucky numbers between two integers.

The following code represents the usage of the class:

```cs
LuckyNumbers luck = new LuckyNumbers();
Console.WriteLine(luck.Calculate(1,10)); // 2
Console.WriteLine(luck.Calculate(123,321)); // 0
Console.WriteLine(luck.Calculate(1,1000000)); // 126
```

HINT! Calculate from *1 to a* and *1 to b* separately, and substract them.

HINT! Do not go through all the numbers, it is very inefficient. Try to find a mathematical pattern!

## Part 2 - Time Complexity

* Deadline 19.5. at 23:59

### Exercise 1


"The example as follows: The input is a string with length of *n* and each character (or element) is either 0 or 1. We want to calculate, how many different ways we can choose two parts of the input so, that the left character is 0 and the right character is 1. For example, in an input of 01001 we can find four ways for this selection:
**01**001, **0**100**1**, 01**0**0**1** and 010**01**."

Time efficiency O(n^2)

```console
counter = 0
for i = 0 to n-1
  for j = 0 to n-1
    if chars[i] == 0 and chars[j] == 1
      counter += 1
print(counter)
```

Time efficiency O(n)

```console
counter = 0
zeros = 0
for i = 0 to n-1
  if chars[i] == 0
    zeros += 1
  else
    counter += zeros
print(counter)
```

* Above you see two algorithms to a same problem, as introduced in the material. Create these solutions in C#.

* Measure the time taken for both algorithms. 

You can do it by adding 

```cs
DateTime start = DateTime.Now;
```

In the beginning of the algorithm and

```cs
DateTime end = DateTime.Now;
Console.WriteLine("Time this took: " + end.Subtract(start));
```

In the end.

* To test both of the solutions, create inputs with 10, 100, 1000 and 10000 (and 1000000, if you want) characthers in input. You can create the input characters with for example the following code:

```cs
// using System.Text

public string CreateInput(int n)
{
  StringBuilder sb = new StringBuilder();
  Random random = new Random();
  for (int i = 0; i < n; i++)
  {
    sb.Append(random.Next(0, 2).ToString());
  }
  return sb.ToString();
}
```

This code is of time efficiency O(n). If you have a more efficient way to do it, feel free to use it, and do share that code!

* DO NOT include the input creation time in the efficiency calculation!

* Save the results of your outputs to a file, clearly marking the size of the input, which algorithm you used, and how long it took. You can use this kind of a table, for example, in an MD file:

```md
| Input size | O(n^2)  | O(n)    |
|:----------:|:-------:|:-------:|
| 10         | 0.000 s | 0.000 s |
| 100        | 0.000 s | 0.000 s |
| 1000       | 0.000 s | 0.000 s |
| 10000      | 0.000 s | 0.000 s |
```

* Add the results in such a detail, that all the results show at least something, i.e. just 1000th of a second might not be enough detail.

* You might want to save the file in the part2 folder of your repository, or use the README.md file at the root.

### Exercise 2

* You are given an array with *n* integers. Your task is to calculate, how long is the longest section of recurring numbers in the array.

* Create a class **LongestRepetition**, with the following method:
  * **int Calculate(int[] t)**, which returns the length of the longest repetition

The following code represents the behavior:

```cs
LongestRepetition p = new LongestRepetition();
Console.WriteLine(p.Calculate(new int[] {1,2,1,1,2})); // 2
Console.WriteLine(p.Calculate(new int[] {1,2,3,4,5})); // 1
Console.WriteLine(p.Calculate(new int[] {1,1,1,1,1})); // 5
```

* You should be able to do this in *O(n)* to get all the points.
  * You can get some points for *O(n^2)*

### Exercise 3

* You are given an array with *n* integers. You want to change the array, so that no number is repeated after one another. On each step, you can change any number from the array to be something else. What is the smallest amount of steps?

* For example, in array \[1,1,2,2,2\] the smallest amount of moves is 2. One solution would be to change the array to be \[1,3,2,1,2\].
  
* Create a class **Changes** with the following method:
  * **int Calculate(int[] t)**, which returns the smallest amount of changes.

The following code represents the behavior:

```cs
Changes m = new Changes();
Console.WriteLine(m.Calculate(new int[] {1,1,2,2,2})); // 2
Console.WriteLine(m.Calculate(new int[] {1,2,3,4,5})); // 0
Console.WriteLine(m.Calculate(new int[] {1,1,1,1,1})); // 2
```

* You should be able to do this in *O(n)* to get all the points.
  * You can get some points for *O(n^2)*

### Exercise 4

* You are given an array with all the integers *1...n* exactly once. You want to collect the integers from smallest to largest, taking one or more *revolutions* in the array. With each revolution, you will traverse the array from left to right and pick as many as possible integers in order. How many revolutions do you do in total?

* For example, in array \[4,1,3,2,5\] the amount of revolutions is three, because on the first revolution you pick up 1 and 2, next revolution 3 and on the third one you pick up 4 and 5.

* Create a class **Revolutions** with the following method:
  * **int Calculate(int[] t)**, which returns the amount of revolutions.

The following code represents the behavior:

```cs
Revolutions r = new Revolutions();
Console.WriteLine(m.Calculate(new int[] {4,1,3,2,5})); // 3
Console.WriteLine(m.Calculate(new int[] {1,2,3,4,5})); // 1
Console.WriteLine(m.Calculate(new int[] {5,4,3,2,1})); // 5
```

* You should be able to do this in *O(n^2)* to get all the points.
  * No points awarded for worse solutions.

### Exercise 5

* You are given an array with *n* integers. In how many ways can you split the array into left and right subarrays in such a way, that the sum of each part are equal?

* For example in array \[1,2,-1,4,0\] all the possible ways to split it are:
  * \[1\] and \[2,-1,4,0\]
  * \[1,2\] and \[-1,4,0\]
  * \[1,2,-1\] and \[4,0\]
  * \[1,2,-1,4\] and \[0\]

* In this array the correct answer is 1, as the sums of left and right side are equal only with \[1,2\] and \[-1,4,0\]. Now the sum of both sides is 3.

* Create a class **Split** with the following method:
  * **int Calculate(int[] t)**, which returns the amount of possible ways.

The following code represents the behavior:

```cs
Split s = new Split();
Console.WriteLine(s.Calculate(new int[] {1,2,-1,4,0})); // 1
Console.WriteLine(s.Calculate(new int[] {1,2,3,4,5})); // 0
Console.WriteLine(s.Calculate(new int[] {0,0,0,0,0})); // 4
```

* You should be able to do this in *O(n)* to get all the points.
  * You can get some points for *O(n^2)*

## Part 3 - Recursion

* Deadline 26.5. at 23:59

* Not all of the exercises require recursion. 

* You can use the built-in sort of C#, unless stated otherwise.

* You can create random content int arrays with length *n* with the following code:

```cs
public static int[] Randomizer(int n)
{
  Random random = new Random();
  int[] arr = new int[n];
  for (int i = 0; i < arr.Length; i++)
  {
    // integers between 1 and 1000 are enough for us
    arr[i] = random.Next(1, 1001);
  }
  return arr;
}
```


### Exercise 1

* Create a method **void Hello(int n)** which prints the string *"Hello!"* **recursively**, *n* amount of times.

* You can find the example from part 1.

The following code represents the behavior:

```cs
Hello(5);
```

```console
Hello!
Hello!
Hello!
Hello!
Hello!
```

### Exercise 2

* You are given an array with *n* integers. Your task is to solve, what is the smallest difference between two elements in the array.

* Create a class **SmallestDifference** with the following method:
  * **int Calculate(int[] t)**, which returns the smallest difference between two elements.


The following code represents the behavior:

```cs
SmallestDifference s = new SmallestDifference();
Console.WriteLine(s.Calculate(new int[] {4,1,8,5})); // 1
Console.WriteLine(s.Calculate(new int[] {1,10,100})); // 9
Console.WriteLine(s.Calculate(new int[] {1,1,1,1,1})); // 0
Console.WriteLine(s.Calculate(Randomizer(10))); // depends on random
```

### Exercise 3

* You are given an array with *n* integers. Your task is to create a [**merge sort**](https://centria.github.io/algo-and-data/part3/#merge-sort) and [**quick sort**](https://centria.github.io/algo-and-data/part3/#quick-sort) for sorting the array.

* I suggest you use the base from the material, linked in the bullet point above. **DO NOT USE built-in sorts!**

* Create a class **Sorting** with the following methods:
  * **void MergeSort(int[] t)**, which sorts the list and prints how long it took.
  * **void QuickSort(int[] t)**, which sorts the list and prints how long it took.

* Measure the time taken for both algorithms. 

You can do it by adding 

```cs
DateTime start = DateTime.Now;
```

In the beginning of the algorithm and

```cs
DateTime end = DateTime.Now;
Console.WriteLine("Time this took: " + end.Subtract(start));
```

* DO NOT include the input creation time in the efficiency calculation!

* Save the results of your outputs to a file, clearly marking the size of the input, which algorithm you used, and how long it took. You can use this kind of a table, for example, in an MD file:

```md
| Input size | Quick   | Merge   |
|:----------:|:-------:|:-------:|
| 10         | 0.000 s | 0.000 s |
| 100        | 0.000 s | 0.000 s |
| 1000       | 0.000 s | 0.000 s |
| 10000      | 0.000 s | 0.000 s |
```

The following code represents the behavior:

```cs
Sorting s = new Sorting();
int[] sortMe = Randomizer(100);
int[] sortMeLarge = Randomizer(1000000);
s.QuickSort(sortMe);
s.MergeSort(sortMe);
s.QuickSort(sortMeLarge);
s.MergeSort(sortMeLarge);
```

### Exercise 4

* You are given an array with *n* integers. Your task is to create a *binary search*, which finds if the array contains an integer *x*.

* You can review the algorithm structure [**from here**](https://centria.github.io/algo-and-data/part3/#binary-search).

* Create a class **BinarySearch** with the following method:
  * **bool Find(int[] t, int x)**, which returns if the array contains x or not.


The following code represents the behavior:

```cs
BinarySearch b = new BinarySearch();
Console.WriteLine(b.Find(new int[] {4,1,8,5}, 2)); // false
Console.WriteLine(b.Find(new int[] {0,0}, 0)); // true
Console.WriteLine(b.Find(new int[] {4,1,8,5,8,7,4,2,3}, 2)); // true
Console.WriteLine(b.Find(new int[] {0}, 0)); // true
Console.WriteLine(b.Find(Randomizer(100000), 3)); // depends on Random
```

### Exercise 5

* Your task is to *create* an array with *n* integers, which contains the numbers *1...n* and it has **exactly** *k* inversions. You can create any array, which fulfills these criteria.

* Create a class **Inversions**, with the following method:
  * **int[] Create(int n, int k)**, which returns the array.


The following code represents the behavior:

```cs
Inversions inv = new Inversions();
int[] t = inv.Create(5, 2);
foreach (int i in t)
{
  Console.Write(i + " ");  // 2 1 3 5 4
}
```

NOTICE! You can decide the locations of the inversions, just make sure the conditions apply!



## Part 4 - List and Trees


* Deadline 2.6. at 23:59

### Exercise 1

Your task is to create a *doubly linked list* with its most common functions.

* Implement class **Node** from the material.
* Implement class **LinkedList**, with the following methods:
  * **void AddFirst(int n)** Adds a **Node** to the beginning of the linked list, with **value** *n*.
  * **void AddLast(int n)** Adds a **Node** to the end of the linked list, with **value** *n*.
  * **void RemoveFirst()** Removes the first node from the linked list.
  * **void RemoveLast()** Removes the last node from the linked list.
  * **int GetNode(int x)** Get the value of the node in position *x*.
  * **override string ToString()** returns the all the values of the list, from the beginning to the end.

```cs
LinkedList myLinks = new LinkedList();
myLinks.AddLast(1);
myLinks.AddFirst(2);
myLinks.AddLast(3);
Console.WriteLine(myLinks); // for example: 2, 1, 3
myLinks.RemoveFirst();
Console.WriteLine(myLinks); // for example: 1, 3
Console.WriteLine(myLinks.GetNode(0)); // 1
Console.WriteLine(myLinks.GetNode(1)); // 3
```

* Your code should be efficient, i.e. all the methods should be at maximum of *O(n)* time comlexity.

### Exercise 2

* In a circle there are *n* children, all numbered *1, 2, 3,...,n*. Every turn every other child leaves the circle, until there is only one child left. What is the number of this child?

For example, with *n = 7*, the children leave the circle in order 2, 4, 6, 1, 5, 3 and 7, so the last child to remain is number 7.

* Create a class **CircleGame** with the following method:
  * **int Last(int n)** returns the number of the last child from an *n* sized circle.

For example:

```cs
CircleGame g = new CircleGame();
Console.WriteLine(g.Last(7)); // 7
Console.WriteLine(g.Last(4)); // 1
Console.WriteLine(g.Last(123)); // 119
```

* This should work with circles up to a million children (I know, that's a lot of people), so be efficient.


### Exercise 3

Your task is to create a class, which keeps a collection of numbers. The collection can be added numbers into and it can be asked, what is the smallest distance between two numbers.

* Create a class **SmallestDistance** with the following methods:
  * **void Add(int x)**
  * **int Calculate()**: returns the smallest distance between two integers.

The following represents the functionality:

```cs
SmallestDistance s = new SmallestDistance();
s.Add(3);
s.Add(8);
Console.WriteLine(s.Calculate()); // 5
s.Add(20);
Console.WriteLine(s.Calculate()); // 5
s.Add(9);
Console.WriteLine(s.Calculate()); // 1
```


### Exercise 4

A binary tree has *n* nodes, numbered *1...n*. You are given the *pre-order a* and *in-order b*, and your task is to produce the *post-order* of said tree.

NOTICE! It is not necessarily a binary search tree, so the nodes can be in any order in the tree.

* Create the class **Order** with the following method:
  * **Create(int[] a, int[] b)**, which returns the post-order of the nodes.

An example:

```cs
Order o = new Order();
int[] a = {4,2,1,3,5};
int[] b = {2,4,3,1,5};
int[] c = o.Create(a,b);
Console.WriteLine(String.Join(" ", c)); // 2 3 5 1 4
```

NOTICE! Your *Create* method can either return the array, or print the values. This is just as fine:


```cs
Order o = new Order();
int[] a = {4,2,1,3,5};
int[] b = {2,4,3,1,5};
o.Create(a,b); // 2 3 5 1 4
```

### Exercise 5

You task is to implement a *binary search tree*, where you can add new nodes and calculate the height of the tree.

If the numbers would be added in order, they would all go into a single line, and the tree would have a very large height. What happens, if you add them in *random* order?

* Create a class **BinarySearchTree** and in it the methods:
  * **void Add(int x)**, adds the integer *x* to your tree.
  * **int Height()**, which returns the height of the tree.

* Add some numbers (1 to 50 or similar) to your tree in random order, and print the result of **Height**. Do this at least three times and save the results.

For example:

```cs
BinarySearchTree bs = new BinarySearchTree();
bs.Add(5); // Becomes your root
bs.Add(4); // Goes to the left
bs.Add(6); // Goes to the right
Console.WriteLine(bs.Height()); // 1
bs.Add(3);
bs.Add(1);
bs.Add(7);
Console.WriteLine(bs.Height()); // 3
```

If you want to try out your tree with larger amount of nodes, here's a code you can use:

```cs
static void RandomNodes(BinarySearchTree tree)
{
  // Quite efficient up to 100000
  int hundrerThousand = 100000;
  Random random = new Random();
  List<int> nodeList = new List<int>();
  // Add all the numbers to the nodelist
  for (int i = 1; i < hundrerThousand + 1; i++)
  {
    nodeList.Add(i);
  }
  // Add them to the tree in random order
  while (nodeList.Count > 1)
  {
    // All the numbers left at the list
    int remove = random.Next(1, nodeList.Count);
    // Add from the index "remove"
    tree.Add(nodeList[remove]);
    // remove the number from index "remove"
    nodeList.RemoveAt(remove);
  }
  // Add the last one, remove from the list
  tree.Add(nodeList[0]);
  nodeList.RemoveAt(0);
}
```

You can call it with

```cs
BinarySearchTree bs = new BinarySearchTree();
RandomNodes(bs);
Console.WriteLine(bs.Height());
// Most probably around 40, +/- something
// With 100000 Nodes
```

## Part 5 - Graphs

* Deadline 9.6. at 23:59

### Exercise 1

DFS and BFS are the common ways to traverse through a graph. In some cases we can use either of them, but sometimes only one will work the way we want.

* Which algorithm can be used in the following tasks? In each one we have an undirected graph. Choose from the options for each question.

1. Is the graph connected?
   * Only depth-first search
   * Only breadth-first search
   * Both
2. Is there a path from node *a* to node *b*?
   * Only depth-first search
   * Only breadth-first search
   * Both
3. How long is the shortest path from node *a* to node *b*?
   * Only depth-first search
   * Only breadth-first search
   * Both
4. How many connected components the graph has?
   * Only depth-first search
   * Only breadth-first search
   * Both
5. Is there a cycle in the graph?
   * Only depth-first search
   * Only breadth-first search
   * Both
6. Is the graph a tree?
   * Only depth-first search
   * Only breadth-first search
   * Both
7. What is the node furthest away from node *x*?
   * Only depth-first search
   * Only breadth-first search
   * Both

* Return your answers in a single file in the repository, preferably MD or TXT file.


### Exercise 2

A network comprises of *n* computers, which are labeled *1, 2, ..., n*. In the network there is a set of connections, through which information can be sent both ways. Your task is to find out, how with how many computers can a certain computer communicate.

NOTICE! In this and the following exercises, the computers can communicate with each other, if there is a connection between through other computers!

* Create a class **Connectivity**, with the following methods:
  * **Connectivity(int n)**, the amount of computers is given in the constructor.
  * **void AddConnection(int a, int b)**, adds a connection between *a* and *b*.
  * **int Calculate(int x)**, returns the amount of computers with which *x* can communicate.

Example code:

```cs
Connectivity c = new Connectivity(6);
c.AddConnection(1,2);
c.AddConnection(2,3);
c.AddConnection(1,3);
c.AddConnection(3,4);
c.AddConnection(5,6);
Console.WriteLine(c.Calculate(1)); // 3
```

### Exercise 3

A network comprises of *n* computers, which are labeled *1, 2, ..., n*. In the network there is a set of connections, through which information can be sent both ways. Two computers belong in the same *component*, if they can communicate with each other. Your task is to calculate the amount of components.

* Create the class **Components**, with the following methods:
  * **Components(int n)**, the amount of computers is given to the constructor.
  * **void AddConnection(int a, int b)**, adds a connection between *a* and *b*.
  * **int Calculate()**, returns the amount of components.

Example code:

```cs
Components k = new Components(6);
k.AddConnection(1,2);
k.AddConnection(2,3);
k.AddConnection(1,3);
k.AddConnection(3,4);
k.AddConnection(5,6);
Console.WriteLine(k.Calculate()); // 2
```

### Exercise 4

A network comprises of *n* computers, which are labeled *1, 2, ..., n*. In the network there is a set of connections, through which information can be sent both ways. You are given pairs of computers and your task is to find out, if they can communicate with one another.

* Create a class **Communication**, with the following methods:
  * **Communication(int n)**, the amount of computers is given to the constructor as a parameter.
  * **void AddConnection(int a, int b)**, adds a connection between *a* and *b*.
  * **bool Examine(int x, int y)**, returns *true* if there is a connection between *x* and *y*, otherwise returns *false*.

```cs
Communication com = new Communication(6);
com.AddConnection(1,2);
com.AddConnection(2,3);
com.AddConnection(1,3);
com.AddConnection(3,4);
com.AddConnection(5,6);
Console.WriteLine(com.Examine(1,4)); // true
Console.WriteLine(com.Examine(2,5)); // false
Console.WriteLine(com.Examine(5,6)); // true
```


### Exercise 5

Your task is to find the shortest path from *x* to *y* in a labyrinth. The labyrinth is a matrix of *n * m* size, and is constructed as follows: *#* means a wall, and *.* means a floor. You can assume that all the tiles on the outside are walls, and there is exactly one *x* and one *y* in the grid.

On a single turn, you can move one step left, right, up or down. You have to give the route of the shortest path as a string, which is made from characters *L*, *R*, *U* and *D* respectively. If there are multiple routes, you can return any of them.

* Create a class **Labyrinth** with the following method:  
  * **string Search(char\[,\] laby)**, returns the description of the shortest path (if there is none, returns null or empty string).      
  
  
  
  
Example code:          
  
  
  
```cs
Labyrinth l = new Labyrinth();
char[,] c = 
{ {'#','#','#','#','#','#','#'},
{'#','x','#','.','y','.','#'},
{'#','.','#','.','#','.','#'},
{'#','.','.','.','.','.','#'},
{'#','#','#','#','#','#','#'} };
Console.WriteLine(l.Search(c)); // DDRRUUR
```

HINT! You can save the width *n* and the height *m* with the following code:

HINT! For the shortest path, you have to make a breadth-first search (BFS).

```cs
int n = laby.GetLength(0);
int m = laby.GetLength(1);
```

## Part 6 - Shortest paths

* Deadline 16.6. at 23:59