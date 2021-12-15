---
description: Overview of dynamic programming
---

# Dynamic Programming

### Memoization

#### Overview

Memoization steps:

1. Find any solution, focusing on _correctness._

* Visualize the problem as a tree
* Implement the tree using recursion
* Test it for correctness

1. Make the solution more efficient.

* Add a memo object
* Add a new base case to check the memo keys (fetching logic)
* Implement the storing logic (placing keys/values into memo)

#### ex. fib memoization

Take a number n and return the nth number of the fibonacci sequence.

Overview: Solve this recursively with memoization. The problem with not using memoization is not the correctness of the function but the efficiency. Without memoization the runtime for large n values grows very fast O(2^n). To fix this we implement a cache to avoid duplication of calculations, reducing the runtime. This may be made clearer in the code blocks below and the image.

We see in the image below that we are repeating calculations very frequently. Each subtree is repeated (besides 6 and 7) and this means calculating the subtrees multiple times is inefficient. The idea is to "remember" previous calculations by storing the fibonacci values for values < n in a hash map, which can be accessed in constant time. Below is an example of the code with and without memoization.

![fibonacci tree for n = 7](<.gitbook/assets/Screen Shot 2021-05-30 at 11.24.05 PM (1).png>)

Below is an example without memoization using recursion with a base case n <= 2.

```
def fib(n):
    if n <= 2:
        return 1
    return fib(n - 1) + fib(n - 2)
```

Below is the code with a cache. We see that if we've already calculated a specific n value, it will be stored in the memo hash table and accessed in constant time. Doing a runtime analysis we can observe that we only calculate the subtree for each given integer 0 - n one time, and after that we just access it in the hash-map. It follows then that this runs in O(n) time.

```
memo = {}
def fib(n):
    nonlocal memo
    if n in memo:
        return memo[n]
    if n <= 2:
        return 1
    memo[n] = fib(n - 1) + fib(n - 2)
    return memo[n]
```

#### ex. gridTraveler

Given the dimensions of an m x n grid, calculate the numbers of ways to get from the top left corner to the bottom right corner, assuming you can only move right and down. For example, calling gridTravel(2, 3), which is a 2 x 3 grid, would have 3 different paths, so it would return 3.

We can first think about the naive solution that makes use of recursion and runs rather slowly. The code for this method is shown below. Because we don't yet make use of memoization, this code has an exponential runtime. If we visualize the problem as a tree, we would get a tree with a height of max(m, n) with each level having double the nodes as the last level. This means that the complexity becomes O(2 ^ (m + n)).

```
def gridTraveler(m, n):
    if m == 1 and n == 1:
        return 1
    else if m == 0 or n == 0:
        return 0
    a = 1 + gridTravel(m - 1, n)
    b = 1 + gridTravel(m, n - 1)
    return a + b 
```

Now we can optimize the code with memoization. Like the fibonacci problem (and many other dp problems), we can look at the tree and try to find duplicates, then use memoization. Additionally, in this specific problem we can recognize that gridTraveler(a, b) = gridTraveler(b, a), which will save even more time. Below I implement this idea in code. Doing a runtime analysis we can observe by observation that we will be "calculating" m x n grids a single time for each unique m and n combination, and then accessing the grid in the hash map every time it is called after the first time. This ultimately yields a runtime of O(m \* n).

```
memo = {}
def gridTravelerMem(m, n):
    nonlocal memo
    key = m + ',' + n
    if key in memo:
        return memo[key]
    if m == 1 and n == 1:
        return 1
    if m == 0 or n == 0:
        return 0
    memo[key] = gridTravelerMem(m - 1, n) + gridTravelerMem(m, n - 1)
    return memo[key]
    
```

#### ex. canSum/howSum/bestSum (code only, less explanation)

Implement a function that takes in a targetSum and an array of numbers and returns a boolean indicating whether it is possible to generate the targetSum from the array. Items in the array can be reused. All numbers are nonnegative integers.

Below is without memoization. This is O(n^m), where n is the amount of numbers and m is the targetSum.

```
def canSum(targetSum, numbers):
    if targetSum == 0:
        return True:
    if targetSum < 0:
        return False
    for num in numbers:
        if canSum(targetSum - num, numbers):
            return True
    return false
```

Now with memoization. This is O(m \* n).

```
memo = {}
def canSumMem(targetSum, numbers):
    nonlocal memo
    if targetSum in memo:
        return memo[targetSum]
    if targetSum == 0:
        return True
    if targetSum < 0:
        return False
    for num in numbers:
        if canSumMem(targetSum - num, numbers):
            memo[targetSum] = True
            return True
    memo[targetSum] = False
    return memo[targetSum]
```

Now we can slightly modify the problem to be howSum, which has similar logic, the difference being we want to return the combination of numbers that add to targetSum rather than just returning a boolean. If multiple exist, return one.

Below is the memoized solution only, with runtime O(n \* m^2)

```
memo = {}
def howSumMem(targetSum, numbers):
    nonlocal memo
    if targetSum in memo:
        return memo[targetSum]
    if targetSum == 0:
        return []
    if targetSum < 0:
        return null
    for num in numbers:
        remainder = targetSum - num
        remainderResult = howSum(remaider, numbers)
        if howSum(reamainder, numbers):
            memo[targetSum] = [num] + remainderResult
            return memo[targetSum]
    memo[targetSum] = null
    return memo[targetSum]
```

Finally, we do bestSum, which modifies howSum to only give the shortest valid array. For examples, \[4,4] is shorter than \[5,1,1,1] for target 8.

```
memo = {}
def bestSumMem(targetSum, numbers): 
    nonlocal memo   
    if targetSum in memo:
        return memo[targetSum]
    if targetSum == 0:
        return []
    if targetSum < 0:
        return null
    shortest = null
    for num in numbers:
        remainder = targetSum - num
        remainderResult = bestSum(remainder, numbers)
        if remainderResult:
            combo = [num] + remainderResult
            if shortest == null or len(combo) < len(shortest):
                shortest = combo
    memo[targetSum] = shortest
    return shortest 
            
```
