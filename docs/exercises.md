---
title: "Exercises"
permalink: /exercises/
nav_order: 99
published: true
---

# Exercises

* Each student is to create a git repository and send a link to that repository to the teacher before the first deadline, via email, or in Slack private message. **DO NOT SHARE YOUR REPOSITORIES WITH EACH OTHER**, even though they can be left public.

* Submission of the exercises is done by having the solutions as a code (or pseudocode) in the repository. *All the exercises are supposed to be done in C#, but you can get points for pseudocode solution.*

* The exercises need to be **clearly marked**. Create a separate class (and file) for all the exercises in one part, so you can try them out in a single Main.
  * [**Example for structure can be found here**](https://github.com/HeikkiHei/algo-examples), and you can use it as a template if you want.

* Each part has separate deadline, before the next part's lesson, *unless stated otherwise*. 

  * Public holidays or other force majeure sitations can move deadlines, and these will be informed in here.

* Submissions are done *by pushing to your personal repository*. The first submission requires submitting the link to the teacher.

* Answers will be gone through at the beginning of the next lesson, after deadline. 
  * After the last deadline, as there is no lesson, all the answers will be published here.

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

Limits:
 * Each string can be from 1 to 100 characters
 * All the characters are from a to z (non-capital)

The code should work as follows:

```cs
Substrings subs = new Substrings();
subs.Calculate("aybabtu", "bab"); // 1
subs.Calculate("aaaaa", "aa"); // 4
subs.Calculate("monkey", "banana"); // 0
```

### Exercise 3

As a parameter, give the program an array with integers. With each step, form a new array, where each element is the sum of two elements that were next to each other in the previous array. Eventually, you will have an array with only one element. For example, with \[1,2,3,2\] should first turn into \[3,5,5\], this into \[8,10\] and finally into \[18\].

* Create a class called **Tables**, which has the following method:

* **int Calculate(int[] t)**, which returns the value of the last element (an integer, not the whole array).

Limits: 
* An array has a maximum of 20 elements
* Each element is between 1...100

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

## Part 3 - Recursion

* Deadline 26.5. at 23:59

## Part 4 - Data structures

* Deadline 2.6. at 23:59

## Part 5 - Algorithms

* Deadline 9.6. at 23:59

## Part 6 - Implementing data structures

* Deadline 16.5. at 23:59