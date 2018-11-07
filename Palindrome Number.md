# Palindrome Number

## Description

Determine whether an integer is a palindrome. An integer is a palindrome when it reads the same backward as forward.

**Example 1:**

```
Input: 121
Output: true
```

**Example 2:**

```
Input: -121
Output: false
Explanation: From left to right, it reads -121. From right to left, it becomes 121-. Therefore it is not a palindrome.
```

**Example 3:**

```
Input: 10
Output: false
Explanation: Reads 01 from right to left. Therefore it is not a palindrome.
```

## Solution 1: same as reverse a number

```python
def solution(x):
    if x < 0:
        return False
    reverse = 0
    input = x
    while input > 0:
        reverse = reverse * 10 + input % 10
        input //= 10
    if reverse == x:
        return True
    else: 
        return False
```

Beat 18.73% python submissions... simply reversing the number is not the best solution for this problem lol

## Solution 2: no need to reverse the whole number, just the last half

```python
def solution(x):
    if x // 10 == 0:
        return True

    if x < 0 or x % 10 == 0:
        return False

    first_half = x
    last_half = 0
    while first_half > last_half:
        last_half = last_half * 10 + first_half % 10
        first_half //= 10
    if first_half == last_half:
        return True
    elif first_half == last_half // 10:
        return True
    else:
        return False
```

The problem reduced to determine if we have reached the half point of the number.

Edges cases should be taken good care of:

1. If x is negative or a multiple of 10, return False
2. If x is in [0, 9], return True
3. If x is 0, which belongs to both 2 cases above, we should then check case 2 first, then case 1

Beat 90.67% python submissions.

## Solution 3: Convert to str, which needs extra space

```python
def solution(x):
    temp = str(x)
    return temp == temp[::-1]
```

