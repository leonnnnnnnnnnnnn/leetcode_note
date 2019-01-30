# Move Zeroes

## Description

Given an array `nums`, write a function to move all `0`'s to the end of it while maintaining the relative order of the non-zero elements.

**Example:**

```
Input: [0,1,0,3,12]
Output: [1,3,12,0,0]
```

**Note**:

1. You must do this **in-place** without making a copy of the array.
2. Minimize the total number of operations.

## Solution 1: Time $O(n)$, Space $O(n)$

```cpp
void moveZeroesV1(vector<int>& nums) {
        vector<int> nonZeroVec;
        for (int i = 0; i < nums.size(); i++)
            if (nums[i])
                nonZeroVec.push_back(nums[i]);

        for (int j = 0; j < nonZeroVec.size(); j++)
            nums[j] = nonZeroVec[j];

        for (int k = nonZeroVec.size(); k < nums.size(); k++)
            nums[k] = 0;
```

## Solution 2: Time $O(n)$, no extra space

```cpp
void moveZeroesV2(vector<int>& nums) {
        int k = 0; // nums[0:k) is nonzero part

        for (int i = 0; i < nums.size(); ++i)
            if (nums[i])
                nums[k++] = nums[i];

        for (int j = k; j < nums.size(); ++j)
            nums[j] = 0;
    }
```

Although it does not need extra space, it still cannot get the work done in only 1 loop

## Solution 3: Solve problem using only 1 loop

```cpp
void moveZeroesV3(vector<int>& nums) {
        int k = 0;

        for (int i = 0; i < nums.size(); ++i)
            if (nums[i])
                swap(nums[k++], nums[i]);
    }
```

It still has many unnecessary swap operations if the array is all if nonzero elements

## Solution 3: Final version

```cpp
void moveZeroesV4(vector<int>& nums) {
        int k = 0;

        for (int i = 0; i < nums.size(); ++i)
            if (nums[i])
                if (k == i)
                    k++;
                else // only perform swap when k != i
                    swap(nums[k++], nums[i]);
    }
```





