# Integer Break - LC 343

## Description

Given a positive integer *n*, break it into the sum of **at least** two positive integers and maximize the product of those integers. Return the maximum product you can get.

**Example 1:**

```
Input: 2
Output: 1
Explanation: 2 = 1 + 1, 1 × 1 = 1.
```

**Example 2:**

```
Input: 10
Output: 36
Explanation: 10 = 3 + 3 + 4, 3 × 3 × 4 = 36.
```

**Note**: You may assume that *n* is not less than 2 and not larger than 58.

## Solution 1: Recursion + Memorization

```cpp
class Solution {
private:
    vector<int> memo;
    
    int max3(int a, int b, int c) {
        return max(a, max(b, c));
    }
    
    int breakInteger(int n) {
        if(n == 1)
            return 1;
        if(memo[n] != -1)
            return memo[n];
        
        int res = -1;
        for(int i = 1; i <= n-1; i++) {
            res = max3(res, i*(n-i), i*breakInteger(n-i));
        }
        memo[n] = res;
        return res;
    }
    
public:
    int integerBreak(int n) {
        memo = vector<int>(n+1, -1);
        return breakInteger(n);
    }
};
```

## Solution 2: Dynamic Programming

```cpp
class Solution {
private:
    int max3(int a, int b, int c) {
        return max(a, max(b, c));
    }
    
public:
    int integerBreak(int n) {
        if(n == 1)
            return 1;
        
        vector<int> memo(n+1, -1);
        memo[1] = 1;
        for(int i = 2; i <= n; i++)
            for(int j = 1; j <= i-1; j++)
                memo[i] = max3(memo[i], j*(i-j), j*memo[i-j]);
        
        return memo[n];        
    }
};
```

$T(n)=O(n^2)$.