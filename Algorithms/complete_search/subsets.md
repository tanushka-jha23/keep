# Subsets

> advice: Trust on your code.

## Introduction

In mathematics, subsets are the possible combinations of a set. Complete search algorithms uses subsets to solve many problems.

The basic method of solving a problem through subset is-:
1) Calculate all possible subsets of a problem.
2) Process the subsets as per the requirement of your question.

## Code
```
s = []

def subset(k, n):
    if k == n:
        print(s)
    
    else:
        s.append(k)
        subset(k + 1, n)
        s.pop()
        subset(k + 1, n)

// if n = 2, subsets will be [0, 1, 2], [0, 1], [0, 2], [0], [1, 2], [1], [2], []
```

- This is a recursive way of creating subsets.
- In the above code, firstly an empty array *s* is created. A function *subset* takes two arguments, *k* and *n* and process the array if value of k and n are equal.
- If there values are not equal, k will be pushed in s and subset function is called with arguments *k+1* and *n*.This step will create all the subsets with *k* included.
- Then 'k' will be popped out and subset is called again with *k+1* and *n*. This step will create the same subsets but this time without including *k*.


## Time complexity of complete search using subsets

The lower bound of complete search using subsets is $2^n$ as there are total $2^n$ subsets if the length of the set is *n*. This time complexity is of non polynomial type, to reduce the average case time complexity of complete search we use various methods like search pruning.











