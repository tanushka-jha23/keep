# Subsets

> advice: Trust on your code.

## Introduction

In mathematics, subsets are the possible combinations of a set. Complete search algorithms uses subsets to solve many problems.

The basic method of solving a problem through subset is-:
1) Calculate all possible subsets of a problem.
2) Process the subsets as per the requirement of your question.

## Recursive method of subsets
```python
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


## Bitwise method of subsets
```python
s = [1, 4, 3, 2]
for i in range(2 ** len(s)):
    filter = [i&1, (i&2)>>1, (i%4)>>2, (i%8)>>3]
    print([s[i] for i, x in enumerate(filter) if x])
```

To make subsets of an array, bitwise operation can be used. To get familiar with the process take an array of 4 elements. Create an array with the name *filter* and create all the 4 bit combinations by performing bitwise AND operation of numbers from (0 to $2^n$) with increasing powers of 2. Now, if you do bitwise AND operation of 2 with 1, 2, 4 and 8 respectively, it will give $0010$. *>>* is used to shift 1 to the right(right-shift) by one place, to get the *filter* array with all elements as binary.
Check whether the element of filter is 1 or 0, if it is 1 then it the element with corresponding index in *s* will be included to get a subset.


## Time complexity of complete search using subsets

The lower bound of complete search using subsets is $2^n$ as there are total $2^n$ subsets if the length of the set is *n*. This time complexity is of non polynomial type, to reduce the average case time complexity of complete search we use various methods like search pruning.











