# Partition Equal Subset Sum - LC 416

## Description

Given a **non-empty** array containing **only positive integers**, find if the array can be partitioned into two subsets such that the sum of elements in both subsets is equal.

**Note:**

1. Each of the array element will not exceed 100.
2. The array size will not exceed 200.

 

**Example 1:**

```
Input: [1, 5, 11, 5]

Output: true

Explanation: The array can be partitioned as [1, 5, 5] and [11].
```

 

**Example 2:**

```
Input: [1, 2, 3, 5]

Output: false

Explanation: The array cannot be partitioned into equal sum subsets.
```

## Solution 1: Memorization

```cpp
class Solution {
private:
    // memo[i,C] means if it can fill a knapsack with capacity of C
    // memo[i,C] = -1 means it hasn`t been calculated
    // memo[i,C] = 0 means it cannot fill the knapsack with nums[0,i]
    // memo[i,C] = 1 means it can fill the knapsack with nums[0,i]
    vector<vector<int>> memo;
    
    // check if there exists a subset in nums[0:index] of which the sum equals the target sum
    bool tryPartition(const vector<int>& nums, int index, int sum) {
        if(sum == 0)
            return true;
        
        if(sum < 0 || index < 0)
            return false;
        
        if(memo[index][sum] != -1)
            return memo[index][sum] == 1;
        
        memo[index][sum] =  (tryPartition(nums, index-1, sum) || 
                tryPartition(nums, index-1, sum-nums[index])) ? 1 : 0;
        
        return memo[index][sum] == 1;
    }
    
public:
    bool canPartition(vector<int>& nums) {
        int sum = 0;
        for(int x : nums)
            sum += x;
        
        if(sum % 2 != 0)
            return false;
        
        memo = vector<vector<int>>(nums.size(), vector<int>(sum/2 + 1, -1));
        
        return tryPartition(nums, nums.size() - 1, sum/2);
    }
};
```



## Solution 2: Dynamic Programming

```cpp
class Solution {
public:
    bool canPartition(vector<int>& nums) {
        int sum = 0;
        for(int x : nums)
            sum += x;
        
        if(sum % 2 != 0)
            return false;
        
        int n = nums.size();
        int c = sum/2;
        
        vector<bool> memo(c + 1, false);
        
        for(int j = c; j >= nums[0]; j--)
            memo[j] = (nums[0] == j ? true : false);
        
        for(int i = 1; i < n; i++)
            for(int j = c; j >= nums[i]; j--)
                memo[j] = (memo[j] || memo[j - nums[i]]);
        
        return memo[c];
    }
};
```

