# Analysis of algorithms

## Introduction to algorithms

The step-by-step procedure of solving any problem is called *algorithm*. If you know about RAM model of computation then algorithms can be explained as the sequence of operations of RAM model.
There are many ways to solve a problem, but here comes to question.
How to compare these solutions?

You can analyse algorithms in many ways but the two most common and important factors which are generally used to analyse any algorithm are
1) Time complexity.
2) Space complexity.

## Time complexity

Computers can have different hardware or people can use different programming languages to write their code. If you run your code in different computers there are chances that the same code will take different runtimes due to their different hardware. Since time depends on such factors, it can not be used to compare any two algorithms.

Instead of time you can use *Time Complexity*. Time complexity is the measure of increase in run time of the algorithm with respect to the input size.
Time complexity can be represented as *T(n)*
Let's take an example of insertion sort to understand it.

### Insertion Sort

Insertion sort is a sorting algorithm. Pseuodocode of insertion sort is written below. Pseuodocodes are basically the way of writing any algorithm by using a combination of natural language and code like structure.

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

To calculate the time complexity of this algorithm, you can consider RAM model of computation. Add the time taken by each operation to get the total time as the function of input size.

> $T(n) = c1 + c2n+ c3(n-1) + c4\sum_{i=1}^{n} + c5\sum_{i=1}^{n} - n + c6\sum_{i=1}^{n} - n + c7(n-1)$ 

1) `i <- 1` is a load operation, it takes some constant time *c1* to be executed.
2) `while i < length(A)` is a loop, it takes time *c2* to run for a single time, but throughout the algorithm is is running *n*(input size) times. Therefore the total runT time of this algorithm will be *c2n*.
3) `j<-i` is again a load operation, it takes some time *c3* for single execution, but it will run *n-1* times throughout the complete algorithm. Why *(n-1)*?
When you check the condition for `i = length(A)`, it will return *false* and hence inner loop will run only *n-1* times.
4) For each $i^th$ iteration of the outer while loop, inner while loop will run $t_i$ times. Therefore, for n iterations of while loop the inner loop will run $\sum_{i=1}^{n} t_i$ times.
5) For each $i^th$ iteration of the outer loop `swap A[j] and A[j-1]` will run $t_i-1$ times. Therefore for *n* iterations of outer loop *swap* will run $\sum_{i=1}^{n} t_i - n$ times.
6) Similarly, `j<-j-1` will run $\sum_{i=1}^{n} t_i -n$ times.
7) `i<-i+1` will take *c7(n-1)* time to run.

*This way the total time taken by the insertion sort as a function of input size can be written.*

Now, there are number of possible cases of sorting.

1) *Best Case* 
If array is already sorted, inner while loop will not run and therefore $\sum_{i=1}^{n}$ will become *0*. Then the equation for time complexity will be
> $T(n) = c_1 + c_2n + c_3(n-1) - c_5n - c_6n + c_7(n-1)$

2) *Worst case* 
If array is reversed, then for 1st iteration of outer while loop the inner while loop will run *(n-1)* times, for the 2nd iteration it will run *(n-2)* times and so on.
Therefore $\sum_{i=1}^{n}$ will become (n-1)+(n-2) +(n-3)+...+1. The result of this sum will be $\frac{n(n-1)}{2}$.
If you simplify the whole equation by putting this value in place of $\sum_{i=1}^{n} t_i$. You'll get,
$n^2(\frac{c4}{2}+\frac{c5}{2}+\frac{c6}{2}) - n(\frac{c4n}{2}+\frac{3c5n}{2}+\frac{3c7n}{2}-c7-c3-c2) + (c1-c3-c7)$.


## Bounds of Time complexity

To deal with different cases of an algorithm, different bounds are considered,

1) *Lower bound* 
$\Omega(f(n))$
A set of all the functions whose value multiplied by some constant *$c_0$* are more than *f(n)* after some *$n_0$*. Then f(n) is called the lower bound.

2) *Upper bound* O(f(n))
A set of all the functions whose value mutliplied by some constant *$c_0$* are less than *f(n)* after some *$ n_0$*. Then f(n) is called the upper bound.
    
3) *Tight bound* 
$\theta(f(n))$
It is a set of functions whose value multiplied by some constant *$c_0$* are less than *f(n)* and value of them multiplied by another constant *$c_1$* are more than *f(n)*. Then f(n) is called the tight bound.


## Analysing time complexity of Insertion sort

- To find the upper bound of insertion sort consider the worst case, then find a function which is always less than *T(n)* after some $n_0$.
Since, *T(n)* of insertion sort has a term of $n^2$ therefore the closest upper bound will be *O($n^2$)*. If you draw a graph for $n^2$ and a graph for T(n)*c (c is some multiplier to make it less than n^2), you'll observe that graph of $n^2$ will always be greater than T(n)*c.

- Similarly, to find the lower bound of insertion sort, you need to consider the best case. The equation for best case of the algorithm contains terms of *n*. If you multiply some constant *c* with T(n) and plot its graph you'll observe that the graph will always be less than the graph of *n*.
Therefore, the lower bound for insertion sort will be $\omega$.

- Tight bound of insertion sort does not exist because the degree of lower bound and upper bound is different in this case. Don't worry! later in merge sort you'll get to know about tight bound.


