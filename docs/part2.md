---
title: "Part 2 - Efficiency"
permalink: /part2/
nav_order: 3
published: true
---

# Efficiency

While designing algorithms, our aim is to create *efficient* algorithms. We want to create algorithms with which we can handle large amounts of date without using a large amount of time. We had a glimpse of that in the last exercise for the previous part.

It could be stated that an algorithm is *good*, when it can deliver a quick answer, even though we would *input* a large amount of data for it. In this part, we will concentrate on how to estimate the efficiency of algorithms, and how to possibly improve some algorithms in the means of efficiency.

*Time complexity* is a central term in efficency. It can give us a compact information of how much an algorithm spends time, from which we can determine the efficiency by looking at the structure of an algorithm, without necessarily implementing and testing the algorithm, just to know if it fast or not.

## Big O

*"Big O notation is a mathematical notation that describes the limiting behavior of a function when the argument tends towards a particular value or infinity.*

*In computer science, big O notation is used to classify algorithms according to how their run time or space requirements grow as the input size grows."* [**Wikipedia**](https://en.wikipedia.org/wiki/Big_O_notation)

We will use this notation in our following examples. This is a very common notation method, and learning it is the main issue of this part.

# Time Complexity

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

## Calculating Big O

Nice thing about time complexity is that we can usually deduct it simply by looking at the structure of an algorithm. Next we'll be looking at some calculation methods, which make this possible.

### Single operations

If the code does not have loops but only single operations, the time complexity is *O(1)*. For example:

```console
c = a + b
if c >= 0
  print(c)
```

Even though we go through three commands, i.e. we have *c = 3*, the notation is still O(1), as each command is run only once.

### Loops

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

### Operations after each other

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

### Multiple variables

Sometimes the time complexity is dependant on multiple factors, and the formula will have multiple variables. For example, the next time complexity is *O(nm)*

```console
for i = 1 to n
  for i = 1 to m
    ...
```

### Rekursive algorithms

For a recursive algorithm we calculate how many recursive calls are made, and how many operations a single call takes. Let's see the next method, which is called with a parameter *n*.

```console
int function(n)
  if n == 1
    return
  function(n-1)
```

The method is called *n* times and all the calls take *O(1)* time. We get the time complexity by multiplying these values together, so the method has a time complexity of *O(n)*. Let's take a look at another example.

```console
int g(n)
  if n == 1
    return
  g(n-1)
  g(n-1)
```

In this case, each method call produces two more calls, so the method is called in total

1 + 2 + 4 + ... 2^(n-1) = 2^n -1 

times. Each call takes *O(1)* time, so the time complexity is *O(2^n)*.

## Common time complexities

Certain time complexities are often found in algorithms. Let's go through a few of these.

### Constant time, O(1) 

*Constant time* algorithm runs a constant amount of operations, and the size of the input does not affect the speed. For example, the following calculation counts the sum for *1 + 2 + ... + n* in constant time.

```console
sum = n*(n+1)/2
```

### Logarithmic, O(log n)

*Logarithmic* algorithm often halves the input size on each operation. For example, the time complexity of the following is *O(log n)*.

```console
counter = 0
while n >= 1
  counter += 1
  n /= 2
```

An important issue with logarithms is, that log *n* is a *small* number, when *N* is any typical number in an algorithm. For example *log 10^6 ~ 20* and *log 10^9 ~ 30*, when the base of the logarithm is 2. Thus when an algorithm does something in logarithmic time, it does not take very long.

### Linear, O(n)

*Linear* algorithm can go through the input with a fixed amount of operations. For example the next *O(n)* algorithm counts the sum of the elements in an array.

```console
sum = 0
for i = 0 to n-1
  sum += array[i]
```

When the input is a data set with *n* elements, linear time complexity is often the best possible we can achieve. This is because the algorithm must go through the whole data set, before it can give us an output.

### (Sorting), O(n log n)

Time complexity of *O(n log n)* often refers to having *sorting* as part of the algorithm, as efficient sorting algorithms use *O(n log n)* time. For example, the following *O(n log n)* time complexity algorithm checks, if the array has two recurring elements.

```console
sort(array)
same = false
for i = 1 to n-1
  if array[i] == array[i-1]
  same = true
```

First, the algorithm sorts the array, after which the recurring elements are next to each other, and easy to find. Sorting takes time *O(n log n)* and the loop takes *O(n)*, so combined the algorithm takes time *O(n log n)*.

### Quadratic, O(n^2)

*Quadratic* algorithm can go through all the possible ways of selecting two elements from the input. For example, the next O(n^2) algorithm searches for two elements, whose sum is *x*.

```console
ok = false
for i = 0 to n-1
  for j = i+1 to n-1
    if array[i] + array[j] == x
      ok = true
```

### Cubic, O(n^3)

*Cubic* algorithm can go through all the possible combinations of three elements in the input. For example, the next algorithm searches for three numbers with the sum of *x*, and has time complexity of O(n^3)*

```console
ok = false
for i = 0 to n-1
  for j = i+1 to n-1
    for k = j+1 to n-1
      if array[i] + array[j] + array[k] == x
        ok = true
```

### (subsets and permutations), O(2^n) and O(n!)

If the time complexity is *O(2^n)*, this often tells us that the algorithm goes through subsets of the elements of the input. This also means that the growth doubles with each addition to the input data set. For example, the recursive calculation of Fibonacci numbers.

