# Recursion - Practice Problems

## Easy Problems

### 1. Climbing Stairs
**LeetCode:** #70

**Description:**
You are climbing a staircase. It takes n steps to reach the top. Each time you can climb 1 or 2 steps. In how many distinct ways can you climb to the top?

**Example:**
```
Input: n = 3
Output: 3
Explanation: Three ways: 1+1+1, 1+2, 2+1
```

**Approach Hint:** Recursion with memoization: f(n) = f(n-1) + f(n-2).

---

### 2. Fibonacci Number
**LeetCode:** #509

**Description:**
Calculate the nth Fibonacci number.

**Example:**
```
Input: n = 4
Output: 3
Explanation: F(4) = F(3) + F(2) = 2 + 1 = 3
```

**Approach Hint:** Use memoization or DP for efficiency.

---

### 3. Power of Two
**LeetCode:** #231

**Description:**
Given an integer n, return true if it is a power of two.

**Example:**
```
Input: n = 16
Output: true
Explanation: 2^4 = 16
```

**Approach Hint:** Recursively divide by 2, or use bit manipulation.

---

### 4. Power of Three
**LeetCode:** #326

**Description:**
Given an integer n, return true if it is a power of three.

**Example:**
```
Input: n = 27
Output: true
```

**Approach Hint:** Recursively divide by 3, or use math.

---

## Medium Problems

### 5. Subsets (Power Set)
**LeetCode:** #78

**Description:**
Given an integer array nums, return all possible subsets (the power set).

**Example:**
```
Input: nums = [1, 2, 3]
Output: [[], [1], [2], [1,2], [3], [1,3], [2,3], [1,2,3]]
```

**Approach Hint:** Use backtracking to include/exclude each element.

---

### 6. Permutations
**LeetCode:** #46

**Description:**
Given an array nums of distinct integers, return all possible permutations.

**Example:**
```
Input: nums = [1, 2, 3]
Output: [[1,2,3], [1,3,2], [2,1,3], [2,3,1], [3,1,2], [3,2,1]]
```

**Approach Hint:** Swap elements and recurse, or use include/exclude pattern.

---

### 7. Generate Parentheses
**LeetCode:** #22

**Description:**
Given n pairs of parentheses, generate all combinations of well-formed parentheses.

**Example:**
```
Input: n = 3
Output: ["((()))", "(()())", "(())()", "()(())", "()()()"]
```

**Approach Hint:** Track open and close counts, add ')' only when close < open.

---

### 8. Letter Combinations of a Phone Number
**LeetCode:** #17

**Description:**
Given a string of digits, return all possible letter combinations.

**Example:**
```
Input: digits = "23"
Output: ["ad","ae","af","bd","be","bf","cd","ce","cf"]
```

**Approach Hint:** Recursively build combinations, each digit maps to 3-4 letters.

---

### 9. Word Search
**LeetCode:** #79

**Description:**
Given an m x n board and a word, determine if the word exists in the grid.

**Example:**
```
Input: board = [["A","B","C","E"],["S","F","C","S"],["A","D","E","E"]], word = "ABCCED"
Output: true
```

**Approach Hint:** DFS with backtracking, mark visited cells.

---

### 10. Pow(x, n)
**LeetCode:** #50

**Description:**
Implement pow(x, n), which calculates x raised to the power n.

**Example:**
```
Input: x = 2.00000, n = 10
Output: 1024.00000
```

**Approach Hint:** Use fast exponentiation: x^n = (x^(n/2))^2.

---

## Hard Problems

### 11. Kth Symbol in Grammar
**LeetCode:** #779

**Description:**
We build a table of n rows. First row is "0". Each subsequent row replaces 0 with "01" and 1 with "10". Find the kth symbol in nth row.

**Example:**
```
Input: n = 2, k = 1
Output: 0
Explanation:
Row 1: 0
Row 2: 01
```

**Approach Hint:** Recursively determine: parent determines child based on position.

---

## Additional Practice

### Reverse String (Easy) - #344
Recursively reverse string.

### Swap Nodes in Pairs (Medium) - #24
Recursively swap pairs.

### Reverse Linked List (Easy) - #206
Recursive reversal.

### Maximum Depth of Binary Tree (Easy) - #104
Recursive tree traversal.

### Same Tree (Easy) - #100
Recursively compare trees.

### Symmetric Tree (Easy) - #101
Recursively check symmetry.

### Path Sum (Easy) - #112
Recursively check path sum.

### Decode String (Medium) - #394
Recursively decode nested string.

### Flatten Binary Tree to Linked List (Medium) - #114
Recursively flatten.

### Validate Binary Search Tree (Medium) - #98
Recursively validate BST.

### Recover Binary Search Tree (Hard) - #99
Find and fix swapped nodes.

### N-Queens (Hard) - #51
Backtracking with recursion.

---

## Problem-Solving Tips

1. **Identify base cases:**
   - What's the smallest input?
   - When should recursion stop?
   - What's the direct answer?

2. **Design recursive case:**
   - How does problem break down?
   - How do subproblems combine?
   - What parameters change?

3. **Common patterns:**
   - Tree: left and right subtrees
   - Array: first element + rest
   - Number: n-1 or n/2
   - Grid: neighbors

4. **Optimization:**
   - Add memoization
   - Consider iterative solution
   - Watch for stack overflow

5. **Edge cases:**
   - Empty input
   - Single element
   - Already sorted/processed
