# Hashing - Key Concepts to Master

## 1. Hash Functions and Properties

### What is a Hash Function?
A function that maps data of arbitrary size to fixed-size values.

### Properties of Good Hash Function
1. **Deterministic:** Same input always gives same output
2. **Uniform Distribution:** Spreads keys evenly across buckets
3. **Efficient:** Fast to compute
4. **Minimize Collisions:** Different inputs rarely produce same hash

### Simple Hash Function Example
```python
def simple_hash(key, table_size):
    hash_value = 0
    for char in str(key):
        hash_value = (hash_value * 31 + ord(char)) % table_size
    return hash_value
```

### Python's Built-in Hash
```python
hash("hello")  # Returns integer hash value
# Note: Hash values are randomized between Python sessions (security)
```

## 2. Collision Resolution

### Chaining (Separate Chaining)
Each bucket contains a linked list of entries.
```python
class HashMapChaining:
    def __init__(self, size=1000):
        self.size = size
        self.buckets = [[] for _ in range(size)]

    def put(self, key, value):
        idx = hash(key) % self.size
        for pair in self.buckets[idx]:
            if pair[0] == key:
                pair[1] = value
                return
        self.buckets[idx].append([key, value])

    def get(self, key):
        idx = hash(key) % self.size
        for pair in self.buckets[idx]:
            if pair[0] == key:
                return pair[1]
        return -1
```

### Open Addressing (Linear Probing)
Find next available slot on collision.
```python
class HashMapOpenAddressing:
    def __init__(self, size=1000):
        self.size = size
        self.keys = [None] * size
        self.values = [None] * size

    def put(self, key, value):
        idx = hash(key) % self.size
        while self.keys[idx] is not None and self.keys[idx] != key:
            idx = (idx + 1) % self.size
        self.keys[idx] = key
        self.values[idx] = value

    def get(self, key):
        idx = hash(key) % self.size
        while self.keys[idx] is not None:
            if self.keys[idx] == key:
                return self.values[idx]
            idx = (idx + 1) % self.size
        return -1
```

## 3. Hash Set vs Hash Map

### Hash Set (Python: set)
Stores unique values only.
```python
seen = set()
seen.add(1)
seen.add(2)
seen.add(1)  # No effect
1 in seen  # True
```

### Hash Map (Python: dict)
Stores key-value pairs.
```python
counter = {}
counter['a'] = counter.get('a', 0) + 1

# Using defaultdict
from collections import defaultdict
counter = defaultdict(int)
counter['a'] += 1
```

## 4. Time Complexity Analysis

| Operation | Average | Worst Case |
|-----------|---------|------------|
| Insert | O(1) | O(n) |
| Delete | O(1) | O(n) |
| Lookup | O(1) | O(n) |

**Worst case:** All keys hash to same bucket (all collisions)

## 5. Using Hashing for O(1) Lookups

### Two Sum Pattern
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

### Duplicate Detection
```python
def contains_duplicate(nums):
    return len(nums) != len(set(nums))
```

## 6. Frequency Counting

### Using Counter
```python
from collections import Counter

def frequency_count(arr):
    return Counter(arr)

# Most common elements
counter = Counter(arr)
top_k = counter.most_common(k)
```

### Manual Counting
```python
def count_frequency(arr):
    freq = {}
    for item in arr:
        freq[item] = freq.get(item, 0) + 1
    return freq
```

## 7. Subarray Sum Using Hashing

### Subarray Sum Equals K
```python
def subarray_sum(nums, k):
    count = 0
    prefix_sum = 0
    sum_count = {0: 1}  # prefix_sum -> count

    for num in nums:
        prefix_sum += num
        # Check if (prefix_sum - k) exists
        if prefix_sum - k in sum_count:
            count += sum_count[prefix_sum - k]
        sum_count[prefix_sum] = sum_count.get(prefix_sum, 0) + 1

    return count
```

### Key Insight
If prefix_sum[j] - prefix_sum[i] = k, then subarray [i+1, j] has sum k.

## Common Hashing Patterns

| Pattern | Use Case | Example |
|---------|----------|---------|
| Seen Set | Track visited | Two Sum, Contains Duplicate |
| Frequency Map | Count occurrences | Anagram, Top K Frequent |
| Prefix Sum Map | Subarray sum | Subarray Sum Equals K |
| Index Map | Store positions | Two Sum indices |
| Grouping | Group by property | Group Anagrams |

## Load Factor and Rehashing

### Load Factor
```
load_factor = number_of_entries / number_of_buckets
```

### When to Rehash
- Python rehashes when load factor exceeds ~2/3
- Rehashing doubles the bucket count
- All entries must be rehashed to new buckets

### Performance Impact
- Low load factor: More memory, fewer collisions
- High load factor: Less memory, more collisions
