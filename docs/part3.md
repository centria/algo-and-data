---
title: "Part 3 - Recursion and Sorting"
permalink: /part3/
nav_order: 5
published: true
---

# Recursion

When we have *recursion*, a method is calling itself. A recursion must end at some point (it should not have an endless loop). The ending criteria is called a *base case*. It does not call the method and ensures the recursion will end.

Recursion is an effective way to represent a complicated algorithms function and logic, although understanding and using recursion takes a bit of practice.

Here's a simple example of how recursion works. Below are more useful examples. Let's have a real number *x* and a natural number *n*. We know, that 

x^n = 1, if n = 0  
x^n = x * x^(n-1), if n > 0

In this case, the n = 0 is the base case, which directly includes the solution. We can write this into a program:

```cs
public static double Power(double x, int n)
{
  if (n == 0)
  {
    return 1;
  }
  return x * Power(x, n - 1);
}
```
What happens, when we call for example **Power(2.0, 4)**? On mathemathical level, something like this:

```console
2^4 =
2 * 2^3 =
2 * (2 * 2^2) =
2 * (2 * (2 * 2^1)) =
2 * (2 * (2 * (2 * 2^0))) =
2 * (2 * (2 * (2 * 1))) =
2 * (2 * (2 * 2)) =
2 * (2 *4) =
2 * 8 =
16
```

Notice, how the recursion "expands" until we reach *n = 0* and then "rewinds" as we calculate the values one by one.

The method has a *run-time stack*, where all this information is stored, until we reach the very end. Basically it means having all the information in the computer memory. As we get into larger examples, the size of the stack might become quite large, and we might run out of memory.

## Single call

The simplest situation is when a method calls itself only once. For example:


```cs
static void Test(int n)
{
  Console.Write(n + " ");
  // The base case
  if (n == 1) return;
  // The recursive call
  Test(n - 1);
}

static void Main(string[] args)
{
  Test(10);
}
```

Here the method **Test** first prints the value for parameter *n*. If n is 1, the method does not continue to run, it ends. Otherwise the method calls itself with a one smaller parameter, *n - 1*. The example print is as follows:

```console
10 9 8 7 6 5 4 3 2 1 
```

## Multiple calls

The situation becomes more interesting, when a mehtod calls itself multiple times. The following code is otherwise equal to the previous one, but the now at the end we have *two* recursive calls:

```cs
static void Main(string[] args)
{
  Test(4);
}

static void Test(int n)
{
  Console.Write(n + " ");
  if (n == 1) return;
  Test(n - 1);
  Test(n - 1);
}
```

Now the example print is as follows:

```console
4 3 2 1 1 2 1 1 3 2 1 1 2 1 1
```

## Stack size

The next method **Sum** calculates the sum *1 + 2 + 3 ... + n* with recursion.

```cs
static void Main(string[] args)
{
  Console.WriteLine(Sum(10)); // 55
}

static long Sum(int n)
{
  if (n == 0) return 0;
  else return Sum(n - 1) + n;
}
```

Everything goes smoothly, when the *n* is small, but with large parameters (like one million), we get an error:

```console
Stack overflow.
```

The reason for this is that all the inner calls we make take space from a memory space, we call a **Stack**. The size of this value is by default limited, and if a recursion has many layers, we might run out of memory.

There are ways of getting around this problem, but those will not be taught in this course. Increasing stack size is not a valid solution. Rather we should make our code work without overflow.


## Example: Files

One reasonable use for recursion is to go through a folder with files in them. We will use the following structure in our example:

```console
test
├── 1.txt
├── 2.txt
├── mary
│   ├── 3.txt
│   ├── 4.txt
│   ├── banana
│   │   ├── 7.txt
│   │   └── 8.txt
│   ├── coconut
│   │   ├── 10.txt
│   │   └── 9.txt
│   └── monkey
│       ├── 5.txt
│       └── 6.txt
└── mike
    ├── 11.txt
    └── 12.txt
```

The following method **Examine** will go through the contents of a given folder. The *File object* given as a parameter can be either a file or a folder. If it is a folder, the method will recursively go through its content. If it is a file, the method will print its name.

```cs
static void Main(string[] args)
{
  Examine("test");
}

static void Examine(string path)
{
  // Check if the file is a directory
  // If the directory does not exist, it's a regular file
  // Or we have a wrong path, and we do not need to continue anyways
  if (Directory.Exists(path))
  {
    // For each file name in the directory
    // GetFileSystemEntries covers files and folders
    foreach (string fileName in Directory.GetFileSystemEntries(path))
    {
      // Recursively call the method
      Examine(fileName);
    }
  }
  // If the file is not a directory
  // Print the name
  else Console.WriteLine(path);
}
```

Our code prints as follows:

```console
test/1.txt
test/2.txt
test/mary/3.txt
test/mary/4.txt
test/mary/banana/7.txt
test/mary/banana/8.txt
test/mary/coconut/10.txt
test/mary/coconut/9.txt
test/mary/monkey/5.txt
test/mary/monkey/6.txt
test/mike/11.txt
test/mike/12.txt
```

## Iterative solutions

As you might have guessed, not everything is reasonable to create with recursion. In the beginning, we had a solution for calculating mathemathical powers with recursion. A more reasonable way could be for example:

```cs
public static double Power(double x, int n)
{
  double result = 1;
  for (int i = 1; i <= n; i++)
  {
    result *= x;
  }
  return result;
}
```

This solution takes up much less space (and is faster), since we do not need a recursion stack. In theory, every recusion can be changed into an iteration. There are solutions, of course, which are easier to explain in one way or the other.

Recursion is usually easier to understand and to create, and the code is shorter. It is, how ever, usually also slower, and takes up more memory space.

# Sorting algorithms