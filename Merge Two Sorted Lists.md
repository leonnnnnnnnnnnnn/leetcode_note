# Merge Two Sorted Lists - LC 21

## Description

Merge two sorted linked lists and return it as a new list. The new list should be made by splicing together the nodes of the first two lists.

**Example:**

```
Input: 1->2->4, 1->3->4
Output: 1->1->2->3->4->4
```

```python
class ListNode:
    def __init__(self, x):
        self.val = x
        self.next = None
```



## Solution 1: Iteration

```python
def solution(l1, l2):
    dummy = curr = ListNode(0)

    while l1 and l2:
        if l1.val < l2.val:
            curr.next = l1
            l1 = l1.next
        else:
            curr.next = l2
            l2 = l2.next
        curr = curr.next
        
    curr.next = l1 or l2
    return dummy.next
```

Beats 99.3% python submission.

## Solution 2: Recurrion

```python
def solution2(l1, l2):
    if not l1 or not l2:
        return l1 or l2
    elif l1.val < l2.val:
        l1.next = solution2(l1.next, l2)
        return l1
    else:
        l2.next = solution2(l1, l2.next)
        return l2
```

More elegant than solution1