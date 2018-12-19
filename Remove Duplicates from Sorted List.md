# Remove Duplicates from Sorted List

## Description

Given a sorted linked list, delete all duplicates such that each element appear only *once*.

**Example 1:**

```
Input: 1->1->2
Output: 1->2
```

**Example 2:**

```
Input: 1->1->2->3->3
Output: 1->2->3
```

## Solution 1: Loop

```python
def solution(head):
    dummy = ListNode(0)
    dummy.next = cur = head
    while cur:
        next = cur.next
        while next and cur.val == next.val:
            next = next.next
        cur.next = next
        cur = cur.next
    return dummy.next
```

Time complexity $O(n)$. Beats 99.41% python submissions

## Solution 2: Recurrsion

```python
def solution(head):
    dummy = ListNode(0)
    dummy.next = head
    if not head or not head.next:
        return dummy.next
    elif head.val == head.next.val:
        dummy.next = solution(head.next)
        return dummy.next
    else:
        head.next = solution(head.next)
        return dummy.next
```

Time complexity $O(1)$, space complexity $O(n)$, might cause stackoverflow. 

Actually, there is no need to create a dummy head variable.

```python
def solution(head):
    if not head or not head.next():
        return head
    elif head.val == head.next.val:
        return solution(head.next)
    else:
        head.next = solution(head.next)
        return head
```

Beats 99.46% python submissions