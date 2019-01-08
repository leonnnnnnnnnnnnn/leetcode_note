# Top K Frequent Elements

## Description

Given a non-empty array of integers, return the **k** most frequent elements.

**Example 1:**

```
Input: nums = [1,1,1,2,2,3], k = 2
Output: [1,2]
```

**Example 2:**

```
Input: nums = [1], k = 1
Output: [1]
```

**Note:**

- You may assume *k* is always valid, 1 ≤ *k* ≤ number of unique elements.
- Your algorithm's time complexity **must be** better than O(*n* log *n*), where *n* is the array's size.

## Solution 1: Priority Queue

### Step 1: Calculate frequency using map

### Step 2: Build a priority queue given the frequency map

```python
def solution(nums, k):
    freq_map = dict()
    for x in nums:
        freq_map[x] = freq_map.get(x, 0) + 1
    pq = PriorityQueue()
    for element, freq in freq_map.items():
        if pq.get_size() < k:
            pq.enqueue(Frequency(element, freq))
        elif freq > pq.get_front().freq:
            pq.dequeue()
            pq.enqueue(Frequency(element, freq))
    res = []
    while not pq.is_empty():
        res.append(pq.dequeue().e)
    return res
```

**Class Frequency**

```python
class Frequency:
    def __init__(self, e, freq):
        self.e = e
        self.freq = freq

    """
    define priority: the smaller the frequency, the higher the priority, which is equivalent to a MinHeap
    """
    def __gt__(self, other):
        if isinstance(other, Frequency):
            return self.freq < other.freq

    def __ge__(self, other):
        if isinstance(other, Frequency):
            return self.freq <= other.freq

    def __lt__(self, other):
        if isinstance(other, Frequency):
            return self.freq > other.freq

    def __le__(self, other):
        if isinstance(other, Frequency):
            return self.freq >= other.freq

    def __eq__(self, other):
        if isinstance(other, Frequency):
            return self.freq == other.freq

    def __ne__(self, other):
        if isinstance(other, Frequency):
            return self.freq != other.freq
```

**class PriorityQueue**

```python
class QueueBase:
    def enqueue(self, e):
        pass

    def dequeue(self):
        pass

    def get_size(self):
        pass

    def get_front(self):
        pass

    def is_empty(self):
        pass
    
class PriorityQueue(QueueBase):
    def __init__(self):
        self._maxheap = MaxHeap()

    def get_size(self):
        return self._maxheap.get_size()

    def is_empty(self):
        return self._maxheap.is_empty()

    def get_front(self):
        return self._maxheap.find_max()

    def enqueue(self, e):
        self._maxheap.add(e)

    def dequeue(self):
        return self._maxheap.extract_max()
```

**class MaxHeap**

```python
class MaxHeap:
    def __init__(self, arr=None, capacity=None):
        if isinstance(arr, Array):
            self._data = arr
            for i in range(self._parent(self._data.get_size() - 1), -1, -1):
                self._sift_down(i)
        else:
            if not capacity:
                self._data = Array()
            else:
                self._data = Array(capacity=capacity)

    def get_size(self):
        return self._data.get_size()

    def is_empty(self):
        return self._data.is_empty()

    @staticmethod
    def _parent(index):
        if index == 0:
            raise IndexError("index-0 does not have parent!")
        return (index - 1) // 2

    @staticmethod
    def _left_child(index):
        return index * 2 + 1

    @staticmethod
    def _right_child(index):
        return index * 2 + 2

    def add(self, e):
        self._data.add_last(e)
        self._sift_up(self.get_size() - 1)

    def _sift_up(self, index):
        while index > 0 and self._data.get(self._parent(index)) < self._data.get(index):
            self._data.swap(index, self._parent(index))
            index = self._parent(index)

    def find_max(self):
        if self._data.is_empty():
            raise ValueError("Heap is empty!")
        return self._data.get(0)

    def extract_max(self):
        rtn = self.find_max()
        self._data.swap(0, self._data.get_size() - 1)
        self._data.remove_last()
        self._sift_down(0)
        return rtn

    def _sift_down(self, index):
        while self._left_child(index) < self.get_size():
            max_child = self._left_child(index)
            if max_child + 1 < self.get_size() and self._data.get(max_child + 1) > self._data.get(max_child):
                max_child += 1
            if self._data.get(index) >= self._data.get(max_child):
                break
            self._data.swap(index, max_child)
            index = max_child

    def replace(self, e):
        rtn = self.find_max()
        self._data.set(0, e)
        self._sift_down(0)
        return rtn
```

