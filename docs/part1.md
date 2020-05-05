---
title: "Part 1 - Introduction"
permalink: /part1/
nav_order: 3
published: true
---

# Introduction

In this course, we learn about algorithms and data structures, what they are and what do they do. This course is intended as a quick look into these matters, and will not go very deep. The idea of this course is to give you some insight, and hopefully raise some questions, and enable to search for more information on your own.

Learning programming is a long process, and it can be divided into two steps. First step is learnt in the course **Basics in Programming**, such as using variables, statements, loops and so on. The second step is to create **efficient** algorithms, a topic we shall look into in this course.

## Why is this necessary?

Even though most of the data structures we will handle on this course have been implemented in some (if not most) coding languages already, for more efficient use it is crucial to understand, how they are built, and what actually happens inside those data structures. Same applies for algorithms: someone, somewhere has probably already done the code you are looking for, but to understand the basics of algorithms is the key to make our own, personal code more efficient.

## What are algorithms?

*Algorithm*, in its simplest form, is an instruction. With said instruction, we can solve a computational problem. Algorithm is given an **input**, which describes the problem, and it produces an **output**, which is the answer to the given problem. All of us have encountered algorithms in our lives, but probably don't think of them as such. The most common algorithm in daily life is probably a **cooking recipe**. Let's take a look.


* 1/2 l    milk
* 50  g    yeast
* 1        egg
* 1,5 tsp  salt
* 0,2 l   sugar
* 1   tbsp cardemom
* 900 g of wheat flour
* 200 g butter

* egg for washing
* pearl sugar for decoration

Here we have our **input**. All these ingredients are needed to describe the "problem" of baking buns. Let's move on to our instructions.

1. Warm up the milk to body temperature and crumble the yeast into it.
2. Add the egg and mix.
3. Add salt, sugar and cardemom.
4. Add flour gradually and mix well.
5. Add softened butter.
6. Beat the dough well, until smooth and comes off your hands and the bowl.
7. Let rest under a cloth for 15 to 20 minutes.
8. Roll the dough on the table and cut into smaller pieces to form buns.
9. Raise the buns under a cloth
10. Wash the buns with beaten egg and add pearl sugar.
11. Bake the buns in 225 degrees Celcius for 8 to 10 minutes, or until golden brown.

Here we have our **instructions**. With the input and these instructions, we get the **output** of (hopefully) delicious Finnish sweet buns.

Let's look into a more computational problem. Let's have an list, where we have *n* integers, and the problem is to calculate the sum of said integers. For example, if our list would be \[2,4,1,8\], the desired output would be 15, since 2 + 4 + 1 + 8 = 15. We can solve this problem with an algorithm, which loops through the integers and counts their sum into a variable.

There are several ways to represent an algorithm. One way is to describe the functionality with words, like we just did. Other solution is to give the code, which implements the algorithm. This time we have to choose a coding language to describe our solution. 

For example, the next C# code implements the algorithm for calculating the sum of the numbers:

```cs
List<int> numbers = new List<int> { /* add n numbers */};

int sum = 0;
for (int i = 0; i < n; i++)
{
  sum += numbers[i];
}
Console.WriteLine(sum);
```

We could also represent the algorithm as **pseudocode** instead of an actual coding language. This means we write code, which is close to a proper programming language, but we can decide the exact notation our selves and take some liberties. This helps us create a more readable interpretation. For example, the algorithm in our example can be presented as follows;

```console
sum = 0
for each number in list
  sum += number
print(sum)
```

In this course, you can run into both kinds of implementations, depending on the situation. C# is used when we want to know how exactly something is done in said language. Otherwise, if we just want to have the general idea of an algorithm, we will use pseudocode.

## What are data structures?

*Data structure* is a data organization, management and organization format, meant to enable efficient access and/or modification of the data it holds. Data structure is a collection of data values, the relationships between them and defines the functions that can be used on said data.

