# Two Sum - LC 1

## Description
Given an array of integers, return **indices** of the two numbers such that they add up to a specific target.

You may assume that each input would have **exactly** one solution, and you may not use the *same* element twice.

**Example:**

```
Given nums = [2, 7, 11, 15], target = 9,

Because nums[0] + nums[1] = 2 + 7 = 9,
return [0, 1].
```

## Solution1: 2 for-loop of O(n^2)
```python
def solution(nums, target):
  for i, x in enumerate(nums):
    for i, y in enumerate(nums[i+1:]):
        if x + y == target:
            return [i, i+j+1]
```
Accepted, but not good though... time complexity = O(n^2)

## Solution2: hasp map, O(n)
```python
def solution(nums, target):
  complement = {}
  for i, x in enumerate(nums):
      if x in complement:
        return [i, complement[x]]
      else:
        complement[target -x ] = i
```

```cpp
#include <vector>
#invlude <unordered_map>

vector<int> twoSum(vector<int>& nums, int target) {
    unordered_map<int, int> complement;

    vector<int> res;
    for(int i = 0; i < nums.size(); i++)
        if(complement.find(nums[i]) != complement.end()) {
            res.push_back(complement[nums[i]]);
            res.push_back(i);
            break;
        }
        else 
            complement.insert(pair<int, int>(target - nums[i], i));

    return res;
}
```