**class Array**

```python
class Array:
    def __init__(self, arr=None, capacity=10):
        if isinstance(arr, list):
            self._data = arr[:]
            self._size = len(arr)
        else:
            self._data = [None] * capacity
            self._size = 0

    def get_size(self):
        return self._size

    def get_capacity(self):
        return len(self._data)

    def is_empty(self):
        return self._size == 0

    def add_last(self, e):
        return self.add(self._size, e)

    def add_first(self, e):
        return self.add(0, e)

    def add(self, index, e):
        if not 0 <= index <= self._size:
            raise IndexError("Array index out of range")
        # dynamically expand array capacity
        if self._size == len(self._data):
            if self._size == 0:
                self._resize(1)
            else:
                self._resize(2 * self._size)
        for i in range(self._size - 1, index - 1, -1):
            self._data[i + 1] = self._data[i]
        self._data[index] = e
        self._size += 1

    def get_last(self):
        return self.get(self._size - 1)

    def get_first(self):
        return self.get(0)

    def get(self, index):
        if not 0 <= index < self._size:
            raise IndexError("Array index out of range")
        return self._data[index]

    def set(self, index, e):
        if not 0 <= index < self._size:
            raise IndexError("Array index out of range")
        self._data[index] = e

    def find(self, e):
        for i in range(self._size):
            if self._data[i] == e:
                return i
        return -1

    def find_all(self, e):
        rtn = []
        for i in range(self._size):
            if self._data[i] == e:
                rtn.append(i)
        return rtn

    def remove_first(self):
        return self.remove(0)

    def remove_last(self):
        return self.remove(self._size - 1)

    def remove(self, index):
        if not 0 <= index < self._size:
            raise IndexError("Array index out of range")
        rtn = self._data[index]
        for i in range(index + 1, self._size):
            self._data[i - 1] = self._data[i]
        self._size -= 1
        self._data[self._size] = None
        # dynamically maintain data capacity
        if self._size != 1 and self._size == len(self._data) // 4:  # lazy evaluation
            self._resize(len(self._data) // 2)
        return rtn

    def remove_element(self, e):
        ind = self.find(e)
        if ind == -1:
            return False
        else:
            self.remove(ind)

    def remove_all(self, e):
        while not self.find(e) == -1:
            self.remove(self.find(e))

    def swap(self, i, j):
        if not 0 <= i < self._size or not 0 <= j < self._size:
            raise IndexError("Array index out of range")
        self._data[i], self._data[j] = self._data[j], self._data[i]

    def _resize(self, new_capacity):
        new_data = [None] * new_capacity
        for i in range(self._size):
            new_data[i] = self._data[i]
        self._data = new_data

    def __contains__(self, item):
        return item in self._data

    def __str__(self):
        return "Array: size={}, capacity={}\n{}".format(self._size, len(self._data), self._data[:self._size])

    def __repr__(self):
        return self.__str__()
```

## Solution 2: Use Python heapq

```python
import heapq


solution(nums, k):
    freq_map = dict()
    for x in nums:
        freq_map[x] = freq_map.get(x, 0) + 1
    freq_list = list(freq_map.items())
    rtn = [val[0] for val in heapq.nlargest(k, freq_list, key=lambda k: k[1])]
    return rtn
```

