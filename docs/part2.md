---
title: "Part 2 - Efficiency"
permalink: /part2/
nav_order: 3
published: true
---

# Efficiency

While designing algorithms, our aim is to create *effcient* algorithms. We want to create algorithms with which we can handle large amounts of date without using a large amount of time. We had a glimpse of that in the last exercise for the previous part.

It could be stated that an algorithm is *good*, when it can deliver a quick answer, even though we would *input* a large amount of data for it. In this part, we will concentrate on how to estimate the efficiency of algorithms, and how to possibly improve some algorithms in the means of efficiency.

*Time complexity* is a central term in efficency. It can give us a compact information of how much an algorithm spends time, from which we can determine the efficiency by looking at the structure of an algorithm, without necessarily implementing and testing the algorithm, just to know if it fast or not.

## Big O

*"Big O notation is a mathematical notation that describes the limiting behavior of a function when the argument tends towards a particular value or infinity.*

*In computer science, big O notation is used to classify algorithms according to how their run time or space requirements grow as the input size grows."*[**Wikipedia**](https://en.wikipedia.org/wiki/Big_O_notation)

We will use this notation in our following examples. This is a very common notation method, and learning it is the main issue of this part.

## Time Complexity

The efficiency of an algorithm is determined by how many operations it takes to run. Our goal now is to estimate the the *amount of operations* in relation to the size of the input *n*. For example, if we had an array for input, *n* would be the size of the array, and if the input would be a string, *n* is the length of said string.

Let's look at an example algorithm, which calculates how many times element *x* can be found from an array of the size *n*

```console
1 counter = 0
2 for i = 0 to n-1
3   if numbers[i] == x
4     counter++
```

We can estimate the efficiency of an algorithm by looking at each line, how many times did the algorithm run it. Our first line is run only once, at the very beginning. After this begins a loop, where lines 2 and 3 are both run *n* times, and line 4 is run *0...n* times, depending on how many times *x* can be found from the array. The algorithm uses at least *2n + 1* and at most *3n + 1* operations.

Analysis of this depth is usually not necessary, how ever. Our goal is to find the *upper limit*, often also called *worst case*. 

We say that an algorithm takes *O(f(n))* time, or its *time complexity* is *O(f(n))*, if it runs at most *cf(n)* operations every time when *n >= n_0*, where *c* and *n_0* are constant. For example, the algorithm above takes *O(n)* time, because it cleary runs a maximum of *4n* operations on all values of *n*.

As our algorithm above always does a maximum of 4 operations, per each element in the array of the size *n*, we get the *worst-case scenario* of a maximum of *4 times n operations*. To place these in our notation *O(cf(n))*, we acknowledge that *c = 4*, and *f(n)* is the function over *n*. This way we get *O(4n)* as our very worst case complexity, and simplify to *O(n)* as our time complexity.

### Calculating Big O

Nice thing about time complexity is that we can usually deduct it simply by looking at the structure of an algorithm. Next we'll be looking at some calculation methods, which make this possible.

#### Single operations

If the code does not have loops but only single operations, the time complexity is *O(1)*. For example:

```console
c = a + b
if >= 0
  print(c)
```

Even though we go through three commands, i.e. we have *c = 3*, the notation is still O(1), as each command is run only once.

#### Loops

We will mark *...* for code, which uses O(1) time. If code has only one loop which takes *n* operations, the time complexity is *O(n)*.

```console
for i = 1 to n 
  ...
```

If we have two loops indented, the time complexity is *O(n^2)*

```console
for i = 1 to n 
  for j = 1 to n 
    ...
```

In general, if the code has *k* indented loops, the time complexity is *O(n^k)*.

Notice, that the constants and lower time complexities do not affect the time complexity. For example, in the following loops there are *2n* and *n - 1* operations, but the time complexity for both are *O(n)*.

```console
for i = 1 to 2*n 
  ...
```

```console
for i = 1 to n - 1
  ...
```

#### Operations after each other

If the code includes multiple sections, the time complexity is that of the largest time complexity. For example, the following code has a time complexity of *O(n^2)*, because the time complexities of its parts are *O(n)*, *O(n^2)* and *O(n)*.

```console
for i = 1 to n
  ...
for i = 1 to n
  for j = 1 to n
    ...
for i = 1 to n
  ...
```

#### Multiple variables

Sometimes the time complexity is dependant on multiple factors, and the formula will have multiple variables. For example, the next time complexity is *O(nm)*

```console
for i = 1 to n
  for i = 1 to m
    ...
```

#### Rekursive algorithms