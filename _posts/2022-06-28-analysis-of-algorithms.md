---
title:  "Analysis of Algorithms"
excerpt: "Algorithmic complexity / Big-O / Asymptotic analysis"

categories:
  - algorithm
tags:
  - [algorithm, asymptotic analysis, asymptotic notations]

permalink: /algorithm/analysis_of_algorithms/

toc: true
toc_sticky: true
 
date: 2022-06-29
last_modified_at: 2022-06-29
---

## Why perform analysis?
* Asymptotic Analysis helps us to grasp the very important concept of efficiency in the code.
* When working with large programs, helps to identify where major slowdowns are likely to cause bottlenecks, and where more attention should be paid to get the 
largest improvements.



## Asymptotic analysis
In asymptotic analysis, we evaluate the performance of an algorithm in terms of `input size`. We calculate, how the time (or space) taken by an algorithm increases with the input size.  

e.g. Compare two search methods in a sorted array.  

constant: tells exactly how long it takes for the given machine to perform the search in seconds.
1. Linear Search (linear order of growth) on a fast computer, constant = 0.2
2. Binary Search (logarithmic order of growth) on a slow computer, constant = 1000

n: input array size  
Linear Search running time in seconds on A: 0.2*n  
Binary Search running time in seconds on B: 1000*log(n)

small n: fast computer may take less time.  
large n: Binary Search will definitely start taking less time compared to the Linear Search.  
Conclusion: Machine dependent `constants` can always be ignored after a certain value of input size.


### Asymptotic analysis is not always perfect  
e.g. Compare two time complexity: 1000nlog(n) and 2nlog(n).  
-> They are `asymptotically` same (order of growth is n*log(n)), therefore we can't judge which one is better as constants are ignored in asymptotic analysis.

asymptotically: 점근적으로 (기존에는 멀리 있어 보이는 결과물이 근삿값에 점점 가까워지고 있는 상태)

---

## Worst, average and best cases
### Worst case analysis (usually done)
Calculate the `upper bound` on the running time of an algorithm (maximum number of operations).  
e.g. linear search: worst case happens when the element to be searched is not present in the array.  
Worst-case time complexity = Θ(n).  

### Average case analysis (sometimes done)
말 그대로 average.

### Best case analysis
Calculate the `lower bound` on the running time of an algorithm (minimum number of operations).  
e.g. linear search: best case happens when the element to be searched is present at the first location.  
Best-case time complexity = Θ(1).  

**Note**: To know the time complexity of an algorithm, we always consider worst case.

---

## Asymptotic notations
<!-- Asymptotic analysis: to have a measure of the efficiency of algorithms that don't depend on machine-specific constants and don't require algorithms to be implemented and time taken by programs to be compared. -->
Asymptotic notations: represent the `time complexity` of algorithms for asymptotic analysis.

1. `Θ notation`: bounds a function from above and below.
   How to get it? -> drop low-order terms and ignore leading constants.

```
Θ(g(n)) = {f(n): there exist positive constants c1, c2 and n0 such 
                 that 0 <= c1*g(n) <= f(n) <= c2*g(n) for all n >= n0 (large values of n)}
```
<!-- 이미지 첨부 -->

2. `Big O notation`: provides asymptotic upper bound of an algorithm.  
e.g. time complexity of insertion sort: O(n^2).  

```
O(g(n)) = { f(n): there exist positive constants c and 
                  n0 such that 0 <= f(n) <= c*g(n) for 
                  all n >= n0}
```

3. `Ω notation`: provides asymptotic lower bound of an algorithm.
   e.g. time complexity of insertion sort can be written as Ω(n).
   Since the best case performance of an algorithm is generally not useful, the omega notation is the least used notation among all three.

```
Ω (g(n)) = {f(n): there exist positive constants c and
                  n0 such that 0 <= c*g(n) <= f(n) for
                  all n >= n0}.
```

---

## Analysis of loops
1. **O(1)**: no loop or recursion, and call to any other non-constant time function.
   e.g.
   * `swap()` function
   * A loop/recursion that runs a constant number of times