```console
int fibonacci(input)
  if input <= 1
    return input;
  return fibonacci(input - 2) + fibonacci(input - 1);
```

If the time complexity is *O(n!)*, the algorithm probably goes through the permutations of the elements from the input. The *!* in mathematical notation means *factorial*. For example, the factorial *5!* could be written as *5 * 4 * 3 * 2 * 1*. Our code example prints the numbers from input *n* in factorial manner.

```console
void factorial(n)
  for i = 0 to n
    print(n)
    factorial(n-1)
```

## Estimating efficiency

Why is it useful to define the time complexity of an algorithm? The benefit is, that the time complexity gives us an estimate of how *good* our algorithm is, or how well it can handle large inputs efficently. With more experience on algorithm design, we can get a clear picture what different time complexities mean in action.

We can get some idea by looking at this table:

|Size of the input | Required time complexity|
|--:|--:|
| 10 | O(n!) |
| 20 | O(2^n) |
| 500 | O(n^3) |
| 5000 | O(n^2) |
| 10^6 | O(n) or O(n log n) |
| large | O(1) or O(log n) |

Time complexity gives us a compact representation of efficiency. We do not have to know the details of an algorithm to get the general idea of efficiency. One interesting aspect to algorithm efficiency, is how large of an input it can handle *fast* (in fractions of a second). This is a good requirement, when we want to use our algorithm in some proper use. 

The table above gives us a ball park estimate of the sufficient time complexities, when done with a modern language on a modern computer. Keep in mind, that these are only estimates, and the real use of time can be affected by multiple reasons. The same algorithm done well can be multiple times faster than a bad version, and also the coding language itself can affect the result.



source: [**Tietorakenteet ja algoritmit**](https://github.com/pllk/tirakirja/raw/master/tirakirja.pdf)

### A small example

You can use multiple different types of algorithms to solve a problem. Next we'll look into a single task with two different algorithms. The first one is a *brute force solution*, working in *O(n^2)* time. The second one is an efficient algorithm, working in *O(n)* time.

The example as follows: The input is a string with length of *n* and each character (or element) is either 0 or 1. We want to calculate, how many different ways we can choose two parts of the input so, that the left character is 0 and the right character is 1. For example, in an input of 01001 we can find four ways for this selection:
**01**001, **0**100**1**, 01**0**0**1** and 010**01**.

### O(n^2) algorithm

We can solve the problem with brute force by going through each possible way to choose the left and right element. This way we can calculate one by one, how many ways the left character is 0 and the right is 1. The following code implements this algorithm:

```console
counter = 0
for i = 0 to n-1
  for j = 0 to n-1
    if chars[i] == 0 and chars[j] == 1
      counter += 1
print(counter)
```

The time complexity for this algorithm is O(n^2), since it has two indented loops, which go through the input.

### O(n) algorithm

Let's see if we can do this more efficiently. We need to find a way to get rid of the second loop from our algorithm. For this we should look at the problem from a different angle. When we are at a certain point of the string, in how many ways can we form a pair, whose right character is at our current location? If our current location points to a 0, there are no possible pairs, but if the character is 1, we can choose *which ever* zero which is left to our position to create a pair.

With this observation we only need to go through the string once from left to right and keep track, how many 0's we have seen. At each character of 1 we increase the answer by the amount of zeros so far. The following code implements the algorithm:

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

### Comparing the algorithms

We now have two algorithms, whose time complexities are *O(n^2)* and *O(n)*, but what does this mean in practice? We can find this out by creating the algorithms with an actual coding language and measuring their running times with different sizes of inputs. This will be done as an exercise.

# Space complexity

Time complexity is not the only aspect we should be interested in algorithms, when we are speaking about efficiency. Another key feature is *space complexity*.

Space complexity is used to describe, how much memory space an algorithm uses *in addition* to the input. If the space complexity is *O(1)*, algorithm needs space only for few variables. At a space complexity of *O(n)*, algorithm could have for example a temporary array the size of the original input.

Let's look at an example, where an array has the numbers 1, 2, ... ,n, par one, and our task is to determine the missing number. One way to solve this in time *O(n)* is to create a temporary array, which keeps track of the numbers included. The space complexity of such solution is *O(n)*, because the extra array takes *O(n)* amount of space.

```console
for i = 0 to n-2
  included[array[i]] = true
for i = 1 to n
  if not included[i]
    missing = i
```

There is another solution to this, whose time complexity is still O(n), but the space complexity is only O(1). This kind of an algorithm first calculates the sum of the numbers from 1 to n, and then substracts the elements from the array from it. The remainder is the value equal to the missing number.

```console
sum = 0
for i = 1 to n
  sum += i
for i = 0 to n-1
  sum -= array[i]
missing = sum
```

Notice, that instead of variables and arrays, *recursion* can also take up space, since all the information of recursive subprogram calls are in a recursion stack in memory. For example, the following method has a space complexity of *O(n)*, because there is at most *n* layers of recursive calls in the memory.

```console
int f(n)
  if n == 1
    return
  f(n-1)
```

In practice, space complexity does not play a major role in algorithms, since if the algorithm is *efficient*, it does not have the time to use up much memory. Especially, the space complexity can not be greater than time complexity. Thus we do not have to worry about space complexity as mcuh, but we can focus on creating algorithms which are fast and efficient, and compare the time complexity of different solutions.

[**Exercises here**](https://centria.github.io/algo-and-data/exercises/#part-2---time-complexity)