We do not come by data structures in our physical world quite often, but as a loose example, a **cooking book** could be thought of as a data structure: It holds in data (the recipes), it is quite efficient to access (there's an indexed list at the beginning), it has the relations (one recipe might require another), and it defines the functions (you can read a recipe from the book, or even delete by ripping a page off).

Usually, how ever, data structures refer to computer science data structures, such as *arrays*, *lists*, *graphs* and *trees*. We are quite familiar in using the first two, but we shall look into them a bit deeper in this course. The two latter are more complex data structures, but are quite common, and ever so efficient. You will get familiar with them during this course.

## Basic parts of programming

Let's take a quick recap in the basics of programming. Even the most complex algorithms are constructed of the simplest of items. We shall go through some of the basic parts, which form a base for our algorithm design. Meanwhile, we will get to know pseudocode representations of some of the items.

### Variable

```cs
int a = 5;
int b = 7;
int c = a + b;
```

In pseudocode we use the variables similarly, but don't mark the types:

```console
a = 5;
b = 7;
c = a + b;
```

### Conditional statement

A conditional statement makes the program's function dependant from for example variable values. The next C# code tells if the variable is even or odd:

```cs
if (x % 2 == 0)
{
  Console.WriteLine("even");
}
else 
{
  Console.WriteLine("odd");
}
```

In pseudocode, it could look like

```console
if x % 2 == 0
  print("even")
else
  print("odd")
```

### Loop

Loop repeats the code inside it. Common loops are *for-loop* for certain set of values, and *while-loop*, which loops as long as the condition is true. For example, the following C# code prints numbers from 1 to 100:

```cs
for (int i = 1; i <= 100; i++)
{
  Console.WriteLine(i);
}
```

Same in pseudocode:

```console
for i = 1 to 100
  print(i)
```

The following code prints positive numbers, starting from *x* and and halves them with each step:

```cs
while (x >= 1)
{
  Console.WriteLine(x);
  x /= 2;
}
```

For example, with x = 50, the code will print 50, 25, 12, 6, 3, 1. And in pseudocode the same code is 

```console
while x >= 1
  print(x)
  x /= 2
```

### Array

Array is (one of) the most basic data structures in computer science. An array has *n* elements, indexed *from 0 to n-1*. This means that an array of size 3, has indexes 0, 1 and 2.

As an example, here's an array that can hold 5 integers, and we add two integers to it:

```cs
int[] numbers = new int[5];
numbers[0] = 4;
numbers[3] = 2;
```

In pseudocode we use array very similarly, but we do not usually initialize it in our code, we can assume such an array exists:

```console
numbers[0] = 4;
numbers[3] = 2;
```

An array is an excellent data structure, but it has two weaknesses:
1. You cannot change the size of an array after once defining it.
2. Finding a speficic element from an array is quite slow.

Array is still quite an important data structure, as for example the computer's memory is based on array-like structures. Thus any other data structure can be implemented using an array.

### Subprogram

Subprogram is a named part of a program, which can be called with parameters. A subprogram has multiple names, depending on the coding language, and in C# it is called a *method*.

For example:

```cs
void Print(int n)
{
  for (int i = 1; i <= n; i++)
  {
    Console.WriteLine(i);
  }
}
```

```console
void Print(n)
  for i = 1 to n
    print(1)
```

Or, to calculate a sum for numbers from 1 to *n*:

```cs
int Sum (int n)
{
  int s = 0;
  for (int i = 1; i <= n; i++) 
  {
    s += i;
  }
  return s;
}
```

```console
int Sum(n)
  s = 0
  for i = 1 to n
    s += i
  return s
```

### Recursion

We will handle recursion more deeply in this course later, but let's have a quick glance. It is quite often used in algorithm design, and it means that a subprogram calls for itself. Here's an example of recursion in action:

```console
void Hello(n)
  if n == 0
    return
  else
    print("Hello!")
    Hello(n-1)
```

This subprogram prints the line "Hello" *n times*. For example, the call **Hello(3)** gives the following result:

```
Hello!
Hello!
Hello!
```

The basic idea is, that if n = 0, the subprogram does not do anything, since there is nothing to print. Otherwise, it will print the line "Hello!" and then call itself with the parameter *n-1*.

Recursion is used quite often, and as said, we will look into it deeper, later on.

With the tools above, we can create *any algorithm possible*. Now it's up to us to *apply our knowledge* of different techniques to different situations.