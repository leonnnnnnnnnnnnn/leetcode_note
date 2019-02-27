# Remove Duplicates from Sorted Array II - LC 80

## Description

Given a sorted array *nums*, remove the duplicates [**in-place**](https://en.wikipedia.org/wiki/In-place_algorithm) such that duplicates appeared at most *twice* and return the new length.

Do not allocate extra space for another array, you must do this by **modifying the input array in-place**with O(1) extra memory.

**Example 1:**

```
Given nums = [1,1,1,2,2,3],

Your function should return length = 5, with the first five elements of nums being 1, 1, 2, 2 and 3 respectively.

It doesn't matter what you leave beyond the returned length.
```

**Example 2:**

```
Given nums = [0,0,1,1,1,1,2,3,3],

Your function should return length = 7, with the first seven elements of nums being modified to 0, 0, 1, 1, 2, 3 and 3 respectively.

It doesn't matter what values are set beyond the returned length.
```

## Solution 1: Two pointers

```cpp
int removeDuplicates(vector<int>& nums) {
    if (nums.empty())
        return 0;
    
    if (nums.size() <= 2)
        return nums.size();
    
    int k = 0;
    for (int j = 2; j < nums.size(); j++) {
        if (nums[j] != nums[k])
            if (k + 2 != j)
                nums[k+2] = nums[j]; // or swap(nums[k+2], nums[j])
        	k++;
    }
    
    return k+2;
}
```

