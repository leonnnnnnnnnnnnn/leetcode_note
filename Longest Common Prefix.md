# Longest Common Prefix - LC 14

## Description


Write a function to find the longest common prefix string amongst an array of strings.

If there is no common prefix, return an empty string `""`.

**Example 1:**

```
Input: ["flower","flow","flight"]
Output: "fl"
```

**Example 2:**

```
Input: ["dog","racecar","car"]
Output: ""
Explanation: There is no common prefix among the input strings.
```

**Note:**

All given inputs are in lowercase letters `a-z`.



## Solution 1

```python
def solution(strs):
    if not strs:
        return ""
    if len(strs) == 1:
        return strs[0]
    rtn = ""
    for char in strs[0]:
        for word in strs[1:]:
            if not word.startswith(rtn + char):
                return rtn
        rtn += char
    return rtn
```

Beat 82.43% python submissions. Use built-in method of python string, strartswith. What if there is not  such one?

Be careful with edge cases such as empty array and array of one string.

Time complexity is ``O(n)``, where n is the sum of all characters in the array. 

This method is actually a vertical scanning, comparing column first.

## Solution 2

```python
def solution(strs):
    if not strs:
        return ""
    if len(strs) == 1:
        return strs[0]
    
    sorted_array = sorted(strs)
    first = sorted_array[0]
    last = sorted_array[-1]
    rtn = ""
    for i in range(min(len(first), len(last))):
        if first[i] == last[i]:
            rtn += first[i]
        else:
            return rtn
    return rtn
```

