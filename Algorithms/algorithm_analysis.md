# Analysis of algorithm

## Introduction to algorithms

The step-by-step procedure of solving any problem is called *algorithm*. If you know about RAM model of computation then algorithms can be explained as the sequence of operations of RAM model.
There are many ways to solve a problem, but here comes to question.
How to analyse that which solution is better?

You can analyse the algorithm in many ways but the two most common and important factors which are generally used to analyse any algorithm are
1) Time complexity.
2) Space complexity.

## Time complexity

Computers can have different hardware or code can be written in different programming languages. Since time is dependent on such factors, it is not a reliable factor to analyse algorithms. 

*Time Complexity* can be used for analysis. Time complexity shows that how the time increases with respect to the input size.
We will represent Time complexity by *T(n)*.
Let's take an example of insertion sort to understand time complexity.

### Insertion Sort 

Pseuodocode of insertion sort is written below. Pseudocodes are way of writing algorithms using a combination of natural languages and programming language like structures.
```
i ← 1
while i < length(A)
    j ← i
    while j > 0 and A[j-1] > A[j]
        swap A[j] and A[j-1]
        j ← j - 1
    end while
    i ← i + 1
end while
```

> $T(n) = c1 + c2n + c3n + c4n\sum_i t_i + c5n\sum_i t_i + c6n\sum_i t_i + c7n$


### Understanding the equation for time complexity of insertion sort

- In RAM model of computation, you've seen that each operation takes some time to be executed. In the above pseudocode, `c1, c2, c3,..., c7` are respective times taken by each line of code to run only once.
c1 is the time to load 1 in i
c2 is the time for checking `i < length(A)` and similarly c3, c4,..., c7 are times for single execution of respetive lines.

- *n* is the size of input. Since, line 2 to line 6 are written inside `for` loop and loop is executing *n-1* times. That's why we've multiplied line 2 to line 6 by *n*.
Line 2 to line 6 are -:

```while i < length(A)
    j ← i
    while j > 0 and A[j-1] > A[j]
        swap A[j] and A[j-1]
        j ← j - 1
    end while
    i ← i + 1
```
- Line 4, line 5 and line 6 will be executed when the condition inside the inner `while` loop i.e. `j > 0 and A[j-1] > A[j]` will be true.

*This way the total time taken by the insertion sort as a function of input size can be written.*

There are number of possible cases of sorting.
1) *Best Case* 
If array is already sorted, equation of time complexity will be
> $T(n) = c1 + c2n + c3n + c7n$

The terms $c4n\sum_i t_i + c5n\sum_i t_i + c6n\sum_i t_i$ are not present in the above equation because if the array is already sorted then condition of inner loop will not be satisfied and inner loop will not run.

2) *Worst case* 
If array is reversed, then
>$T(n) = c_1 + c_2n + c_3n + c_4n(n-1)+ c_5n(n-1) + c_6n(n-1) + c_7n$
This equation can be simplified as 
>$T(n) = (c_4 + c_5 + c_6)n^2 + (c_2 + c_3 - c_4 - c_5 - c_6 + c_7)n + c_1$

## Bounds of Time complexity or Asymptotic analysis

To deal with different cases of an algorithm, bounds are taken into account.
There are 3 bounds of algorithm

1) *Lower bound* ($\omega(f(n))$)
It is a set of all the functions whose value multiplied by some constant *$c_0$* are more than *f(n)* after some *$n_0$*. Then f(n) is called the lower bound.

2) *Upper bound* (O(f(n)))
It is a set of all the functions whose value mutliplied by some constant *$c_0$* are less than *f(n)* after some *$ n_0$*. Then f(n) is called the upper bound.
    
3) *Tight bound* ($\theta(f(n))$)
It is a set of functions whose value multiplied by some constant *$c_0$* are less than *f(n)* and value of them multiplied by another constant *$c_1$* are more than *f(n)*. Then f(n) is called the tight bound.


## Analysing time complexity of Insertion sort

Lower bound of Insertion sort is O(n)
Upper bound is $\omega(n^2)$
Tight bound of insertion sort does not exist because lower bound and upper bound have different degree.















 
 









