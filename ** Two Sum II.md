# Two Sum II

## Description


Given an array of integers that is already **sorted in ascending order**, find two numbers such that they add up to a specific target number.

The function twoSum should return indices of the two numbers such that they add up to the target, where index1 must be less than index2.

**Note:**

- Your returned answers (both index1 and index2) are not zero-based.
- You may assume that each input would have *exactly* one solution and you may not use the *same* element twice.

**Example:**

```
Input: numbers = [2,7,11,15], target = 9
Output: [1,2]
Explanation: The sum of 2 and 7 is 9. Therefore index1 = 1, index2 = 2.
```

## Solution 1: Binary Search

```cpp
#include<vector>

int binarySearch(vector<int> nums, int l, int r, int target) {
        while(l <= r) {
            int mid = l + (r - l) / 2;
            if (nums[mid] == target)
                return mid;
            else if (nums[mid] > target)
                r = mid - 1;

            else // nums[mid < target
                l = mid + 1;
        }
        return -1;
    }

vector<int> twoSum1(vector<int> &numbers, int target) {
        vector<int> ret;
        int size = static_cast<int>(numbers.size());

        for (int i = 0; i < numbers.size(); ++i) {
            int index = binarySearch(numbers, i + 1, size - 1, target - numbers[i]);
            if (index != -1){
                ret.push_back(i + 1);
                ret.push_back(index + 1);
                return ret;
            }
        }
        throw invalid_argument("This input has no solution!");
    }
```

$T(n)=O(nlogn)$

## Solution 2: Two pointers

```cpp
 vector<int> twoSum2(vector<int> &numbers, int target) {
        int i = 0;
        int j = static_cast<int>(numbers.size()) - 1;

        vector<int> ret;

        while(i < j) {
            if (numbers[i] + numbers[j] == target) {
                ret.push_back(i + 1);
                ret.push_back(j + 1);
                return ret;
            }

            else if(numbers[i] + numbers[j] < target)
                i++;

            else // numbers[i] + numbers[j] > target
                j--;
        }
        throw invalid_argument("The input has no solution!");
    }
```

$T(n)=O(n)$

