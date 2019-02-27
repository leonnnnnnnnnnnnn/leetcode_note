# Reverse Integer - LC 7

## Description

Given a 32-bit signed integer, reverse digits of an integer.

**Example 1:**

```
Input: 123
Output: 321
```

**Example 2:**

```
Input: -123
Output: -321
```

**Example 3:**

```
Input: 120
Output: 21
```

**Note:**
Assume we are dealing with an environment which could only store integers within the 32-bit signed integer range: [−231,  231 − 1]. For the purpose of this problem, assume that your function returns 0 when the reversed integer overflows.



## Solution1

```python
def reverse(x):
    if x > 2**31 - 1 or x < -2**31:
        return 0

	def inverse(input):
    	rtn = 0
    	while input != 0:
        	rtn = rtn * 10 + input % 10
        	input //= 10
        	return rtn
        
    sign = 1
    if x < 0:
        sign = -1
        rtn = inverse(abs(x)) * sign
        if rtn > 2**31 - 1 or rtn < -2**31:
            return 0
        return rtn
    
```

As of overflow issue, should consider both input and output!!!