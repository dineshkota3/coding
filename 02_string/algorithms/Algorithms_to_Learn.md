# String - Algorithms to Learn

## 1. Longest Substring Without Repeating Characters

### Problem
Find the length of the longest substring without repeating characters.

### Algorithm
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

### Complexity
- **Time:** O(n)
- **Space:** O(min(n, alphabet_size))

---

## 2. Longest Palindromic Substring

### Problem
Find the longest palindromic substring in a given string.

### Algorithm (Expand Around Center)
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

### Complexity
- **Time:** O(n²)
- **Space:** O(1)

---

## 3. Valid Anagram

### Problem
Determine if two strings are anagrams of each other.

### Algorithm
```python
def is_anagram(s, t):
    if len(s) != len(t):
        return False

    count = {}
    for char in s:
        count[char] = count.get(char, 0) + 1

    for char in t:
        if char not in count:
            return False
        count[char] -= 1
        if count[char] == 0:
            del count[char]

    return len(count) == 0

# Alternative using Counter
from collections import Counter
def is_anagram_simple(s, t):
    return Counter(s) == Counter(t)
```

### Complexity
- **Time:** O(n)
- **Space:** O(1) - limited to alphabet size

---

## 4. String to Integer (atoi)

### Problem
Convert a string to a 32-bit signed integer.

### Algorithm
```python
def my_atoi(s):
    s = s.strip()
    if not s:
        return 0

    sign = 1
    i = 0
    result = 0

    if s[0] in ['+', '-']:
        sign = -1 if s[0] == '-' else 1
        i = 1

    while i < len(s) and s[i].isdigit():
        digit = int(s[i])
        # Check for overflow
        if result > (2**31 - 1 - digit) // 10:
            return 2**31 - 1 if sign == 1 else -2**31
        result = result * 10 + digit
        i += 1

    return sign * result
```

### Complexity
- **Time:** O(n)
- **Space:** O(1)

---

## 5. KMP Pattern Matching

### Problem
Find the first occurrence of pattern in text.

### Algorithm
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

def str_str(text, pattern):
    if not pattern:
        return 0

    lps = compute_lps(pattern)
    i = j = 0

    while i < len(text):
        if text[i] == pattern[j]:
            i += 1
            j += 1

            if j == len(pattern):
                return i - j
        else:
            if j != 0:
                j = lps[j - 1]
            else:
                i += 1

    return -1
```

### Complexity
- **Time:** O(n + m)
- **Space:** O(m)

---

## 6. Rabin-Karp Algorithm

### Problem
Pattern matching using rolling hash.

### Algorithm
```python
def rabin_karp(text, pattern):
    n, m = len(text), len(pattern)
    if m > n:
        return -1

    base = 256
    mod = 10**9 + 7
    h = pow(base, m - 1, mod)

    pattern_hash = 0
    window_hash = 0

    for i in range(m):
        pattern_hash = (pattern_hash * base + ord(pattern[i])) % mod
        window_hash = (window_hash * base + ord(text[i])) % mod

    for i in range(n - m + 1):
        if pattern_hash == window_hash:
            if text[i:i + m] == pattern:
                return i

        if i < n - m:
            window_hash = (window_hash - ord(text[i]) * h) % mod
            window_hash = (window_hash * base + ord(text[i + m])) % mod
            window_hash = (window_hash + mod) % mod

    return -1
```

### Complexity
- **Time:** O(n + m) average, O(nm) worst case
- **Space:** O(1)

---

## 7. Z Algorithm

### Problem
Find all occurrences of pattern in text using Z-array.

### Algorithm
```python
def compute_z_array(s):
    n = len(s)
    z = [0] * n
    left = right = 0

    for i in range(1, n):
        if i <= right:
            z[i] = min(right - i + 1, z[i - left])

        while i + z[i] < n and s[z[i]] == s[i + z[i]]:
            z[i] += 1

        if i + z[i] - 1 > right:
            left, right = i, i + z[i] - 1

    return z

def z_algorithm_search(text, pattern):
    combined = pattern + '$' + text
    z = compute_z_array(combined)
    m = len(pattern)

    return [i - m - 1 for i in range(m + 1, len(z)) if z[i] == m]
