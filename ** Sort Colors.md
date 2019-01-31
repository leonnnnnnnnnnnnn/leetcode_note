# Sort Colors

## Description

Given an array with *n* objects colored red, white or blue, sort them **in-place** so that objects of the same color are adjacent, with the colors in the order red, white and blue.

Here, we will use the integers 0, 1, and 2 to represent the color red, white, and blue respectively.

**Note:** You are not suppose to use the library's sort function for this problem.

**Example:**

```
Input: [2,0,2,1,1,0]
Output: [0,0,1,1,2,2]
```

## Solution 1: Counting Sort

```cpp
void sortColors(vector<int>& nums) {
        int count[3] = {0}; // count[i]: numbers of color i

        for (int i = 0; i < nums.size(); ++i) {
            assert(nums[i] >= 0 && nums[i] <= 2); // index boundary check
            count[nums[i]]++;
        }

        int index = 0;
        for (int j = 0; j < 3; ++j) {
            for (int i = 0; i < count[j]; ++i)
                nums[index+i] = j;
            index += count[j];
        }
    }
```

Time $O(n)$, Space $O(1)$. But it has to iterate twice.

## Solution 2: QuickSort3Ways

```cpp
void sortColors2(vector<int>& nums) {
        int zero = -1; // nums[0:zero] = 0, empty segment when zero < 0
        int two = nums.size(); // nums[two:n-1] = 2, empty segment when two > n-1

        for (int i = 0; i < two;) {
            if (nums[i] == 1)
                i++;

            else if(nums[i] == 2)
                swap(nums[--two], nums[i]);

            else {// nums[i] == 0
                assert(nums[i] == 0);
                swap(nums[++zero], nums[i++]);
            }
        }
    }
```



