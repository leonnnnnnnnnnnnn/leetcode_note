#  Implement strStr()

## Description

Implement [strStr()](http://www.cplusplus.com/reference/cstring/strstr/).

Return the index of the first occurrence of needle in haystack, or **-1** if needle is not part of haystack.

**Example 1:**

```
Input: haystack = "hello", needle = "ll"
Output: 2
```

**Example 2:**

```
Input: haystack = "aaaaa", needle = "bba"
Output: -1
```

**Clarification:**

What should we return when `needle` is an empty string? This is a great question to ask during an interview.

For the purpose of this problem, we will return 0 when `needle` is an empty string. This is consistent to C's [strstr()](http://www.cplusplus.com/reference/cstring/strstr/) and Java's [indexOf()](https://docs.oracle.com/javase/7/docs/api/java/lang/String.html#indexOf(java.lang.String)).

## Solution 1: A naive algo

```python
def solution(haystack, needle):
    if not needle:
        return 0

    l_needle = len(needle)
    l_hay = len(haystack)

    if l_needle > l_hay:
        return -1

    elif l_needle == l_hay:
        return 0 if needle == haystack else -1

    else:
        for i in range(l_hay - l_needle + 1):
            if haystack[i:i + l_needle] == needle:
                return i

        return -1
```

Beats 96.3% python submission. Time complexity $O(n)$.

## Solution 2: Use str.find() method of Python

```python
def solution(haystack, needle):
    return haystack.find(needle)
```