2. **O(n)**: Time complexity of a loop. Loop variables are `incremented/decremented` by a constant amount.
   ```cpp
   // c = positive integer constant
   for (int i=1; i<=n; i+=c) {
       // some O(1) expressions
   }

   for (int i=n; i>0; i-=c) {
       // some O(1) expressions
   }
   ```

3. **O(n^c)**: Time complexity of `nested loops` = number of times the innermost statement is executed.  
   e.g. `selection sort` and `insertion sort`.
   ```cpp
   // The following sample loops have O(n^2) time complexity.

   for (int i=1; i<=n; i+=c) {
       for (int j=1; j<=n; j+=c) {
           // some O(1) expressions
       }
   }

   for (int i=n; i>0; i-=c) {
       for (int j=i+1; j<=n; j+=c) {
           // some O(1) expressions
       }
   }
   ```

4. **O(log(n))**: Time complexity of a loop. 
   * Loop variables are `divided/multiplied` by a constant amount.
   * `Recursive call` in recursive function.
   e.g. `binary search`. 
   ```cpp
   for (int i = 1; i <=n; i *= c) {
       // some O(1) expressions
   }
   for (int i = n; i > 0; i /= c) {
       // some O(1) expressions
   }
   ``` 

5. O(log(log(n))): Loop variables are reduced/increased `exponentially` by a constant amount.  
   ```cpp
   // Here c is a constant greater than 1   
   for (int i = 2; i <=n; i = pow(i, c)) { 
       // some O(1) expressions
   }
   //Here fun is sqrt or cuberoot or any other constant root
   for (int i = n; i > 1; i = fun(i)) { 
       // some O(1) expressions
   }
   ```
   Refer to [here](https://www.geeksforgeeks.org/time-complexity-loop-loop-variable-expands-shrinks-exponentially/, "geeksforgeeks link") for mathematical details. 


### How to combine the time complexities of consecutive loops?
Calculate it as a `sum` of time complexities of individual loops.
```
For two consecutive loops with time complexities O(m) and O(m):  
time complexity = O(m+n).
If m==n, time complexity = O(2n) = O(n).
```

### How to calculate the time complexity when there are many if, else statements inside loops?
Consider the `worst-case` time complexity.  
When the code is too complex to consider all if-else cases, we can get an upper bound by ignoring if-else and other complex control statements.

### How to calculate the time complexity of recursive functions?
We must know how to solve recurrences (discussed in next chapter).

### Algorithms cheat sheet
|Algorithm     |Best Case |Average Case|Worst Case|  
|--------------|----------|------------|----------|  
|selection sort|O(n^n)    |O(n^n)      |O(n^n)    |  
|bubble sort   |O(n)      |O(n^n)      |O(n^n)    |  
|insertion sort|O(n)      |O(n^n)      |O(n^n)    |  
|tree sort     |O(nlog(n))|O(nlog(n)   |O(n^n)    |  
|merge sort    |O(nlog(n))|O(nlog(n))  |O(nlog(n))|  
|heap sort     |O(nlog(n))|O(nlog(n))  |O(nlog(n))|  
|quick sort    |O(nlog(n))|O(nlog(n))  |O(n^n)    |  
|bucket sort   |O(n+k)    |O(n+k)      |O(n^n)    |  
|counting sort |O(n+k)    |O(n+k)      |O(n+k)    |  

[Quiz on analysis of algorithms](https://www.geeksforgeeks.org/algorithms-gq/analysis-of-algorithms-gq/)


### Solving recurrences
Recurrence: A recursively defined function over N(natural number).

Three ways of solving recurrences:
1. Substitution method. 
2. Recurrence tree method.
3. Master method:
   Only works for the following type of recurrences or for recurrences that can be transformed into the following type.
   ```
   T(n) = aT(n/b) + f(n) where a >= 1 and b > 1
   ```

   There are following three cases:
   ```
   1. If f(n) = O(n^c) where c < Log_b(a) then T(n) = Θ(n^Log_b(a)) 
   2. If f(n) = Θ(n^c) where c = Log_b(a) then T(n) = Θ((n^c)Log(n)) 
   3. If f(n) = Ω(n^c) where c > Log_b(a) then T(n) = Θ(f(n))
   ```

---

## Amortized analysis