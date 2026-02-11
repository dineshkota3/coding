# Trie - Algorithms to Learn

## 1. Trie Implementation

### Problem
Implement a trie with insert, search, and startsWith.

### Algorithm
```python
class TrieNode:
    def __init__(self):
        self.children = {}
        self.is_end = False

class Trie:
    def __init__(self):
        self.root = TrieNode()

    def insert(self, word):
        node = self.root
        for char in word:
            if char not in node.children:
                node.children[char] = TrieNode()
            node = node.children[char]
        node.is_end = True

    def search(self, word):
        node = self.root
        for char in word:
            if char not in node.children:
                return False
            node = node.children[char]
        return node.is_end

    def startsWith(self, prefix):
        node = self.root
        for char in prefix:
            if char not in node.children:
                return False
            node = node.children[char]
        return True
```

### Complexity
- **Insert/Search/Prefix:** O(m) where m = word length
- **Space:** O(N × M)

---

## 2. Insert Operation

### Problem
Insert word into trie.

### Algorithm
```python
def insert(self, word):
    node = self.root

    for char in word:
        if char not in node.children:
            node.children[char] = TrieNode()
        node = node.children[char]
        # Optional: increment count for frequency

    node.is_end = True
```

### Complexity
- **Time:** O(m)
- **Space:** O(m) for new nodes

---

## 3. Search Operation

### Problem
Check if word exists in trie.

### Algorithm
```python
def search(self, word):
    node = self.root

    for char in word:
        if char not in node.children:
            return False
        node = node.children[char]

    return node.is_end
```

### Complexity
- **Time:** O(m)
- **Space:** O(1)

---

## 4. Starts With (Prefix Search)

### Problem
Check if any word starts with prefix.

### Algorithm
```python
def starts_with(self, prefix):
    node = self.root

    for char in prefix:
        if char not in node.children:
            return False
        node = node.children[char]

    return True
```

### Complexity
- **Time:** O(m)
- **Space:** O(1)

---

## 5. Delete Operation

### Problem
Remove word from trie.

### Algorithm
```python
def delete(self, word):
    def _delete(node, word, depth):
        if depth == len(word):
            if not node.is_end:
                return False  # Word doesn't exist
            node.is_end = False
            return len(node.children) == 0

        char = word[depth]
        if char not in node.children:
            return False

        should_delete = _delete(node.children[char], word, depth + 1)

        if should_delete:
            del node.children[char]
            return len(node.children) == 0 and not node.is_end

        return False

    _delete(self.root, word, 0)
```

### Complexity
- **Time:** O(m)
- **Space:** O(m) for recursion

---

## 6. Word Dictionary with Wildcard

### Problem
Search with '.' wildcard matching any character.

### Algorithm
```python
class WordDictionary:
    def __init__(self):
        self.root = TrieNode()

    def addWord(self, word):
        node = self.root
        for char in word:
            if char not in node.children:
                node.children[char] = TrieNode()
            node = node.children[char]
        node.is_end = True

    def search(self, word):
        def dfs(node, index):
            if index == len(word):
                return node.is_end

            char = word[index]
            if char != '.':
                if char not in node.children:
                    return False
                return dfs(node.children[char], index + 1)
            else:
                for child in node.children.values():
                    if dfs(child, index + 1):
                        return True
                return False

        return dfs(self.root, 0)
```

### Complexity
- **Add:** O(m)
- **Search:** O(m) without wildcards, O(26^m) worst case with wildcards

---

## 7. Implement Trie with Count

### Problem
Track number of words inserted and words with prefix.

### Algorithm
```python
class TrieWithCount:
    def __init__(self):
        self.root = {'count': 0}

    def insert(self, word):
        node = self.root
        for char in word:
            if char not in node:
                node[char] = {'count': 0}
            node = node[char]
            node['count'] += 1
        node['is_end'] = True

    def count_words_with_prefix(self, prefix):
        node = self.root
        for char in prefix:
            if char not in node:
                return 0
            node = node[char]
        return node.get('count', 0)
```

### Complexity
- **Insert:** O(m)
- **Count:** O(m)

---

## 8. Replace Words

### Problem
Replace words with their shortest root from dictionary.

### Algorithm
```python
def replace_words(dictionary, sentence):
    trie = {}
    for root in dictionary:
        node = trie
        for char in root:
            if char not in node:
                node[char] = {}
            node = node[char]
        node['#'] = root  # Mark end with root

    def replace(word):
        node = trie
        for i, char in enumerate(word):
            if '#' in node:
                return node['#']
            if char not in node:
                break
            node = node[char]
        return word

    return ' '.join(replace(word) for word in sentence.split())
```

### Complexity
- **Time:** O(n × m) where n = words, m = average length
- **Space:** O(dictionary size)

---

## 9. Longest Word in Dictionary

### Problem
Find longest word that can be built one character at a time.

### Algorithm
```python
def longest_word(words):
    trie = {}
    for word in words:
        node = trie
        for char in word:
            if char not in node:
                node[char] = {}
            node = node[char]
        node['#'] = word

    result = ""

    def dfs(node, path):
        nonlocal result
        if '#' in node:
            word = node['#']
            if len(word) > len(result) or (len(word) == len(result) and word < result):
                result = word

        for char in sorted(node.keys()):
            if char != '#' and '#' in node[char]:
                dfs(node[char], path + char)

    dfs(trie, "")
    return result
```

### Complexity
- **Time:** O(n × m)
- **Space:** O(n × m)
