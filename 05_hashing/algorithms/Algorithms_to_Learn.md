# Hashing - Algorithms to Learn

## 1. Two Sum Using Hash Map

### Problem
Find indices of two numbers that add up to target.

### Algorithm
```python
def two_sum(nums, target):
    seen = {}
    for i, num in enumerate(nums):
        complement = target - num
        if complement in seen:
            return [seen[complement], i]
        seen[num] = i
    return []
```

### Complexity
- **Time:** O(n)
- **Space:** O(n)

---

## 2. Group Anagrams

### Problem
Group strings that are anagrams of each other.

### Algorithm
```python
from collections import defaultdict

def group_anagrams(strs):
    groups = defaultdict(list)

    for s in strs:
        # Sort string as key
        key = ''.join(sorted(s))
        groups[key].append(s)

    return list(groups.values())

# Alternative: Use character count as key
def group_anagrams_count(strs):
    groups = defaultdict(list)

    for s in strs:
        count = [0] * 26
        for c in s:
            count[ord(c) - ord('a')] += 1
        groups[tuple(count)].append(s)

    return list(groups.values())
```

### Complexity
- **Time:** O(n × k log k) where k is max string length
- **Space:** O(n × k)

---

## 3. Longest Consecutive Sequence

### Problem
Find the length of longest consecutive elements sequence.

### Algorithm
```python
def longest_consecutive(nums):
    num_set = set(nums)
    longest = 0

    for num in num_set:
        # Only start counting if num-1 not in set
        if num - 1 not in num_set:
            current_num = num
            current_streak = 1

            while current_num + 1 in num_set:
                current_num += 1
                current_streak += 1

            longest = max(longest, current_streak)

    return longest
```

### Complexity
- **Time:** O(n)
- **Space:** O(n)

---

## 4. Subarray Sum Equals K

### Problem
Find total number of continuous subarrays with sum equal to k.

### Algorithm
```python
def subarray_sum(nums, k):
    count = 0
    prefix_sum = 0
    sum_count = {0: 1}

    for num in nums:
        prefix_sum += num
        if prefix_sum - k in sum_count:
            count += sum_count[prefix_sum - k]
        sum_count[prefix_sum] = sum_count.get(prefix_sum, 0) + 1

    return count
```

### Complexity
- **Time:** O(n)
- **Space:** O(n)

---

## 5. Find Duplicate in Array

### Problem
Find the duplicate number in array where each element is 1 to n-1.

### Algorithm (Using Set)
```python
def find_duplicate(nums):
    seen = set()
    for num in nums:
        if num in seen:
            return num
        seen.add(num)
    return -1
```

### Algorithm (Floyd's Cycle Detection)
```python
def find_duplicate_floyd(nums):
    slow = fast = nums[0]

    # Find intersection point
    while True:
        slow = nums[slow]
        fast = nums[nums[fast]]
        if slow == fast:
            break

    # Find entrance to cycle
    slow = nums[0]
    while slow != fast:
        slow = nums[slow]
        fast = nums[fast]

    return slow
```

### Complexity
- **Time:** O(n)
- **Space:** O(1) with Floyd's

---

## 6. Count Frequency of Elements

### Problem
Count frequency of each element in array.

### Algorithm
```python
from collections import Counter

def count_frequency(nums):
    return Counter(nums)

# Manual implementation
def count_frequency_manual(nums):
    freq = {}
    for num in nums:
        freq[num] = freq.get(num, 0) + 1
    return freq
```

### Complexity
- **Time:** O(n)
- **Space:** O(n)

---

## 7. LRU Cache Implementation

### Problem
Design a Least Recently Used (LRU) cache.

### Algorithm
```python
from collections import OrderedDict

class LRUCache:
    def __init__(self, capacity):
        self.capacity = capacity
        self.cache = OrderedDict()

    def get(self, key):
        if key not in self.cache:
            return -1
        self.cache.move_to_end(key)
        return self.cache[key]

    def put(self, key, value):
        if key in self.cache:
            self.cache.move_to_end(key)
        self.cache[key] = value
        if len(self.cache) > self.capacity:
            self.cache.popitem(last=False)
```

### Using Doubly Linked List + Hash Map
```python
class Node:
    def __init__(self, key=0, value=0):
        self.key = key
        self.value = value
        self.prev = None
        self.next = None

class LRUCacheManual:
    def __init__(self, capacity):
        self.capacity = capacity
        self.cache = {}
        self.head = Node()
        self.tail = Node()
        self.head.next = self.tail
        self.tail.prev = self.head

    def _remove(self, node):
        node.prev.next = node.next
        node.next.prev = node.prev

    def _add(self, node):
        node.prev = self.tail.prev
        node.next = self.tail
        self.tail.prev.next = node
        self.tail.prev = node

    def get(self, key):
        if key in self.cache:
            node = self.cache[key]
            self._remove(node)
            self._add(node)
            return node.value
        return -1

    def put(self, key, value):
        if key in self.cache:
            self._remove(self.cache[key])
        node = Node(key, value)
        self._add(node)
        self.cache[key] = node
        if len(self.cache) > self.capacity:
            lru = self.head.next
            self._remove(lru)
            del self.cache[lru.key]
```

### Complexity
- **Time:** O(1) for both get and put
- **Space:** O(capacity)

---

## 8. LFU Cache Implementation

### Problem
Design a Least Frequently Used (LFU) cache.

### Algorithm
```python
from collections import defaultdict, OrderedDict

class LFUCache:
    def __init__(self, capacity):
        self.capacity = capacity
        self.min_freq = 0
        self.key_to_val_freq = {}  # key -> (value, frequency)
        self.freq_to_keys = defaultdict(OrderedDict)  # freq -> OrderedDict of keys

    def get(self, key):
        if key not in self.key_to_val_freq:
            return -1

        value, freq = self.key_to_val_freq[key]
        del self.freq_to_keys[freq][key]

        if not self.freq_to_keys[freq]:
            del self.freq_to_keys[freq]
            if freq == self.min_freq:
                self.min_freq += 1

        self.freq_to_keys[freq + 1][key] = True
        self.key_to_val_freq[key] = (value, freq + 1)

        return value

    def put(self, key, value):
        if self.capacity <= 0:
            return

        if key in self.key_to_val_freq:
            self.get(key)  # Update frequency
            self.key_to_val_freq[key] = (value, self.key_to_val_freq[key][1])
            return

        if len(self.key_to_val_freq) >= self.capacity:
            lru_key, _ = self.freq_to_keys[self.min_freq].popitem(last=False)
            del self.key_to_val_freq[lru_key]

        self.key_to_val_freq[key] = (value, 1)
        self.freq_to_keys[1][key] = True
        self.min_freq = 1
```

### Complexity
- **Time:** O(1) for both get and put
- **Space:** O(capacity)
