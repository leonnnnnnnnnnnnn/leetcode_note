# Add Two Numbers

## Description

You are given two **non-empty** linked lists representing two non-negative integers. The digits are stored in **reverse order** and each of their nodes contain a single digit. Add the two numbers and return it as a linked list.

You may assume the two numbers do not contain any leading zero, except the number 0 itself.

**Example:**

```
Input: (2 -> 4 -> 3) + (5 -> 6 -> 4)
Output: 7 -> 0 -> 8
Explanation: 342 + 465 = 807.
```



## Solution1

```python
def solution(l1, l2):
  if len(l1) >= len(l2):
    short = len(l2)
    long = len(l1)
    long_ls = l1
  else:
    short = len(l1)
    long = len(l2)
    long_ls = l1
    
  flag = 0
  rtn = []
  for i in range(short):
    s = l1[i] + l2[i] + flag
    flag = 0
    if s>=10:
      rtn.append(s - 10)
      flag = 1
    else:
      rtn.append(s)
      
  for x in long_ls[m:]:
    s = x + flag
    flag = 0
    if x>= 10:
      rtn.append(s - 10)
      flag = 1
     else:
       rtn.append(s)
   return rtn
    
```

Wrong answer!!! l1 and l2 are linked list! No len() attribute!!! Give another try!!!

```python
class ListNode:
  def __init__(self, x):
    self.val = x
    self.next = None
```

## Solution2:

```python
def addTwoNumbers(self, l1, l2):
    head = ListNode(0)
    previous = head
    flag = 0
    while l1 or l2 or flag:
        s = flag
        node = ListNode(0)
        if l1==l2==None:
            node.val += s
            previous.next = node
            break
        elif l1 is None:
            s += l2.val
        elif l2 is None:
            s += l1.val
        else:
            s += l1.val + l2.val
        
        flag = 0
    
        if s >= 10:
            node.val += (s - 10)
            flag = 1
        else:
            node.val += s
        if l1 is not None:
            l1 = l1.next
        if l2 is not None:
            l2 = l2.next

        previous.next = node
        previous = previous.next
    return head.next
```

Kind of excited ^o^. Faster than 95.33% of python3 submission!

## Solution 3 improvement of solution2

```python
def addTwoNumbers(self, l1, l2):
    prehead = ListNode(0)
    previous = prehead
    carry = 0
    while l1 or l2 or carry:
        if l1:
            carry += l1.val
            l1 = l1.next
        if l2:
            carry += l2.val
            l2 = l2.next
            
        node = ListNode(carry%10)
        carry //= 10
        
        previous.next = node
        previous = previous.next
        
    return prehead.next
```

More concise, more comfortable