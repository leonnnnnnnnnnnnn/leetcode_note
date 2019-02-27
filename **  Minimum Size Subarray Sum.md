#  Minimum Size Subarray Sum - LC 209

## Description

Given an array of **n** positive integers and a positive integer **s**, find the minimal length of a **contiguous** subarray of which the sum ≥ **s**. If there isn't one, return 0 instead.

**Example:** 

```
Input: s = 7, nums = [2,3,1,2,4,3]
Output: 2
Explanation: the subarray [4,3] has the minimal length under the problem constraint.
```

## Solution 1: Moving Window

```cpp
int minSubArrayLen1(int s, vector<int>& nums) {
    int l = 0;
    int ret = INT_MAX;
    int sum = 0;

    for(int r = 0; r < nums.size(); r++) {
        sum += nums[r];
        while(sum >= s) {
            ret = min(ret, r - l + 1);
            sum -= nums[l++];
        }
    }

    return (ret != INT_MAX) ? ret : 0;
}

int minSubArrayLen2(int s, vector<int>& nums) {
    int i = 0, j = -1; // nums[i:j] is the moving window
    int sum = 0;
    int ret = INT_MAX; // since the max value ret can take is nums.size(), the initial value should be greater the maximum

    while(i < nums.size()) {
        if(sum < s && j + 1 < nums.size())
            sum += nums[++j];
        else
            sum -= nums[i++];

        if(sum >= s)
            ret = (j - i + 1) < ret ? j - i + 1 : ret;
    }

    return (ret != INT_MAX) ? ret : 0;
}
```

$T(n)=O(n)$

