# Trie - Key Concepts to Master

## 1. Trie Node Structure

### Basic Node
```python
class TrieNode:
    def __init__(self):
        self.children = {}  # or dict
        self.is_end = False  # Marks end of word
```

### With Count
```python
class TrieNode:
    def __init__(self):
        self.children = {}
        self.is_end = False
        self.count = 0  # Number of words through this node
```

## 2. Trie Properties

### Characteristics
- Root represents empty string
- Each edge represents a character
- Path from root to node = prefix
- Node marked is_end = complete word

### Example Trie
```
Words: ["car", "cat", "dog", "door"]

       root
      /    \
     c      d
     |      |
     a      o
    / \     |
   r   t    o
   |   |    |
  (E) (E)   r
            |
           (E)

(E) = end of word marker
```

## 3. Insert Operation

```python
def insert(self, word):
    node = self.root

    for char in word:
        if char not in node.children:
            node.children[char] = TrieNode()
        node = node.children[char]

    node.is_end = True
```

## 4. Search Operation

### Exact Match
```python
def search(self, word):
    node = self.root

    for char in word:
        if char not in node.children:
            return False
        node = node.children[char]

    return node.is_end
```

### Prefix Search
```python
def starts_with(self, prefix):
    node = self.root

    for char in prefix:
        if char not in node.children:
            return False
        node = node.children[char]

    return True
```

## 5. Delete Operation

```python
def delete(self, word):
    def _delete(node, word, index):
        if index == len(word):
            if not node.is_end:
                return False  # Word not found
            node.is_end = False
            return len(node.children) == 0  # Can delete if no children

        char = word[index]
        if char not in node.children:
            return False  # Word not found

        should_delete_child = _delete(node.children[char], word, index + 1)

        if should_delete_child:
            del node.children[char]
            return len(node.children) == 0 and not node.is_end

        return False

    _delete(self.root, word, 0)
```

## 6. Complete Trie Implementation

```python
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

## 7. Trie vs Hash Map

| Operation | Trie | Hash Map |
|-----------|------|----------|
| Insert | O(m) | O(m) |
| Search | O(m) | O(m) |
| Prefix search | O(m) | O(m × n) |
| Space (shared prefix) | Less | More |
| Space (no shared) | More | Less |

**m = word length, n = number of words**

## 8. Memory Optimization

### Compressed Trie (Radix Tree)
- Merge nodes with single child
- Store substrings on edges

### Ternary Search Tree
- Each node has 3 children
- Space efficient for sparse tries

### Using Array Instead of Dict
```python
class TrieNode:
    def __init__(self):
        self.children = [None] * 26  # For lowercase a-z
        self.is_end = False

    def get_index(self, char):
        return ord(char) - ord('a')
```

## 9. Common Applications

| Application | Use Case |
|-------------|----------|
| Autocomplete | Find words with prefix |
| Spell checker | Find similar words |
| IP routing | Longest prefix match |
| Word games | Find valid words |
| Search suggestions | Prefix matching |

## Time Complexity

| Operation | Time |
|-----------|------|
| Insert | O(m) |
| Search | O(m) |
| Delete | O(m) |
| Prefix search | O(m) |

**m = length of word/prefix**

## Space Complexity
- O(N × M) where N = number of words, M = average length
- Better with shared prefixes
- Worse when no shared prefixes
