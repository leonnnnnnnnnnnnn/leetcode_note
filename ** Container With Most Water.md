# Container With Most Water - LC 11

## Description

Given *n* non-negative integers *a1*, *a2*, ..., *an* , where each represents a point at coordinate (*i*, *ai*). *n*vertical lines are drawn such that the two endpoints of line *i* is at (*i*, *ai*) and (*i*, 0). Find two lines, which together with x-axis forms a container, such that the container contains the most water.

**Note:** You may not slant the container and *n* is at least 2.

![](./image/question_11.jpg)

The above vertical lines are represented by array [1,8,6,2,5,4,8,3,7]. In this case, the max area of water (blue section) the container can contain is 49.

## Solution 1: Two pointers

```cpp
int maxArea(vector<int>& height) {
        int i = 0, j = static_cast<int>(height.size()) - 1;
        int maxArea = 0;

        while(i < j) {
            int area = (j - i) * min(height[i], height[j]);
            maxArea = area > maxArea ? area : maxArea;

            if(height[i] < height[j])
                i++;
            else // height[i] >= height[j]
                j--;
        }

        return maxArea;
    }
```

*The area is determined by the line of shorter length.* If we try to move the pointer at the longer line inwards, we won't gain any increase in area, since it is limited by the shorter line. But moving the shorter line's pointer could turn out to be beneficial, as per the same argument, despite the reduction in the width. 

$T(n)=O(n)$

