# Maximum Subarray - LC 53

## Description


Given an integer array `nums`, find the contiguous subarray (containing at least one number) which has the largest sum and return its sum.

**Example:**

```
Input: [-2,1,-3,4,-1,2,1,-5,4],
Output: 6
Explanation: [4,-1,2,1] has the largest sum = 6.
```

**Follow up:**

If you have figured out the O(*n*) solution, try coding another solution using the divide and conquer approach, which is more subtle.

## Solution 1: $O(n)$

```cpp
class Solution {
  public:
  	int maxSubArray(vector<int>& nums) {
      int cumSum = 0;
      int maxSum = nums[0];
      
      for(int x : nums) {
        cumSum += x;
        maxSum = max(cumSum, maxSum);
        cumSum = max(cumSum, 0);
      }
      
      return maxSum;
    }
}
```



```python
def solution(nums):
    result = nums[0]
    sum = 0
    for num in nums:
        sum += num
        if sum > result:
            result = sum
        if sum <= 0:
            sum = 0
    return result
```

Another $O(n)$ solution:

```python
def solution(nums):
    prev_sub = max_sub = nums[0]
    for i in range(1, len(nums)):
        prev_sub = nums[i] + max(0, prev_sub)
        max_sub = prev_sub if prev_sub > max_sub else max_sub
    return max_sub
```

## Solution 2: Divide and Conquer

```python
def solution(nums):
    max_sub = temp = nums[0]
    temp_min = min(0, temp)
    for i in range(1, len(nums)):
        temp += nums[i]
        if temp - temp_min > max_sub:
            max_sub = temp - temp_min
        if temp < temp_min:
            temp_min = temp
    return max_sub
```

Define $T(i)=\sum_{x=1}^{i}nums[x]$ , $V(i,j)=T(j)-T(i-1)$, and $T(0)=nums[0]$, where $V(i,j)$ is subarray ending at $j$. For any fixed $j$, $V(i,j)$ is maxized when $T(i-1)$ is minimized. So the maximum subarray ending at $j$ is $V_{max}=T(j)-T_{min}$ where $T_{min}=min(T(0),T(1),\dots T(j-1))$. If we keep track of and update $V_{max}$ and $T_{min}$ as $j$ increases, we have the above algorithm. 