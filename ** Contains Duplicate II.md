# Contains Duplicate II - LC 219

## Description

Given an array of integers and an integer *k*, find out whether there are two distinct indices *i* and *j* in the array such that **nums[i] = nums[j]** and the **absolute** difference between *i* and *j* is at most *k*.

**Example 1:**

```
Input: nums = [1,2,3,1], k = 3
Output: true
```

**Example 2:**

```
Input: nums = [1,0,1,1], k = 1
Output: true
```

**Example 3:**

```
Input: nums = [1,2,3,1,2,3], k = 2
Output: false
```

## Solution 1: Lookup Table + Sliding Window

```cpp
bool containsNearbyDuplicate(vector<int>& nums, int k) {
    unordered_set<int> record;

    for(int i = 0; i < nums.size(); i++) {
        if(record.find(nums[i]) != record.end())
            return true;
        else
            record.insert(nums[i]);

        if(record.size() == k + 1)
            record.erase(nums[i - k]);
    }
    return false;
}
```

$T(n)=O(n)$, operations on *unordered set* is $O(1)$.