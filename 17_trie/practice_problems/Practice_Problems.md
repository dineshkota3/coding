# Trie - Practice Problems

## Medium Problems

### 1. Implement Trie (Prefix Tree)
**LeetCode:** #208

**Description:**
Implement a trie with insert, search, and startsWith methods.

**Example:**
```
trie.insert("apple")
trie.search("apple") -> true
trie.search("app") -> false
trie.startsWith("app") -> true
trie.insert("app")
trie.search("app") -> true
```

**Approach Hint:** Build TrieNode class with children dict and is_end flag.

---

### 2. Design Add and Search Words Data Structure
**LeetCode:** #211

**Description:**
Design data structure that supports adding and searching words. Search can contain '.' wildcard.

**Example:**
```
wordDictionary.addWord("bad")
wordDictionary.addWord("dad")
wordDictionary.addWord("mad")
wordDictionary.search("pad") -> false
wordDictionary.search("bad") -> true
wordDictionary.search(".ad") -> true
wordDictionary.search("b..") -> true
```

**Approach Hint:** DFS when encountering wildcard.

---

### 3. Word Search II
**LeetCode:** #212

**Description:**
Given board and list of words, find all words from list that exist in board.

**Example:**
```
Input: board = [["o","a","a","n"],["e","t","a","e"],["i","h","k","r"],["i","f","l","v"]], words = ["oath","pea","eat","rain"]
Output: ["eat","oath"]
```

**Approach Hint:** Build trie from words, DFS on board with trie traversal.

---

### 4. Prefix and Suffix Search
**LeetCode:** #745

**Description:**
Design data structure to search words by prefix and suffix.

**Example:**
```
WordFilter(["apple"])
WordFilter.f("a", "e") -> 0 (word "apple" has prefix "a" and suffix "e")
```

**Approach Hint:** Store all suffix+separator+prefix combinations in trie.

---

### 5. Stream of Characters
**LeetCode:** #1032

**Description:**
Design data structure that accepts characters and checks if suffix forms word.

**Example:**
```
streamChecker = StreamChecker(["cd","f","kl"])
streamChecker.query('a') -> false
streamChecker.query('b') -> false
streamChecker.query('c') -> false
streamChecker.query('d') -> true (suffix "cd" is word)
```

**Approach Hint:** Build trie with reversed words, track current suffix.

---

### 6. Map Sum Pairs
**LeetCode:** #677

**Description:**
Insert key-value pairs, return sum of values for keys with given prefix.

**Example:**
```
mapSum.insert("apple", 3)
mapSum.sum("ap") -> 3
mapSum.insert("app", 2)
mapSum.sum("ap") -> 5
```

**Approach Hint:** Store values in trie nodes, DFS to sum all values under prefix.

---

### 7. Implement Magic Dictionary
**LeetCode:** #676

**Description:**
Check if word exists with exactly one character difference.

**Example:**
```
magicDictionary.buildDict(["hello", "leetcode"])
magicDictionary.search("hello") -> false
magicDictionary.search("hhllo") -> true (replace 'e' with 'h')
```

**Approach Hint:** Use trie, try replacing each character during search.

---

### 8. Concatenated Words
**LeetCode:** #472

**Description:**
Find all words that can be formed by concatenating other words.

**Example:**
```
Input: words = ["cat","cats","catsdogcats","dog","dogcatsdog","hippopotamuses","rat","ratcatdogcat"]
Output: ["catsdogcats","dogcatsdog","ratcatdogcat"]
```

**Approach Hint:** Build trie, DFS with memoization to check concatenation.

---

### 9. Replace Words
**LeetCode:** #648

**Description:**
Replace words with their shortest root from dictionary.

**Example:**
```
Input: dictionary = ["cat","bat","rat"], sentence = "the cattle was rattled by the battery"
Output: "the cat was rat by the bat"
```

**Approach Hint:** Build trie of roots, find shortest matching prefix.

---

### 10. Longest Word in Dictionary
**LeetCode:** #720

**Description:**
Find longest word that can be built one character at a time.

**Example:**
```
Input: words = ["w","wo","wor","worl","world"]
Output: "world"
```

**Approach Hint:** Build trie, DFS only to nodes that complete words.

---

## Hard Problems

### 11. Palindrome Pairs
**LeetCode:** #336

**Description:**
Find all pairs of words that concatenate to form palindrome.

**Example:**
```
Input: words = ["abcd","dcba","lls","s","sssll"]
Output: [[0,1],[1,0],[3,2],[2,4]]
```

**Approach Hint:** Use trie with reversed words, check palindrome conditions.

---

## Additional Practice

### Maximum XOR of Two Numbers (Medium) - #421
Use binary trie for XOR maximization.

### Word Squares (Hard) - #425
Build word squares using trie for prefix lookup.

### Short Encoding of Words (Medium) - #820
Find minimum encoding length using suffix trie.

### Search Suggestions System (Medium) - #1268
Return suggested products for search word.

### Add Bold Tag in String (Medium) - #616
Add bold tags for words from dictionary.

### Delete Operation for Two Strings (Medium) - #583
Can be optimized with trie for common prefix.

---

## Problem-Solving Tips

1. **Trie construction:**
   - Define node structure first
   - Use dict for flexibility
   - Mark end of words clearly

2. **Common patterns:**
   - Insert all words first
   - Traverse for search/operations
   - DFS for wildcard/complex search

3. **Optimizations:**
   - Store additional info in nodes
   - Use count for prefix counting
   - Reverse for suffix matching

4. **Edge cases:**
   - Empty trie
   - Empty word
   - Word not found
   - Prefix vs exact match

5. **When to use trie:**
   - Prefix matching required
   - Multiple string lookups
   - Autocomplete features
   - Shared prefixes (space efficient)
