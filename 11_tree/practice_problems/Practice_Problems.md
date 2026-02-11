# Tree - Practice Problems

## Easy Problems

### 1. Maximum Depth of Binary Tree
**LeetCode:** #104

**Description:**
Given the root of a binary tree, return its maximum depth.

**Example:**
```
Input: root = [3, 9, 20, null, null, 15, 7]
Output: 3
```

**Approach Hint:** Recursively return 1 + max(left_depth, right_depth).

---

### 2. Invert Binary Tree
**LeetCode:** #226

**Description:**
Given the root of a binary tree, invert the tree (mirror it).

**Example:**
```
Input: root = [4, 2, 7, 1, 3, 6, 9]
Output: [4, 7, 2, 9, 6, 3, 1]
```

**Approach Hint:** Swap left and right children, recurse.

---

### 3. Symmetric Tree
**LeetCode:** #101

**Description:**
Given the root of a binary tree, check whether it is symmetric.

**Example:**
```
Input: root = [1, 2, 2, 3, 4, 4, 3]
Output: true
```

**Approach Hint:** Check if left subtree mirrors right subtree.

---

### 4. Path Sum
**LeetCode:** #112

**Description:**
Given root and targetSum, determine if root-to-leaf path sums to targetSum.

**Example:**
```
Input: root = [5, 4, 8, 11, null, 13, 4, 7, 2, null, null, null, 1], targetSum = 22
Output: true (5 + 4 + 11 + 2 = 22)
```

**Approach Hint:** Subtract node value from target, recurse until leaf.

---

### 5. Sum Root to Leaf Numbers
**LeetCode:** #129

**Description:**
Each root-to-leaf path forms a number. Return sum of all numbers.

**Example:**
```
Input: root = [1, 2, 3]
Output: 25 (12 + 13 = 25)
```

**Approach Hint:** Build number as you traverse: current_sum * 10 + node.val.

---

## Medium Problems

### 6. Binary Tree Right Side View
**LeetCode:** #199

**Description:**
Return values visible from right side (last node at each level).

**Example:**
```
Input: root = [1, 2, 3, null, 5, null, 4]
Output: [1, 3, 4]
```

**Approach Hint:** Level order, take last node of each level.

---

### 7. Flatten Binary Tree to Linked List
**LeetCode:** #114

**Description:**
Flatten tree to linked list in preorder order (in-place).

**Example:**
```
Input: root = [1, 2, 5, 3, 4, null, 6]
Output: [1, null, 2, null, 3, null, 4, null, 5, null, 6]
```

**Approach Hint:** Flatten left, flatten right, restructure.

---

### 8. Construct Binary Tree from Preorder and Inorder
**LeetCode:** #105

**Description:**
Construct tree from preorder and inorder traversal arrays.

**Example:**
```
Input: preorder = [3, 9, 20, 15, 7], inorder = [9, 3, 15, 20, 7]
Output: [3, 9, 20, null, null, 15, 7]
```

**Approach Hint:** First of preorder is root, find in inorder to split.

---

### 9. Construct Binary Tree from Inorder and Postorder
**LeetCode:** #106

**Description:**
Construct tree from inorder and postorder traversal arrays.

**Example:**
```
Input: inorder = [9, 3, 15, 20, 7], postorder = [9, 15, 7, 20, 3]
Output: [3, 9, 20, null, null, 15, 7]
```

**Approach Hint:** Last of postorder is root, find in inorder to split.

---

### 10. Lowest Common Ancestor of a Binary Tree
**LeetCode:** #236

**Description:**
Find lowest common ancestor of two nodes.

**Example:**
```
Input: root = [3, 5, 1, 6, 2, 0, 8, null, null, 7, 4], p = 5, q = 1
Output: 3
```

**Approach Hint:** If found in both subtrees, current is LCA.

---

### 11. Serialize and Deserialize Binary Tree
**LeetCode:** #297

**Description:**
Design algorithm to serialize and deserialize binary tree.

**Example:**
```
Input: root = [1, 2, 3, null, null, 4, 5]
Serialized: "1,2,null,null,3,4,null,null,5,null,null"
```

**Approach Hint:** Use preorder with null markers.

---

## Hard Problems

### 12. Binary Tree Maximum Path Sum
**LeetCode:** #124

**Description:**
Find maximum path sum where path can start and end at any nodes.

**Example:**
```
Input: root = [1, 2, 3]
Output: 6 (path: 2 → 1 → 3)
```

**Approach Hint:** At each node, compute max path through it, update global max.

---

## Additional Practice

### Same Tree (Easy) - #100
Check if two trees are identical.

### Subtree of Another Tree (Easy) - #572
Check if subtree.

### Minimum Depth of Binary Tree (Easy) - #111
Find minimum depth.

### Balanced Binary Tree (Easy) - #110
Check if balanced.

### Binary Tree Level Order Traversal (Medium) - #102
Level by level traversal.

### Binary Tree Zigzag Level Order Traversal (Medium) - #103
Zigzag traversal.

### Populating Next Right Pointers (Medium) - #116
Connect nodes at same level.

### Path Sum II (Medium) - #113
Find all root-to-leaf paths with target sum.

### Count Complete Tree Nodes (Medium) - #222
Count nodes in complete tree.

### Kth Smallest Element in a BST (Medium) - #230
Find kth smallest.

### House Robber III (Medium) - #337
Max money without robbing adjacent nodes.

---

## Problem-Solving Tips

1. **Traversal order matters:**
   - Inorder: sorted for BST
   - Preorder: good for copying
   - Postorder: good for deletion
   - Level order: BFS, level-by-level

2. **Common patterns:**
   - DFS for path problems
   - BFS for level problems
   - Bottom-up for subtree info
   - Top-down for path accumulation

3. **Recursive thinking:**
   - What's true for subtree?
   - How to combine children results?
   - What's base case?

4. **Edge cases:**
   - Empty tree
   - Single node
   - Only left/right children
   - Skewed tree
