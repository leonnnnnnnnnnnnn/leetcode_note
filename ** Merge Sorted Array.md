# Merge Sorted Array - LC 88

## Description

Given two sorted integer arrays *nums1* and *nums2*, merge *nums2* into *nums1* as one sorted array.

**Note:**

- The number of elements initialized in *nums1* and *nums2* are *m* and *n* respectively.
- You may assume that *nums1* has enough space (size that is greater or equal to *m* + *n*) to hold additional elements from *nums2*.

**Example:**

```
Input:
nums1 = [1,2,3,0,0,0], m = 3
nums2 = [2,5,6],       n = 3

Output: [1,2,2,3,5,6]
```

## Solution 1: Merge Sort

```cpp
void merge(vector<int>& nums1, int m, vector<int>& nums2, int n) {
    vector<int> aux;
    for (int i = 0; i < m; i++)
        aux.push_back(nums1[i]);

    int j = 0, k = 0;
    for (int i = 0; i < m + n; i++) {
        if (j < m && k < n) {
            if (aux[j] < nums2[k])
                nums1[i] = aux[j++];
            else
                nums1[i] = nums2[k++];
        }

        else if( j >= m)
            nums1[i] = nums2[k++];
        else // k >= n
            nums1[i] = aux[j++];
    }
}
```

Time $O(2m+n)$, Space $O(m)$. Need extrad space to store nums1.

## Solution 2: Merge Sort Enhanced

```cpp
void merge(vector<int>& nums1, int m, vector<int>& nums2, int n) {
    int lastIndex = m + n -1;

    while (m > 0 && n >0) {
        if (nums1[m-1] > nums2[n-1])
            nums1[lastIndex--] = nums1[--m];
        else
            nums1[lastIndex--] = nums2[--n];
    }

    while (m > 0) {
        nums1[lastIndex--] = nums1[--m];
    }

    while (n > 0) {
        nums1[lastIndex--] = nums2[--n];
    }
}
```

Take advantage of nums1`s space. Select the larger element first. Time $O(m+n)$, space $O(1)$.