```

### Complexity
- **Time:** O(n + m)
- **Space:** O(n + m)

---

## 8. Manacher's Algorithm

### Problem
Find the longest palindromic substring in O(n) time.

### Algorithm
```python
def manacher(s):
    # Transform string
    t = '#' + '#'.join(s) + '#'
    n = len(t)
    p = [0] * n
    center = right = 0

    for i in range(n):
        mirror = 2 * center - i

        if i < right:
            p[i] = min(right - i, p[mirror])

        # Attempt to expand palindrome
        while (i + p[i] + 1 < n and
               i - p[i] - 1 >= 0 and
               t[i + p[i] + 1] == t[i - p[i] - 1]):
            p[i] += 1

        # Update center and right boundary
        if i + p[i] > right:
            center = i
            right = i + p[i]

    # Find maximum palindrome
    max_len = max(p)
    center_idx = p.index(max_len)
    start = (center_idx - max_len) // 2

    return s[start:start + max_len]
```

### Complexity
- **Time:** O(n)
- **Space:** O(n)

---

## 9. Minimum Window Substring

### Problem
Find minimum window in s that contains all characters of t.

### Algorithm
```python
from collections import Counter

def min_window(s, t):
    if not s or not t:
        return ""

    need = Counter(t)
    have = {}
    need_count = len(need)
    have_count = 0

    left = 0
    min_len = float('inf')
    min_start = 0

    for right, char in enumerate(s):
        have[char] = have.get(char, 0) + 1

        if char in need and have[char] == need[char]:
            have_count += 1

        while have_count == need_count:
            if right - left + 1 < min_len:
                min_len = right - left + 1
                min_start = left

            have[s[left]] -= 1
            if s[left] in need and have[s[left]] < need[s[left]]:
                have_count -= 1
            left += 1

    return s[min_start:min_start + min_len] if min_len != float('inf') else ""
```

### Complexity
- **Time:** O(n + m)
- **Space:** O(k)

---

## 10. Group Anagrams

### Problem
Group strings that are anagrams of each other.

### Algorithm
```python
from collections import defaultdict

def group_anagrams(strs):
    groups = defaultdict(list)

    for s in strs:
        # Use sorted string as key
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
- **Time:** O(n × k log k)
- **Space:** O(n × k)

---

## 11. Palindromic Substrings

### Problem
Count number of palindromic substrings.

### Algorithm
```python
def count_substrings(s):
    count = 0

    def expand(left, right):
        nonlocal count
        while left >= 0 and right < len(s) and s[left] == s[right]:
            count += 1
            left -= 1
            right += 1

    for i in range(len(s)):
        expand(i, i)    # Odd length
        expand(i, i + 1)  # Even length

    return count
```

### Complexity
- **Time:** O(n²)
- **Space:** O(1)

---

## 12. Longest Palindromic Subsequence

### Problem
Find length of longest palindromic subsequence.

### Algorithm
```python
def longest_palindrome_subseq(s):
    n = len(s)
    dp = [[0] * n for _ in range(n)]

    for i in range(n):
        dp[i][i] = 1

    for length in range(2, n + 1):
        for i in range(n - length + 1):
            j = i + length - 1
            if s[i] == s[j]:
                dp[i][j] = 2 + dp[i + 1][j - 1] if length > 2 else 2
            else:
                dp[i][j] = max(dp[i + 1][j], dp[i][j - 1])

    return dp[0][n - 1]
```

### Complexity
- **Time:** O(n²)
- **Space:** O(n²)

---

## 13. Decode String

### Problem
Decode string with nested encoding (e.g., "3[a2[c]]" → "accaccacc").

### Algorithm
```python
def decode_string(s):
    stack = []
    current_num = 0
    current_str = ""

    for char in s:
        if char.isdigit():
            current_num = current_num * 10 + int(char)
        elif char == '[':
            stack.append((current_str, current_num))
            current_str = ""
            current_num = 0
        elif char == ']':
            prev_str, num = stack.pop()
            current_str = prev_str + current_str * num
        else:
            current_str += char

    return current_str
```

### Complexity
- **Time:** O(n)
- **Space:** O(n)

---

## 14. Encode and Decode Strings

### Problem
Encode list of strings to single string and decode back.

