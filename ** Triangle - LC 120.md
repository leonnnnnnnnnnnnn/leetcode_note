# Triangle - LC 120

## Description

Given a triangle, find the minimum path sum from top to bottom. Each step you may move to adjacent numbers on the row below.

For example, given the following triangle

```
[
     [2],
    [3,4],
   [6,5,7],
  [4,1,8,3]
]
```

The minimum path sum from top to bottom is `11` (i.e., **2** + **3** + **5** + **1** = 11).

**Note:**

Bonus point if you are able to do this using only *O*(*n*) extra space, where *n* is the total number of rows in the triangle.

## Solution 1: Dynamic programming

```cpp
 int minimumTotal(vector<vector<int>>& triangle) {
   for(int l = triangle.size() - 2; l >= 0; l--)
     for(int j = 0; j <= l; j++)
       triangle[l][j] += min(triangle[l+1][j], triangle[l+1][j+1]);

   return triangle[0][0];
 }
```

$T(n)=O(n^2)$, $S(n)=O(1)$. Bottom-up DP.

```cpp
int minimumTotal(vector<vector<int>>& triangle) {
  int n = triangle.size();
  for(int l = 1; l < n; l++) {
    triangle[l][0] += triangle[l-1][0];
    triangle[l][l] += triangle[l-1][l-1];
    for(int j = 1; j < l; j++)
      triangle[l][j] += min(triangle[l-1][j-1], triangle[l-1][j]);
  }


  return *min_element(triangle[n-1].begin(), triangle[n-1].end());
}
```

$T(n)=O(n^2)$, $S(n)=O(1)$. Top-down DP.

