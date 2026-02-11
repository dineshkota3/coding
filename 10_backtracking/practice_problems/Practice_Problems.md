# Backtracking - Practice Problems

## Easy Problems

### 1. Subsets
**LeetCode:** #78

**Description:**
Given an integer array nums, return all possible subsets (the power set). The solution set must not contain duplicate subsets.

**Example:**
```
Input: nums = [1, 2, 3]
Output: [[], [1], [2], [3], [1,2], [1,3], [2,3], [1,2,3]]
```

**Approach Hint:** At each element, choose to include or exclude it.

---

### 2. Subsets II
**LeetCode:** #90

**Description:**
Given an integer array nums that may contain duplicates, return all possible subsets without duplicate subsets.

**Example:**
```
Input: nums = [1, 2, 2]
Output: [[], [1], [2], [1,2], [2,2], [1,2,2]]
```

**Approach Hint:** Sort and skip duplicates when i > start.

---

## Medium Problems

### 3. Permutations
**LeetCode:** #46

**Description:**
Given an array nums of distinct integers, return all possible permutations.

**Example:**
```
Input: nums = [1, 2, 3]
Output: [[1,2,3], [1,3,2], [2,1,3], [2,3,1], [3,1,2], [3,2,1]]
```

**Approach Hint:** Swap elements or use visited array.

---

### 4. Permutations II
**LeetCode:** #47

**Description:**
Given a collection of numbers that may contain duplicates, return all possible unique permutations.

**Example:**
```
Input: nums = [1, 1, 2]
Output: [[1,1,2], [1,2,1], [2,1,1]]
```

**Approach Hint:** Sort, use visited array, skip duplicates.

---

### 5. Combination Sum
**LeetCode:** #39

**Description:**
Find all unique combinations of candidates that sum to target. The same number may be chosen unlimited times.

**Example:**
```
Input: candidates = [2, 3, 6, 7], target = 7
Output: [[2,2,3], [7]]
```

**Approach Hint:** Backtrack with index to avoid duplicates.

---

### 6. Combination Sum II
**LeetCode:** #40

**Description:**
Find all unique combinations that sum to target. Each number used at most once.

**Example:**
```
Input: candidates = [10, 1, 2, 7, 6, 1, 5], target = 8
Output: [[1,1,6], [1,2,5], [1,7], [2,6]]
```

**Approach Hint:** Sort, skip duplicates, increment index.

---

### 7. Palindrome Partitioning
**LeetCode:** #131

**Description:**
Given a string s, partition s such that every substring is a palindrome. Return all possible partitions.

**Example:**
```
Input: s = "aab"
Output: [["a","a","b"], ["aa","b"]]
```

**Approach Hint:** Try all possible substrings, check palindrome.

---

### 8. Generate Parentheses
**LeetCode:** #22

**Description:**
Given n pairs of parentheses, generate all combinations of well-formed parentheses.

**Example:**
```
Input: n = 3
Output: ["((()))", "(()())", "(())()", "()(())", "()()()"]
```

**Approach Hint:** Track open/close counts, add ')' only when close < open.

---

### 9. Letter Combinations of a Phone Number
**LeetCode:** #17

**Description:**
Given a string of digits, return all possible letter combinations.

**Example:**
```
Input: digits = "23"
Output: ["ad","ae","af","bd","be","bf","cd","ce","cf"]
```

**Approach Hint:** Map digits to letters, build combinations recursively.

---

### 10. Word Search
**LeetCode:** #79

**Description:**
Given an m x n board and a word, determine if the word exists in the grid.

**Example:**
```
Input: board = [["A","B","C","E"],["S","F","C","S"],["A","D","E","E"]], word = "ABCCED"
Output: true
```

**Approach Hint:** DFS with backtracking, mark and unmark visited.

---

## Hard Problems

### 11. N-Queens
**LeetCode:** #51

**Description:**
Place n queens on an n×n chessboard so no two queens attack each other.

**Example:**
```
Input: n = 4
Output: [[".Q..","...Q","Q...","..Q."],["..Q.","Q...","...Q",".Q.."]]
```

**Approach Hint:** Backtrack by rows, check column and diagonal conflicts.

---

### 12. Sudoku Solver
**LeetCode:** #37

**Description:**
Solve a 9×9 Sudoku board by filling empty cells.

**Example:**
```
Input: board with some cells filled, others '.'
Output: Solved board
```

**Approach Hint:** Find empty cell, try 1-9, check validity, backtrack.

---

## Additional Practice

### Combinations (Medium) - #77
Return all combinations of k numbers from 1 to n.

### Restore IP Addresses (Medium) - #93
Generate valid IP addresses from string.

### Split a String Into the Max Number of Unique Substrings (Medium) - #1593
Maximize unique substrings.

### Beautiful Arrangement (Medium) - #526
Count beautiful arrangements.

### Increasing Subsequences (Medium) - #491
Find all increasing subsequences.

### Word Search II (Hard) - #212
Find all words from dictionary in board.

### Expression Add Operators (Hard) - #282
Add operators to form target.

### Remove Invalid Parentheses (Hard) - #301
Remove minimum parentheses to make valid.

---

## Problem-Solving Tips

1. **Template for backtracking:**
   ```python
   def backtrack(state, choices):
       if is_complete(state):
           save(state)
           return

       for choice in choices:
           if is_valid(choice):
               make_choice(choice)
               backtrack(next_state)
               undo_choice(choice)
   ```

2. **Pruning strategies:**
   - Check validity early
   - Skip duplicates
   - Bound by remaining/limit
   - Sort and skip impossible paths

3. **Common optimizations:**
   - Sort input for duplicate handling
   - Use visited array for permutations
   - Pass remaining instead of recalculating
   - Early termination when invalid

4. **Edge cases:**
   - Empty input
   - Single element
   - All duplicates
   - No solution exists
