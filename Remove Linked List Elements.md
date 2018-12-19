# Remove Linked List Elements

## Description

Remove all elements from a linked list of integers that have value **val**.

**Example:**

```
Input:  1->2->6->3->4->5->6, val = 6
Output: 1->2->3->4->5
```

## Solution 1: Loop

```python
def solution(head, val):
    dummy = pre = ListNode(0)
    dummy.next = head
    while pre:
        cur = pre.next
        while cur and cur.val == val:
            cur = cur.next
        pre.next = cur
        pre = pre.next
    return dummy.next
```

Time complexity $O(n)$. Beats 100% python submission

Another loop solution:

```python
def solution(head, val):
    dummy = pre = ListNode(0)
    dummy.next = head
    while pre.next:
        if pre.next.val == val:
            pre.next = pre.next.next
        else:
            pre = pre.next

    return dummy.next
```



## Solution 2: Recursion

```python
def solution(head, val):
    dummy = ListNode(0)
    dummy.next = head
    if not head:
        return dummy.next
    elif head.val == val:
        dummy.next = recursion_remove_element(head.next, val)
        return dummy.next
    else:
        head.next = recursion_remove_element(head.next, val)
        return dummy.next
```

Time complexity $O(1)$, but $O(n)$ space cpmpleity; it might cause stackoverflow.

Actually, there is no need to create a dummy head, which is similar to problem *Remove Duplicates from Sorted List*.

```python
def solution(head, val):
    if not head:
        return head
    elif head.val == val:
        return solution(head.next, val)
    else:
        head.next = solution(head.next, val)
        return head
```

