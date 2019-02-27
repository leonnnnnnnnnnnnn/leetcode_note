# Reverse String - LC 344

## Description

Write a function that reverses a string. The input string is given as an array of characters `char[]`.

Do not allocate extra space for another array, you must do this by **modifying the input array in-place**with O(1) extra memory.

You may assume all the characters consist of [printable ascii characters](https://en.wikipedia.org/wiki/ASCII#Printable_characters).

 

**Example 1:**

```
Input: ["h","e","l","l","o"]
Output: ["o","l","l","e","h"]
```

**Example 2:**

```
Input: ["H","a","n","n","a","h"]
Output: ["h","a","n","n","a","H"]
```

## Solution 1: Two pointers

```cpp
void reverseString(vector<char>& s) {
        int i = 0;
        int j = static_cast<int>(s.size()) - 1;
        
        while(i < j) {
            swap(s[i], s[j]);
            i++;
            j--;
        }
        
    }
```

