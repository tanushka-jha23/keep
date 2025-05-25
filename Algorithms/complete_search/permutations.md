# Permutations

## Introduction
Permutation is used to solve many problems, it solves the problem by creating multiple permuatations to find the required solution.

## Recursive method of calculating permutations
```
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
