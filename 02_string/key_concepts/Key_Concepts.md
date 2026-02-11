# String - Key Concepts to Master

## 1. Two Pointers for String Manipulation

### Opposite Direction Pointers
```python
def reverse_string(s):
    left, right = 0, len(s) - 1
    s = list(s)  # Convert to list for mutability
    while left < right:
        s[left], s[right] = s[right], s[left]
        left += 1
        right -= 1
    return ''.join(s)
```
**Use Cases:**
- Reverse string
- Check palindrome
- Valid palindrome ignoring non-alphanumeric

## 2. Sliding Window for Substring Problems

### Fixed Size Window
```python
def find_anagrams(s, p):
    result = []
    p_count = Counter(p)
    s_count = Counter(s[:len(p)])

    if s_count == p_count:
        result.append(0)

    for i in range(len(p), len(s)):
        # Add new character
        s_count[s[i]] += 1
        # Remove old character
        s_count[s[i - len(p)]] -= 1
        if s_count[s[i - len(p)]] == 0:
            del s_count[s[i - len(p)]]

        if s_count == p_count:
            result.append(i - len(p) + 1)

    return result
```

### Variable Size Window
```python
def length_of_longest_substring(s):
    char_index = {}
    left = max_len = 0

    for right, char in enumerate(s):
        if char in char_index and char_index[char] >= left:
            left = char_index[char] + 1
        char_index[char] = right
        max_len = max(max_len, right - left + 1)

    return max_len
```

## 3. KMP Algorithm for Pattern Matching

### Compute LPS (Longest Proper Prefix which is also Suffix)
```python
def compute_lps(pattern):
    lps = [0] * len(pattern)
    length = 0
    i = 1

    while i < len(pattern):
        if pattern[i] == pattern[length]:
            length += 1
            lps[i] = length
            i += 1
        else:
            if length != 0:
                length = lps[length - 1]
            else:
                lps[i] = 0
                i += 1

    return lps

def kmp_search(text, pattern):
    if not pattern:
        return 0

    lps = compute_lps(pattern)
    i = j = 0

    while i < len(text):
        if text[i] == pattern[j]:
            i += 1
            j += 1

            if j == len(pattern):
                return i - j  # Found at index i - j
        else:
            if j != 0:
                j = lps[j - 1]
            else:
                i += 1

    return -1
```
**Time Complexity:** O(n + m) where n = text length, m = pattern length

## 4. Palindrome Expansion Technique

### Expand Around Center
```python
def longest_palindrome(s):
    def expand(left, right):
        while left >= 0 and right < len(s) and s[left] == s[right]:
            left -= 1
            right += 1
        return s[left + 1:right]

    result = ""
    for i in range(len(s)):
        # Odd length palindrome
        odd = expand(i, i)
        # Even length palindrome
        even = expand(i, i + 1)
        result = max(result, odd, even, key=len)

    return result
```
**Time Complexity:** O(n²)
**Space Complexity:** O(1)

## 5. String Hashing (Rabin-Karp)

### Rolling Hash
```python
def rabin_karp(text, pattern):
    n, m = len(text), len(pattern)
    if m > n:
        return -1

    # Parameters for hashing
    base = 256
    mod = 10**9 + 7

    # Calculate (base^(m-1)) % mod
    h = pow(base, m - 1, mod)

    # Calculate hash of pattern and first window
    pattern_hash = 0
    window_hash = 0

    for i in range(m):
        pattern_hash = (pattern_hash * base + ord(pattern[i])) % mod
        window_hash = (window_hash * base + ord(text[i])) % mod

    # Slide the pattern over text
    for i in range(n - m + 1):
        if pattern_hash == window_hash:
            if text[i:i + m] == pattern:
                return i

        if i < n - m:
            # Remove leading character, add trailing
            window_hash = (window_hash - ord(text[i]) * h) % mod
            window_hash = (window_hash * base + ord(text[i + m])) % mod
            window_hash = (window_hash + mod) % mod  # Handle negative

    return -1
```

## 6. Trie for Prefix Matching

See Trie section for detailed implementation.

**Use Cases:**
- Autocomplete
- Spell checker
- Longest common prefix
- Word search with wildcards

## Common String Patterns

| Pattern | Use Case | Example |
|---------|----------|---------|
| Two Pointers | Palindrome, Reverse | Valid Palindrome |
| Sliding Window | Substring problems | Longest Substring Without Repeating |
| Hash Map | Anagram, Frequency | Group Anagrams |
| Stack | Parsing, Matching | Valid Parentheses |
| Trie | Prefix operations | Word Dictionary |
| KMP | Pattern matching | Implement strStr() |

## Time Complexity Reference

| Operation | Time Complexity |
|-----------|----------------|
| Access char by index | O(1) |
| Search char | O(n) |
| Concatenation | O(n + m) |
| Slice | O(k) |
| KMP search | O(n + m) |
| Rabin-Karp (avg) | O(n + m) |
| Expand around center | O(n²) |
