# Introduction

Generalised complete search uses an idea of solving problems, an idea of *building a solution* followed by *backtracking* and finally *processing* the correct solution.

Any problem related to programming can be solved by using the idea of generalised complete search. Whereas, subsets and permutation are two application of complete search. Both the problems of calculating subsets and permutations can be solved by using complete search. Furthermore, subsets and permutations can be used to solve another problems.

Let's say, if the generalised idea of complete search is an electron and subsets and permutation are smaller elements like Hydrogen.
Now, if you want to solve a larger problem (take it as equivalent to making Uranium), you can make uranium with the help of electrons but you can make it with the help of hydrogen also.
This example justifies the above statement.

To understand this method, let's break down these steps and understand them separately.

## Code that calculates the number of paths to reach the final position from the initial position
```
n = 5
path = [[False] * n for _ in range(n)]
path[0][0] = True

def is_valid_path(x1, y1):
    return x1 >= 0 and x1 < n and y1 >= 0 and y1 < n \
        and not path[x1][y1]

def all_covered():
    return all([all(path[i]) for i in range(n)])

count = 0
def searchpaths(x, y):
    global count
    if(x == n - 1 and y == n - 1):
        if(all_covered()):
            count += 1
        return
            
    directions = [(x, y-1), (x, y+1), (x-1, y), (x+1, y)]
    for x1, y1 in directions:
        if not is_valid_path(x1, y1):
            continue
        path[x1][y1] = True
        searchpaths(x1, y1)
        path[x1][y1] = False

```

This function `searchpaths` calculates the number of paths from initial position (0, 0) to final position (4, 4).
To build the solution of this problem, it searches for all the possible directions. Here, `path` is used to keep the track of visited coordinates. Whenever we jump on a new coordinate, make the index of that equal to True and after calling `searchpaths` make it equal to False again. When you make it False, you're actually backtracking and finding the new path. 

Now, there are two cases either the solution is complete (i.e. all the coordinates are visited). In this case you can process it as a solution. In another case the solution may be incomplete, now you can backtrack and find the complete solution.

This way, you can find the number of paths without using subsets or permutations but by directly using the idea of generalised complete search.
