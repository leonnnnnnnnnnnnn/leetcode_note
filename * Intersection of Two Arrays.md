# Intersection of Two Arrays - LC 349

## Description

Given two arrays, write a function to compute their intersection.

**Example 1:**

```
Input: nums1 = [1,2,2,1], nums2 = [2,2]
Output: [2]
```

**Example 2:**

```
Input: nums1 = [4,9,5], nums2 = [9,4,9,8,4]
Output: [9,4]
```

**Note:**

- Each element in the result must be unique.
- The result can be in any order.

## Solution 1: Set

```python
def solution(nums1, nums2):
    nums1_set = {x for x in nums1}
    rtn = {x for x in nums2 if x in nums1_set}
    return list(rtn)
```

```cpp
#include <vector>
#include <set>

vector<int> intersection(vector<int>& nums1, vector<int>& nums2) {
    set<int> record(nums1.begin(), nums1.end());
    
    set<int> resultSet;
    for(auto iter = nums2.begin(); iter != nums2.end(); iter++)
        if(record.find(*iter) != record.end())
            resultSet.insert(*iter);
    
    return vector<int>(resultSet.begin(), resultSet.end());
}
```