### Algorithm
```python
def encode(strs):
    result = ""
    for s in strs:
        result += str(len(s)) + '#' + s
    return result

def decode(s):
    result = []
    i = 0

    while i < len(s):
        j = i
        while s[j] != '#':
            j += 1
        length = int(s[i:j])
        j += 1
        result.append(s[j:j + length])
        i = j + length

    return result
```

### Complexity
- **Time:** O(n)
- **Space:** O(n)

---

## 15. Text Justification

### Problem
Format text with full justification.

### Algorithm
```python
def full_justify(words, maxWidth):
    result = []
    line = []
    line_length = 0

    for word in words:
        if line_length + len(word) + len(line) > maxWidth:
            # Distribute spaces
            total_spaces = maxWidth - line_length
            if len(line) == 1:
                result.append(line[0] + ' ' * total_spaces)
            else:
                space_between = total_spaces // (len(line) - 1)
                extra = total_spaces % (len(line) - 1)
                line_str = ""
                for i, w in enumerate(line[:-1]):
                    line_str += w + ' ' * (space_between + (1 if i < extra else 0))
                line_str += line[-1]
                result.append(line_str)

            line = []
            line_length = 0

        line.append(word)
        line_length += len(word)

    # Last line - left justified
    last_line = ' '.join(line)
    last_line += ' ' * (maxWidth - len(last_line))
    result.append(last_line)

    return result
```

### Complexity
- **Time:** O(n)
- **Space:** O(n)

---

## 16. Find All Anagrams in String

### Problem
Find all start indices of p's anagrams in s.

### Algorithm
```python
from collections import Counter

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

### Complexity
- **Time:** O(n)
- **Space:** O(k)

---

## 17. Multiply Strings

### Problem
Multiply two numbers represented as strings.

### Algorithm
```python
def multiply(num1, num2):
    if num1 == "0" or num2 == "0":
        return "0"

    m, n = len(num1), len(num2)
    result = [0] * (m + n)

    for i in range(m - 1, -1, -1):
        for j in range(n - 1, -1, -1):
            mul = (ord(num1[i]) - ord('0')) * (ord(num2[j]) - ord('0'))
            p1, p2 = i + j, i + j + 1
            total = mul + result[p2]

            result[p2] = total % 10
            result[p1] += total // 10

    result_str = ''.join(map(str, result))
    return result_str.lstrip('0')
```

### Complexity
- **Time:** O(m × n)
- **Space:** O(m + n)

---

## 18. Add Binary

### Problem
Add two binary strings.

### Algorithm
```python
def add_binary(a, b):
    result = []
    carry = 0
    i, j = len(a) - 1, len(b) - 1

    while i >= 0 or j >= 0 or carry:
        total = carry
        if i >= 0:
            total += int(a[i])
            i -= 1
        if j >= 0:
            total += int(b[j])
            j -= 1

        result.append(str(total % 2))
        carry = total // 2

    return ''.join(result[::-1])
```

### Complexity
- **Time:** O(max(m, n))
- **Space:** O(max(m, n))

---

## 19. Compare Version Numbers

### Problem
Compare two version numbers.

### Algorithm
```python
def compare_version(version1, version2):
    v1 = list(map(int, version1.split('.')))
    v2 = list(map(int, version2.split('.')))

    max_len = max(len(v1), len(v2))

    for i in range(max_len):
        n1 = v1[i] if i < len(v1) else 0
        n2 = v2[i] if i < len(v2) else 0

        if n1 < n2:
            return -1
        elif n1 > n2:
            return 1

    return 0
```

### Complexity
- **Time:** O(n + m)
- **Space:** O(n + m)

---

## 20. Reverse Words in String

### Problem
Reverse words in string with proper spacing.

### Algorithm
```python
def reverse_words(s):
    words = s.split()
    return ' '.join(words[::-1])

# In-place version (for mutable array)
def reverse_words_inplace(s):
    s = list(s)

    def reverse(l, r):
        while l < r:
            s[l], s[r] = s[r], s[l]
            l += 1
            r -= 1

    # Reverse entire string
    reverse(0, len(s) - 1)

    # Reverse each word
    start = 0
    for i in range(len(s)):
        if s[i] == ' ':
            reverse(start, i - 1)
            start = i + 1
    reverse(start, len(s) - 1)

    return ''.join(s)
```

### Complexity
- **Time:** O(n)
- **Space:** O(n) or O(1) in-place
