# Kth Largest Element in an Array

## Description

Find the **k**th largest element in an unsorted array. Note that it is the kth largest element in the sorted order, not the kth distinct element.

**Example 1:**

```
Input: [3,2,1,5,6,4] and k = 2
Output: 5
```

**Example 2:**

```
Input: [3,2,3,1,2,4,5,5,6] and k = 4
Output: 4
```

**Note:** 
You may assume k is always valid, 1 ≤ k ≤ array's length.

## Solution 1: Quick Sort

```c++
#include <cassert>
#include <time.h>

template <typename T>
int __partition(T arr[], int l, int r, int k){
    swap(arr[l], arr[rand() % (r - l + 1) + l]);

    T pivot = arr[l];

    int j = l;

    for (int i = l; i <= r; ++i) {
        if (arr[i] < pivot)
            swap(arr[i], arr[++j]);
    }

    swap(arr[l], arr[j]);

    return j;
}

template <typename T>
T __selection(T arr[], int l, int r, int k){
    if (l == r)
        return arr[l];

    int p = __partition(arr, l, r, k);
    if (p == k)
        return arr[p];
    else if (p < k)
        return __selection(arr, p+1, r, k);
    else
        return __selection(arr, l, p-1, k);
}

template <typename T>
T nLargestElement(T arr[], int n, int k){
    assert(k >= 0 && k < n);
    srand(time(nullptr));
    return __selection(arr, 0, n-1, n-k);
}

template <typename T>
T nSmallestElement(T arr[], int n, int k){
    assert(k >= 0 && k < n);
    srand(time(nullptr));
    return __selection(arr, 0, n-1, k-1);
}
```

This algo is $O(n)$ 