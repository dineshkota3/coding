# BST - Practice Problems

## Easy Problems

### 1. Validate Binary Search Tree
**LeetCode:** #98

**Description:**
Given the root of a binary tree, determine if it is a valid BST.

**Example:**
```
Input: root = [2, 1, 3]
Output: true

Input: root = [5, 1, 4, null, null, 3, 6]
Output: false (3 < 5 but in right subtree)
```

**Approach Hint:** Use range validation or inorder traversal with previous tracking.

---

### 2. Lowest Common Ancestor of a BST
**LeetCode:** #235

**Description:**
Given BST and two nodes, find their lowest common ancestor.

**Example:**
```
Input: root = [6, 2, 8, 0, 4, 7, 9, null, null, 3, 5], p = 2, q = 8
Output: 6
```

**Approach Hint:** Use BST property: if both < root, go left; if both > root, go right.

---

### 3. Convert Sorted Array to Binary Search Tree
**LeetCode:** #108

**Description:**
Convert sorted array to height-balanced BST.

**Example:**
```
Input: nums = [-10, -3, 0, 5, 9]
Output: [0, -3, 9, -10, null, 5]
```

**Approach Hint:** Middle element is root, recursively build left and right.

---

### 4. Minimum Absolute Difference in BST
**LeetCode:** #530

**Description:**
Find minimum absolute difference between values of any two nodes.

**Example:**
```
Input: root = [4, 2, 6, 1, 3]
Output: 1
```

**Approach Hint:** In-order traversal gives sorted values, check adjacent.

---

### 5. Two Sum IV - Input is a BST
**LeetCode:** #653

**Description:**
Given BST and target, find if two elements sum to target.

**Example:**
```
Input: root = [5, 3, 6, 2, 4, null, 7], k = 9
Output: true (2 + 7 = 9)
```

**Approach Hint:** Use set while traversing, or two-pointer on sorted values.

---

## Medium Problems

### 6. Kth Smallest Element in a BST
**LeetCode:** #230

**Description:**
Find kth smallest element in BST.

**Example:**
```
Input: root = [3, 1, 4, null, 2], k = 1
Output: 1
```

**Approach Hint:** In-order traversal, count nodes until k.

---

### 7. Balanced Binary Tree
**LeetCode:** #110

**Description:**
Check if binary tree is height-balanced.

**Example:**
```
Input: root = [3, 9, 20, null, null, 15, 7]
Output: true
```

**Approach Hint:** Check height diff at each node, propagate -1 if unbalanced.

---

### 8. Binary Tree Maximum Path Sum
**LeetCode:** #124

**Description:**
Find maximum path sum where path can be any node to any node.

**Example:**
```
Input: root = [1, 2, 3]
Output: 6 (path: 2 → 1 → 3)
```

**Approach Hint:** At each node, max path through it = node + max(0, left) + max(0, right).

---

### 9. Binary Tree Level Order Traversal
**LeetCode:** #102

**Description:**
Return level order traversal as list of levels.

**Example:**
```
Input: root = [3, 9, 20, null, null, 15, 7]
Output: [[3], [9, 20], [15, 7]]
```

**Approach Hint:** BFS with queue, process level by level.

---

### 10. Convert BST to Sorted Doubly Linked List
**LeetCode:** #426

**Description:**
Convert BST to sorted circular doubly linked list in-place.

**Example:**
```
Input: root = [4, 2, 5, 1, 3]
Output: [1, 2, 3, 4, 5] as circular doubly linked list
```

**Approach Hint:** In-order traversal, connect prev and current.

---

## Hard Problems

### 11. Count of Smaller Numbers After Self
**LeetCode:** #315

**Description:**
For each element, count smaller elements to its right.

**Example:**
```
Input: nums = [5, 2, 6, 1]
Output: [2, 1, 1, 0]
```

**Approach Hint:** Build BST from right to left, count smaller during insert.

---

## Additional Practice

### Search in a Binary Search Tree (Easy) - #700
Search for value in BST.

### Insert into a Binary Search Tree (Medium) - #701
Insert value into BST.

### Delete Node in a BST (Medium) - #450
Delete node from BST.

### Closest Binary Search Tree Value (Easy) - #270
Find closest value to target.

### Mode in Binary Search Tree (Easy) - #501
Find most frequent value(s).

### Range Sum of BST (Easy) - #938
Sum of values in range.

### Trim a Binary Search Tree (Medium) - #669
Trim BST to given range.

### Serialize and Deserialize BST (Medium) - #449
Serialize/deserialize BST.

### Contains Duplicate III (Hard) - #220
BST approach for sliding window.

### Count of Range Sum (Hard) - #327
Count range sums using BST.

---

## Problem-Solving Tips

1. **BST Property:**
   - Left subtree < root < right subtree
   - In-order gives sorted values
   - Search/insert/delete: O(h)

2. **Validation:**
   - Use range (min, max) at each node
   - Or track previous in inorder

3. **Common patterns:**
   - In-order for sorted access
   - BST property for LCA
   - Iterative for iterator

4. **Optimization:**
   - Use iterative when possible
   - Balance tree for O(log n)
   - Augment tree for additional info

5. **Edge cases:**
   - Empty tree
   - Single node
   - Skewed tree (degrades to linked list)
   - Duplicate values (decide policy)
