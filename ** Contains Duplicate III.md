# Contains Duplicate III - LC 220

## Description

Given an array of integers, find out whether there are two distinct indices *i* and *j* in the array such that the **absolute** difference between **nums[i]** and **nums[j]** is at most *t* and the **absolute** difference between *i* and *j* is at most *k*.

**Example 1:**

```
Input: nums = [1,2,3,1], k = 3, t = 0
Output: true
```

**Example 2:**

```
Input: nums = [1,0,1,1], k = 1, t = 2
Output: true
```

**Example 3:**

```
Input: nums = [1,5,9,1,5,9], k = 2, t = 3
Output: false
```

## Solution 1: Use ordered set

```cpp
bool containsNearbyDuplicate(vector<int>& nums, int k, int t) {
    set<int> record;

    for(int i = 0; i < nums.size(); i++) {
        if(record.lower_bound(nums[i] - t) != record.end() && *record.lower_bound(nums[i] - t) <= nums[i] + t)
            return true;
        else
            record.insert(nums[i]);

        if(record.size() == k + 1)
            record.erase(nums[i - k]);
    }
    return false;
}
```

$T(n)=O(nlogn)$. Operations on *ordered set* is $O(nlogn)$.