# House Robber - LC 198

## Description

You are a professional robber planning to rob houses along a street. Each house has a certain amount of money stashed, the only constraint stopping you from robbing each of them is that adjacent houses have security system connected and **it will automatically contact the police if two adjacent houses were broken into on the same night**.

Given a list of non-negative integers representing the amount of money of each house, determine the maximum amount of money you can rob tonight **without alerting the police**.

**Example 1:**

```
Input: [1,2,3,1]
Output: 4
Explanation: Rob house 1 (money = 1) and then rob house 3 (money = 3).
             Total amount you can rob = 1 + 3 = 4.
```

**Example 2:**

```
Input: [2,7,9,3,1]
Output: 12
Explanation: Rob house 1 (money = 2), rob house 3 (money = 9) and rob house 5 (money = 1).
             Total amount you can rob = 2 + 9 + 1 = 12.
```

## Solution 1： Recursion + Memorization

```cpp
class Solution {
private:
    vector<int> memo;
		// consider rob from house[index,...,n-1]
    int tryRob(vector<int>& nums, int index) {
        if(index >= nums.size())
            return 0;

        if(memo[index] != -1)
            return memo[index];

        int res = 0;
        for(int i = index; i < nums.size(); i++)
            res = max(res, nums[i] + tryRob(nums, i+2));
        memo[index] = res;
        return res;
    }

public:
    int rob(vector<int>& nums) {
        memo = vector<int>(nums.size(), -1);
        return tryRob(nums, 0);
    }
};
```

$T(n)=O(n), S(n)=O(n)$



## Solution 2: Dynamic programming

- **State: maximum money can get if consider robbing from [x, …, n-1]**

- **State transition function:**

  $f(x) = max(nums[x]+f(x+2), nums[x+1]+f(x+3)+\dots+nums[n-3]+f(n-1), nums[n-2], nums[n-1])$

- **Initial state:**

  $f(n-1)=nums[n-1]$

```cpp
class Solution {
public:
    // Dynamic programming
    int rob(vector<int>& nums) {
        int n = nums.size();
        if(n == 0)
            return 0;
        
        vector<int> memo(n, -1);
        memo[n-1] = nums[n-1];
        
        for(int i = n-2; i >= 0; i--)
            for(int j = i; j < n; j++)
                memo[i] = max(memo[i], nums[j]+(j + 2 > n-1 ? 0 : memo[j+2]));
        
        return memo[0];
    }
};
```

$T(n)=O(n^2), S(n)=O(n)$



***Another implementation***

- **State: maximum money can get if consider robbing from [0, …, x]**

- **State transition function:**

  $f(x) = max(nums[x]+f(x-2), nums[x-1]+f(x-3)+\dots+nums[2]+f(0), nums[1], nums[0])$

- **Initial state:**

  $f(0)=nums[0]$

```cpp
class Solution {
public:
    // Dynamic programming
    int rob(vector<int>& nums) {
        int n = nums.size();
        if(n == 0)
            return 0;
        
        vector<int> memo(n, -1);
        memo[0] = nums[0];
        
        for(int i = 1; i < n; i++)
            for(int j = i; j >= 0; j--)
                memo[i] = max(memo[i], nums[j] + (j - 2 < 0 ? 0 : memo[j-2]));
        
        return memo[n-1];
    }
};
```



## Solution 3: $O(n)$ Dynamic programming

```cpp
class Solution {
public:
    // Dynamic programming
    int rob(vector<int>& nums) {
        int n = nums.size();
        if(n == 0)
            return 0;
        
        vector<int> memo(n, -1);
        memo[n-1] = nums[n-1];
        
        for(int i = n-2; i >= 0; i--)
            memo[i] = max(memo[i+1], nums[i]+(i + 2 > n-1 ? 0 : memo[i+2]));
        
        return memo[n-1];
    }
};
```

```cpp
class Solution {
public:
    // Dynamic programming
    int rob(vector<int>& nums) {
        int n = nums.size();
        if(n == 0)
            return 0;
        
        vector<int> memo(n, -1);
        memo[0] = nums[0];
        
        for(int i = 1; i < n; i++)
            memo[i] = max(memo[i-1], nums[i]+(i - 2 < 0 ? 0 : memo[i-2]));
        
        return memo[n-1];
    }
};
```







