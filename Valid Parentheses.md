# Valid Parentheses

## Description

Given a string containing just the characters `'('`, `')'`, `'{'`, `'}'`, `'['` and `']'`, determine if the input string is valid.

An input string is valid if:

1. Open brackets must be closed by the same type of brackets.
2. Open brackets must be closed in the correct order.

Note that an empty string is also considered valid.

**Example 1:**

```
Input: "()"
Output: true
```

**Example 2:**

```
Input: "()[]{}"
Output: true
```

**Example 3:**

```
Input: "(]"
Output: false
```

**Example 4:**

```
Input: "([)]"
Output: false
```

**Example 5:**

```
Input: "{[]}"
Output: true
```

## Solution 1: Stack

```python
def solution(s):
    length = len(s)

    if not length % 2 == 0:
        return False

    if length == 0:
        return True

    paren = {"(": ")", "[": "]", "{": "}"}

    stack = []

    for p in s:
        if not stack or p in paren.keys():
            stack.append(p)
        elif stack[-1] in paren.keys() and p == paren[stack[-1]]:
            stack.pop()
        else:
            return False

    if len(stack) == 0:
        return True
    else:
        return False
```

Time complexity $O(n)$



