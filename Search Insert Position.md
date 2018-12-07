# Search Insert Position

## Description

Given a sorted array and a target value, return the index if the target is found. If not, return the index where it would be if it were inserted in order.

You may assume no duplicates in the array.

**Example 1:**

```
Input: [1,3,5,6], 5
Output: 2
```

**Example 2:**

```
Input: [1,3,5,6], 2
Output: 1
```

**Example 3:**

```
Input: [1,3,5,6], 7
Output: 4
```

**Example 4:**

```
Input: [1,3,5,6], 0
Output: 0
```

## Solution 1

```python
def solution(nums, target):
    ind = -1
    for i, x in enumerate(nums):
        if x == target:
            return i
        elif x < target:
            ind = i
        else:
            return ind + 1
    return len(nums)
```

Actually, there is no need to check if target is in nums, just find the element which is greater than or equal to target and return its index.

## Solution 2

```python
def solution(nums, target):
    for i, x in enumerate(nums):
        if x >= target:
            return i
    return len(nums)
```

