# Unique Paths - LC 62

## Description

A robot is located at the top-left corner of a *m* x *n* grid (marked 'Start' in the diagram below).

The robot can only move either down or right at any point in time. The robot is trying to reach the bottom-right corner of the grid (marked 'Finish' in the diagram below).

How many possible unique paths are there?

![question_52](/Users/apple/myProjects/leetcode_note/image/question_52.png)

**Example:**

```
Input: m = 7, n = 3
Output: 28
```

## Solution 1: Dynamic Programming

```cpp
int uniquePaths(int m, int n) {
    if(m == 1 || n == 1)
        return 1;

    int memo[n][m];

    for(int i = n-2; i >= 0; i--)
        memo[i][m-1] = 1;
    for(int j = m-2; j >= 0; j--)
        memo[n-1][j] = 1;

    for(int i = n-2; i >= 0; i--)
        for(int j = m-2; j >= 0; j--)
            memo[i][j] = memo[i][j+1] + memo[i+1][j];

    return memo[0][0];
}
```

$T(n)=O(m*n), S(n)=O(m*n)$.