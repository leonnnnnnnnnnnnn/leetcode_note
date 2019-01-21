# Reverse Pairs - Hard

## Description

Given an array `nums`, we call `(i, j)` an **important reverse pair** if `i < j` and `nums[i] > 2*nums[j]`.

You need to return the number of important reverse pairs in the given array.

**Example1:**

```
Input: [1,3,2,3,1]
Output: 2
```



**Example2:**

```
Input: [2,4,3,5,1]
Output: 3
```



**Note:**

1. The length of the given array will not exceed `50,000`.
2. All the numbers in the input array are in the range of 32-bit integer.

## Solution 1: Merge Sort

```python
def _count_reverse_pairs(arr, l, r):
    if l >= r:
        return 0

    count = 0
    mid = int((l + r) / 2)

    count += _count_reverse_pairs(arr, l, mid)
    count += _count_reverse_pairs(arr, mid+1, r)

    j, k = l, mid + 1
    while j <= mid and k <= r:
        if arr[j] > 2 * arr[k]:
            count += mid - j + 1
            k += 1
        else:
            j += 1

    arr[l:r+1] = sorted(arr[l:r+1])

    return count


def reverse_pairs(nums):
    if not nums:
        return 0
    res = _count_reverse_pairs(nums, 0, len(nums)-1)
    return res
```

$T(n)=O(nlogn)​$ 