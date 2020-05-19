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

Sorting is an essential problem in algorithmics, where the problem is to sort *n* elements into order of magnitude. For example, we could have an array **\[5, 2, 4, 2, 6, 1\]** and we could sort the elements from smallest to largest, resulting in **\[1, 2, 2, 4, 5, 6\]**.

Our goal is to do this *efficiently*. It is easy to sort an algorithm in *O(n^2)*, but this is too slow on a large array. We will look into some efficient sorting algorithms, which only take *O(n log n)* time.

We can use sorting in many ways in algorithm design, because we can often make the problem solving easier by first orderding the data.

## Sorting in O(n^2)

Let's first see a simple sorting algorithm, which sorts an array with *n* elements in *O(n^2)* with two loops. Even though the algorithm is not fast, it is worth knowing and gives a base for designing more efficient algorithms.

## Insertion sort

*Insertion sort* goes through the array from left to right. When the algorithm comes into a certain point in array, it will move the element in that position to the correct position in the beginning of the array, so that the beginning of the array is in order. So, when the algorithm reaches the end, the whole array is sorted.


![Merge sort](https://github.com/centria/algo-and-data/raw/master/assets/images/insertionsort.png)  
source: [**Tietorakenteet ja algoritmit**](https://github.com/pllk/tirakirja/raw/master/tirakirja.pdf)


Here we see the insertation sort in action. In each row, the element highlighted in gray is moved into its correct position in the beginning of the array. The line marks the location of where the array is sorted upto. The following code will implement this sorting:

```console
for i = 1 to n-1
  j = i-1
  while j >= 0 and array[j] > array[j+1]
    swap(array[j], array[j+1])
    j -= 1
```

The code goes through all the positions *1...n-1* and transfers the element in position *i* to the correct position. This is done with the inner while-loop, where each step swaps the element and the one left of it. Here the command *swap* is a notation for switching the two elements together.

The efficiency of insertion sort is dependant on the content of the array we are sorting. The algorithm is faster, the more the array is already in order. If the array is already in order, it spends *O(n)*, since no element needs to be moved. The worst case for the algorithm is an array in *inverted order*, where each element has to be moved to the beginning of the array, and time spent is *O(n^2)*.

## Inversions

A useful term in analysation of sorting algorithms is *inversion*: two elements in an array, which are in wrong order. For example in array **\[3, 1, 4, 2\]** is three inversions: **(3,1)**, **(3,2)** and **(4,2)**. The amount of inversions tells about the order of the array: The less there are inversions, the closer the array is to being in correct order. Most notably, *an array is in order when it has no inversions*.

When a sorting algorithm sorts an array, it *removes* inversions. For example, each time the insertion sort swaps the two elements with each other, it is removing one insertion from the array. Thus the work load for insertion sort is equal to the amount of inversions in the array.

We have already established, that the worst input for insertion sort is a reverse ordered array. In an array like this each pair of elements create an inversion, so the amount of inversions is

n(n-1) / 2 = O(n^2)  

How well does the insertion sort work *on average*? If we assume that an array has *n* elements in random order, each pair of elements forms an inversion with the probability of 1/2. Thus the *expected value* for inversions is

n(n-1) / 4 = O(n^2)  

Which means we are still spending quadratic time. The reason why insertation sort is so *inefficient* is that it does not remove the inversions efficiently enough. If we want to create a better sorting algorithm, we have to design it in such a way, that it can remove multiple inversions *at the same time*. In practice, the algorithm should be able to move the element from the wrong position to the other side of the array *efficiently*.

## Sorting in O(n log n)

Next we will look into two efficient sorting algorithms, which are based on recursion. In both algorithms the idea is, that when we want to sort an array, we split it into two smaller parts and sort them recursively. After this we merge the sorted subarrays into a complete sorted array.

## Merge sort

![Merge sort](https://github.com/centria/algo-and-data/raw/master/assets/images/mergesort.png)  
source: [**Tietorakenteet ja algoritmit**](https://github.com/pllk/tirakirja/raw/master/tirakirja.pdf)

*Merge sort* is a recursive sorting algorith,. which is based on halving the array. When we get an array of size *n* to be sorted, we split it from the middle into two subarray, which both have aproximately *n/2* elements. After this we sort the subarrays and *merge* the sorted subarrays, so that they form a complete ordered array. Recursion ends at *n = 1*, when array is already in order and nothing more needs to be done. The following code shows the functionality of merge sort:

```console
sort(a,b)
  if a == b
    return
  k = (a+b)/2
  sort(a,k)
  sort(k+1,b)
  merge(a,k,k+1,b)
```

The method sorts the array *a...b* (a subarray from point *a* to point *b*), so if we want to order the whole array, we call the method with parameters *a = 0* and *b = n-1*, i.e. the first and the last index. First the method checks if the array only has one element, and if so, the method ends. Otherwise it will save the middle value into the variable *k* and sorts the left and right parts recursively. In the end, it will call the method *merge*, which combines the ordered halves. The next code shows the functionality of this method:

```console
merge(a1, b1, a2, b2)
  a = a1, b = b2
  for i = a to b
    if a2 > b2 or (a1 <= b1 and array[a1] <= array[a2])
      help[i] = array[a1]
      a1 += 1
    else
      help[i] = array[a2]
      a2 += 1
  for i = a to b
    array[i] = help[i]
```

As parameters are given values *a1...b1* and *a2...b2*, where *b1 + 1 = a2*. The method assumes, that the values between these have been ordered, and it will merge the elements in a way that the whole area *a1...b2* is ordered. The method is based on a loop, which goes through the *a1...b1* and *a2...b2* side by side, and chooses the always the next smallest element to the final order. For the merge not to mix the array, the method uses a global help array, where it first forms the sorted subarray, and then copies the elements from said array to the actual array.

The picture above shows how the algorithm works with an array **\[5, 1, 2, 9, 7, 5, 4, 2\]**. First the array is halved into **\[5, 1, 2, 9\]** and **\[7, 5, 4, 2\]** and it sorts both of these subarrays by calling itself. When the algorithm gets the array **\[5, 1, 2, 9\]** as a parameter, it will divide it into subarrays **\[5, 1\]** and **\[2, 9\]**, and so on. Eventually we will have subarrays of Length one left, which are in order. Then the rekursive division ends and the algorithm starts to reassemble the sorted subarrays from smallest to largest.

How efficient is merge sort? Since all the calls in the method *sort* half the size of the array, the recursion will form *O(log n)* layers (see the picture above). On the topmost layer we have an array with *n* elements, next level we have two arrays with *n/2* elements, next we have four arrays with *n/4* elements, and so on. The method *merge* functions in linear time, So on each level the merges take up *O(n)*. Thus the total time complexity of the algorithm is *O(n)* * *O(log n)*, which is of course *O(n log n)*.

## Quick sort

![Merge sort](https://github.com/centria/algo-and-data/raw/master/assets/images/quicksort.png)  
source: [**Tietorakenteet ja algoritmit**](https://github.com/pllk/tirakirja/raw/master/tirakirja.pdf)

*Quick sort* gives another type of recursive approach to sorting an array. When we receive an array to be sorted, we first choose one of its elements as the *pivot*. After this we shift the elements so, that the elements *smaller than the pivot* are on the left side of the pivot, and the elements *larger than the pivot* are on the right side, and equal elements can be *on either side*. Finally, we recursively sort the subarrays, which are formed on the left side and the right side of the pivot. The following code shows us this functionality:

```console
sort(a, b)
  if a >= b
    return
  k = pivot(a,b)
  sort(a, k-1)
  sort(k+1, b)
```

The method sorts the array with range *a...b*. If the range is empty or if it has only one element, the method does nothing. Otherwise it will call the method **pivot**, which chooses the *pivot*, shifts the elements accordingly and returns the position *k*, where the pivot will be after the shifts.

After this, the the left part of the array (a...k-1) and right part (k+1...b) are sorted recursively.

The function **pivot** can be done in many ways, because we can choose any element as the pivot point, and there are many ways with which to move the elements. In our example, we are using the follwing code:

```console
pivot(a,b)
  k = a
  for i = a+1 to b
    if array[i] < array[a]
      k += 1
      swap(array[i], array[k])
  swap(array[a], array[k])
  return k
```

In this example, the pivot is always the first element. The method goes through each element in the range, and moves the elements smaller than the pivot to the beginning. The variable *k* determines the position, where the next smaller element will be moved. In the end, the pivot itself will be moved to the middle to position *k*, which the method returns.

The picture above shows how the algorithm works with an array **\[5, 1, 2, 9, 7, 5, 4, 2\]**. Each grey element shows the location of the pivot. First the pivot for the whole array is 5, and the algorithm moves the elements so that on the left side there are elements **\[2, 1, 2, 4\]** and on the right **\[5, 9, 7\]**. After this the left and right subarrays are sorted similarly recursively.

The efficiency of quick sort is dependant on how the elements are divided around the pivot. If we are lucky, there are approximately the same amount of elements on both sides of the pivot. This way the array is halved after every pivot, and quick sort is efficient. As the method **pivot** works in linear time, quick sort takes in this situation *O(n log n)*, just like merge sort.

There is a possibility, that the pivot point divides the array unevenly. The image below illustrates a situation, where all the elements are on the right side of the pivot. This time quick sort takes up *O(n^2*), since there are *O(n)* recursive levels. It clearly is *not* a good idea to choose the first element of an array as the pivot in all cases. For example, an array that is already in order, takes up *O(n^2)* time.

![Merge sort](https://github.com/centria/algo-and-data/raw/master/assets/images/badsplit.png)  
source: [**Tietorakenteet ja algoritmit**](https://github.com/pllk/tirakirja/raw/master/tirakirja.pdf)


Another situation is where an array has multiples of the same value. In extreme situation, *all the elements* are the same, which is a very possible input. This time the method **pivot** in our soilution will always create a bad result, where all the elements are on the right side of the pivot. It is not enough to choose a good pivot, but also the way of moving elements affects the efficiency of quick sort.

How could we improve quick sort? There have been multiple variations over the years, which aim to improve it. On more advanced way of choosing a pivot is to take the first, middle and last elements, and choose the one which is in the middle of these three in order. This works quite well in most cases. A better way of moving elements for example is to go through side by side elements from the beginning and the end, and to make sure the pivot stays in the middle, if all the elements are equal.

These were just two common ways of sorting an array, but there are many, many more. You can find more about other sorting algorithms from here [**https://en.wikipedia.org/wiki/Sorting_algorithm**](https://en.wikipedia.org/wiki/Sorting_algorithm).

## Using sorting

The meaning of sorting for algorithmics is that we can solve problems efficienty, as long as the data is in order. Thus a common way to create an efficient algorithm is first to sort the input in *O(n log n)* and then use the sorting to our advantage later in the algorithm.

## Array algorithms

With sorting we can solve in *O(n log n)* time many tasks for arras. We will now go throught two of such tasks.

First task is to calculate, how many *different* elements a given array has. For example, an array **\[2, 1, 4, 2, 4, 2\]** includes three different elements: 1, 2 and 4. We can solve this by first sorting the array, after which the equal numbers are next to each other. After this we can calculate the output easily, as we only need to check at how many position there are different elements *next to each other*. We can do it like this:


```console
sort(array)
counter = 1
for i = 1 to n-1
  if array[i-1] != array[i]
    counter += 1
print(counter)
```

The algorithm first sorts the array in time *O(n log n)*, after which it goes through the array with a for-loop in *O(n)*. The total time complexity is *O(n log n)*.

But what if we want to know, what is the *most common* value in the array? With the same example array, the most common element is 2, as it is three times in the array. This can also be done with sorting, since after it the same elements are next to eachh other, and all we have to do is find the longest repetition. We can do it as follows:

```console
sort(array)
amount = 1
largest = 1
common = array[0]
for i = 1 to n-1
  if array[i-1] != array[i]
    amount = 0
  amount += 1
  if amount > largest
    largest = amount
    common = array[i]
print(common)
```

Also here the sorting algorithm takes *O(n log n)*, and for-loop takes *O(n)*, so the total time complexity is again *O(n log n)*.

## Binary search

*Binary search* is a method for finding an element from a sorted array in time *O(log n)*. The idea is to keep in mind the search range where the value can be, and half the range with each step by looking at the element in the middle of the range. As the array is in order, we can always deduct, which way we should keep going with our search. The following code searches an element *x* from an array with binary search:

```console
a = 0
b = n-1
while a <= b
  k = (a+b)/2
  if array[k] == x
    // we found the x
    break
  if array[k] < x
    a = k+1
  if array[k] > x
    b = k-1
```

The algorithm keeps track of the search range **\[a,b\]**, which at the beginning is **\[0, n-1\]**, since the element might be anywhere in the array. With each step the algorithm checks the element in the middle *k = (a+b)/2*. If it is *x*, the search ends. If the element is less than *x*, the search continues on the right side, and if it is more than *x*, the search continues on the left side. As the range is halved on each step, the time complexity is *O(log n)*.

![Binary search](https://github.com/centria/algo-and-data/raw/master/assets/images/binarysearch.png)  
source: [**Tietorakenteet ja algoritmit**](https://github.com/pllk/tirakirja/raw/master/tirakirja.pdf)

The picture above shows the functionality, when we are looking for the value of *6* from an ordered array. At first, the range is the whole array, and the middle element is 4. Thuse we know, that if the array contains a 6, it has to be at the right half of the array. Next the range is the top half of the array, and the middle is at 7. Now we can deduct, that 6 has to be on the left side of this. The range is halved on each step, and as we continue, after two more steps there is only one element in the range, and it is 6, which we were looking for.

With binary search we could find out for example, if the array has two elements *a* and *b* so, that *a + b = x*, where x is the given input. The idea is to sort the array first and then go through all the elements of the array. With each element we examine, could it be *a*. In this case, there would have to be another element *b* in such a way, that *a + b = x*, or the array should contain an element *x - a*. We can find this with binary search in *O(log n)*. As a result, we have an algorithm, which takes up time *O(n log n)*, because both sorting and going through the array with binary search take up *O(n log n)*.

[**Exercises here**](https://centria.github.io/algo-and-data/exercises/#part-3---recursion)