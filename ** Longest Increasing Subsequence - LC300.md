# Longest Increasing Subsequence - LC300

## Description

Given an unsorted array of integers, find the length of longest increasing subsequence.

**Example:**

```
Input: [10,9,2,5,3,7,101,18]
Output: 4 
Explanation: The longest increasing subsequence is [2,3,7,101], therefore the length is 4. 
```

**Note:** 

- There may be more than one LIS combination, it is only necessary for you to return the length.
- Your algorithm should run in O(*n2*) complexity.

**Follow up:** Could you improve it to O(*n* log *n*) time complexity?



## Solution 1: Dynamic Programming

```cpp
class Solution {
public:
    int lengthOfLIS(vector<int>& nums) {
        int n = nums.size();
        
        if(n == 0)
            return 0;
        
        // memo[i] stands for the length of the LIS which ends with nums[i]
        vector<int> memo(n, 1);
        
        for(int i = 1; i < n; i++){
            for(int j = 0; j < i; j++)
                memo[i] = (nums[j] < nums[i] ? max(memo[i], memo[j] + 1) : memo[i]);
        }
        
        int rtn = memo[0];
        for(int i = 1; i < n; i++)
            rtn = max(rtn, memo[i]);
        
        return rtn;
    }
};
```

Time complexity: O(n^2)

