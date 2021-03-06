---
title: "Exam prep"
permalink: /examprep/
nav_order: 999
published: true
---

# Preparations for the exam

* The exam will be held *23.10.2020 at 10.00*, IN TEAMS.
  * Teams link will be in Slack
* Actual Exam done via Microsoft Forms
* The exam will be done from home, from your own computer
  * *Web camera on, so I can see you doing the exam!*
* The exam will consist of 20 questions
  * Questions range from multiple choice to coding
  * Question difficulty varies from easy to extreme
  * Once again, even trying can get you points!
* The exam is graded, so you can pass the course even without the exercises
* Your best grade matters (exercises / exam)
* Exam is compulsory, even if you pass with just the exercises

## Exam grading

The exam will have a total of 55 points, and questions in the exam range from 1 to 8 points, depending on the difficulty. Some of them are quite easy and small, some of them are larger. There are a total of 20 questions.

| Score | Grade |
|--|--|
| 0 - 24 | 0 |  
| 25 - 30 | 1  |
| 31 - 36 | 2  |
| 37 - 42 | 3  |
| 43 - 48 | 4  |
| 49 - 55 | 5  |

## Exercises before the exam

As promised, you can do exercises to rehearse for the exam. These exercises can also be used for the exercise grade, so it is recommended you do these, no matter what. These exercises are worth 10 points in total (2 points for 1-3, 4 points for 5).

* Do these exercises in the same repository as you did your course exercises.
* Make a separate folder for these in the the repository
* Deadline is *22.10. at 23.59*
* Same rules apply as with regular exercises, i.e. you can get points for trying and pseudocode

### Exercise 1

You start to calculate a sum of numbers, 1, 2, 3, etc, until the sum of the numbers is at least *n*. How far do you have to traverse, to reach the sum? For example, if *n = 11*, the correct answer is *5*, as *1+2+3+4=10* and *1+2+3+4+5=15* (which is more than 11).

* Create a class **Numbers**, which calculates the amount of steps needed.
  * **int Steps(int x)**, returns the number of steps required.

For example:

```cs
Numbers num = new Numbers();
Console.WriteLine(num.Steps(11)); // 5
Console.WriteLine(num.Steps(15)); // 5
Console.WriteLine(num.Steps(2)); // 2
```

### Exercise 2

You are given a array with *n* integers. With each step you can choose *two adjacent integers of same value* and remove them from the array. You want to remove as many integers as possible.

For example if the array is \[1,2,2,1,1,1,3\], you can do the removals like this:
* \[1,2,2,1,1,1,3\]
* \[1,1,1,1,3\]
* \[1,1,3\]
* \[3\]
This is the shortest possible array with this method.

* Create a class **ShortenArray**
  * **int Calculate(int[] input)**, returns the shortest possible size of the array after the removals.

For example:

```cs
ShortenArray s = new ShortenArray();
int[] array1 = {1,2,2,1,1,1,3};
int[] array2 = {1,2,3,4,5,6,7,8};
int[] array3 = {1,1,1,1,2,2,2,2};
int[] array4 = {1,2,3,4,4,3,2,1};
int[] array5 = {1,2,1,1,2,2,1,1,2,2,1};
Console.WriteLine(s.Calculate(array1)); // 1
Console.WriteLine(s.Calculate(array2)); // 8
Console.WriteLine(s.Calculate(array3)); // 0
Console.WriteLine(s.Calculate(array4)); // 0
Console.WriteLine(s.Calculate(array5)); // 3
```

### Exercise 3

You are given a map of rooms in a house, and your task is to calculate, how many rooms a house has. A map is a grid where each square is either floor (marked with *0*) or wall (marked with *1*). Two floor squares are in the same room, if they are adjacent horizontally or vertically. You can assume each square on the outer perimeter is wall.

* Create a class **Rooms**
  * **int Calculate(int[,] input)**, returns the amount of rooms in the house.

For example:

```cs
Rooms r = new Rooms();
int[,] house = {
    {1,1,1,1,1,1,1,1},
    {1,0,1,0,1,0,0,1},
    {1,1,1,0,1,0,1,1},
    {1,0,1,0,1,0,0,1},
    {1,1,1,1,1,1,1,1},
};
Console.WriteLine(r.Calculate(house)); // 4

```

### Exercise 4

You are given details about flights between cities, and your task is to find the best route between cities. All flights go only one way. You should primarily minimize the amount of flights and secondarily the total price.

* Create a class **Flights** with following methods:
  * **public void AddConnection(string departure, string destination, int price)**
  * **public int RoutePrice(string departure, string destination)**

The method **AddConnection** adds a connection between cities **departure** and **destination**, with the price of **price**. The method **RoutePrice** returns the best price from city **departure** to the city **destination** (or -1 if there is no such route). Each connection price is between 1...1000, and each city name contains 1...10 letters from a...z, lowercase.

For example:

```cs
Flights f = new Flights();
f.AddConnection("helsinki", "tampere", 100);
f.AddConnection("tampere", "oulu", 100);
f.AddConnection("oulu", "vaasa", 100);
f.AddConnection("helsinki", "turku", 500);
f.AddConnection("turku", "vaasa", 700);
Console.WriteLine(f.RoutePrice("helsinki","vaasa")); // 1200
```

Notife, that it would be cheaper to travel via *tampere* and *oulu*, but this would mean three flights, whereas the best route through *turku* only has two flights.