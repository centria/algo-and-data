---
title: "Part 1 - Introduction"
permalink: /part1/
nav_order: 3
published: true
---

# Introduction

In this course, we learn about algorithms and data structures, what they are and what do they do. This course is intended as a quick look into these matters, and will not go very deep. The idea of this course is to give you some insight, and hopefully raise some questions, and enable to search for more information on your own.

Learning programming is a long process, and it can be divided into two steps. First step is learnt in the course **Basics in Programming**, such as using variables, statements, loops and so on. The second step is to create **efficient** algorithms, a topic we shall look into in this course.

## Why are we here?

Even though most of the data structures we will handle on this course have been implemented in some (if not most) coding languages already, for more efficient use it is crucial to understand, how they are built, and what actually happens inside those data structures. Same applies for algorithms: someone, somewhere has probably already done the code you are looking for, but to understand the basics of algorithms is the key to make our own, personal code more efficient.

## How does this course work?

The course runs for 6 weeks and is worth 3 credits. As one credit is 27 hours, this means that weekly amount of work is around 15 hours. Out of this 15, 5 are considered for the lectures (even though they might not last that long), and around 10 for homework.

The course consists of lectures, which at least in **spring 2020** are held online, in Teams. Each lecture session is 2-3 x 90 minutes or so, depending on the session and the amount of questions from the students. For best learning experience, I encourage you to ask questions, especially if you want to know more of a certain subject.

After the lecture, exercises will be published, and the deadline is before the next week's lecture, unless stated otherwise. The exercises are meant to be done individually, and each student return their own answers. You can, of course, help each other, and I do encourage you to do so. Each student, anyways, returns their own answers. [**More information about the exercises are on the exercise page.**](../exercises)

## What are algorithms?

Algorithm, in its simplest form, is an instruction. With said instruction, we can solve a computational problem. Algorithm is given an **input**, which describes the problem, and it produces an **output**, which is the answer to the given problem. All of us have encountered algorithms in our lives, but probably don't think of them as such. The most common algorithm in daily life is probably a **cooking recipe**. Let's take a look.


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
print sum
```

In this course, you can run into both kinds of implementations, depending on the situation. C# is used when we want to know how exactly something is done in said language. Otherwise, if we just want to have the general idea of an algorithm, we will use pseudocode.