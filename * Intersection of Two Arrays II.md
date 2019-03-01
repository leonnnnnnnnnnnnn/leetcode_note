# Intersection of Two Arrays II - LC 350

## Description

Given two arrays, write a function to compute their intersection.

**Example 1:**

```
Input: nums1 = [1,2,2,1], nums2 = [2,2]
Output: [2,2]
```

**Example 2:**

```
Input: nums1 = [4,9,5], nums2 = [9,4,9,8,4]
Output: [4,9]
```

**Note:**

- Each element in the result should appear as many times as it shows in both arrays.
- The result can be in any order.

## Solution 1: Map

```python
def solution(nums1, nums2):
    rtn = []
    nums1_set = {}
    for x in nums1:
        nums1_set[x] = nums1_set.get(x, 0) + 1
    for x in nums2:
        if x in nums1_set:
            rtn.append(x)
            nums1_set[x] = nums1_set.get(x) - 1
            if nums1_set[x] == 0:
                nums1_set.pop(x)
    return rtn
```

```cpp
#include <vector>
#include <map>

vector<int> intersect(vector<int>& nums1, vector<int>& nums2) {
    map<int, int> freq_nums1;

    for(const auto& num : nums1)
        freq_nums1[num]++; // lookup operation of O(logn)

    vector<int> res;
    for(auto iter = nums2.begin(); iter != nums2.end(); iter++) {
        if(freq_nums1[*iter] != 0) {
            res.push_back(*iter);
            freq_nums1[*iter]--;
        }
    }
    return res;
}
```

$T(n)=O(nlogn)$, the $logn$ comes from the lookup operation of map which is implemented by a balanced binary search tree. If *unordered_map* is used, $T(n)=O(n)$, because now the lookup operation takes $O(1)$ time.