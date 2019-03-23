# 4 Sum II

## Description

Given four lists A, B, C, D of integer values, compute how many tuples `(i, j, k, l)` there are such that `A[i] + B[j] + C[k] + D[l]` is zero.

To make problem a bit easier, all A, B, C, D have same length of N where 0 ≤ N ≤ 500. All integers are in the range of -228 to 228 - 1 and the result is guaranteed to be at most 231 - 1.

**Example:**

```
Input:
A = [ 1, 2]
B = [-2,-1]
C = [-1, 2]
D = [ 0, 2]

Output:
2

Explanation:
The two tuples are:
1. (0, 0, 0, 1) -> A[0] + B[0] + C[0] + D[1] = 1 + (-2) + (-1) + 2 = 0
2. (1, 1, 0, 0) -> A[1] + B[1] + C[0] + D[0] = 2 + (-1) + (-1) + 0 = 0
```

## Solution 1: Lookup table

```cpp
int fourSumCount(vector<int>& A, vector<int>& B, vector<int>& C, vector<int>& D) {
    unordered_map<int, int> record;
    for (int i : C)
        for (int j : D)
            record[i + j]++;

    int res = 0;
    for (int k : A)
        for ( int l : B)
            if (record.find(0 - k - l) != record.end())
                res += record[0 - k - l];
    return res;
}
```

$T(n)=O(n^2)$. Although the above solution has time complexity of $n^2$, given the data size, an algo of $n^2$ is totally acceptable.