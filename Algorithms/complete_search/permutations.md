# Permutations

## Introduction
Permutation is used to solve many problems, it solves the problem by creating multiple attachments to find the required solution.

## Recursive method of calculating permutations
```python
permutation = []
chosen = []

def permutations(n):
    if len(permutation) == n:
        print(permutation)
    else:
        for i in range(n):
            if chosen[i]:
                continue
            chosen[i] = True
            permutation.append(i)
            permutations(n)
            chosen[i] = False
            permutation.pop()
```
This code builds the solution by chosing an element and making permutation of all the other elements. Similarly, it creates permutations of other elements recursively. If you get the length of permutation equal to the length of your list, you can process the solution. After processing the solution, you can backtrack by deselecting the element which you've selected above.
