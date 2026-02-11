# Tree - Algorithms to Learn

## 1. Inorder Traversal

### Problem
Traverse tree in left-root-right order.

### Algorithm (Recursive)
```python
def inorder_traversal(root):
    result = []

    def inorder(node):
        if node:
            inorder(node.left)
            result.append(node.val)
            inorder(node.right)

    inorder(root)
    return result
```

### Algorithm (Iterative)
```python
def inorder_traversal(root):
    result = []
    stack = []
    current = root

    while current or stack:
        while current:
            stack.append(current)
            current = current.left
        current = stack.pop()
        result.append(current.val)
        current = current.right

    return result
```

### Complexity
- **Time:** O(n)
- **Space:** O(h)

---

## 2. Preorder Traversal

### Problem
Traverse tree in root-left-right order.

### Algorithm (Recursive)
```python
def preorder_traversal(root):
    result = []

    def preorder(node):
        if node:
            result.append(node.val)
            preorder(node.left)
            preorder(node.right)

    preorder(root)
    return result
```

### Algorithm (Iterative)
```python
def preorder_traversal(root):
    if not root:
        return []

    result = []
    stack = [root]

    while stack:
        node = stack.pop()
        result.append(node.val)
        if node.right:
            stack.append(node.right)
        if node.left:
            stack.append(node.left)

    return result
```

### Complexity
- **Time:** O(n)
- **Space:** O(h)

---

## 3. Postorder Traversal

### Problem
Traverse tree in left-right-root order.

### Algorithm (Recursive)
```python
def postorder_traversal(root):
    result = []

    def postorder(node):
        if node:
            postorder(node.left)
            postorder(node.right)
            result.append(node.val)

    postorder(root)
    return result
```

### Algorithm (Iterative)
```python
def postorder_traversal(root):
    if not root:
        return []

    result = []
    stack = [root]

    while stack:
        node = stack.pop()
        result.append(node.val)
        if node.left:
            stack.append(node.left)
        if node.right:
            stack.append(node.right)

    return result[::-1]
```

### Complexity
- **Time:** O(n)
- **Space:** O(h)

---

## 4. Level Order Traversal (BFS)

### Problem
Traverse tree level by level.

### Algorithm
```python
from collections import deque

def level_order(root):
    if not root:
        return []

    result = []
    queue = deque([root])

    while queue:
        level = []
        for _ in range(len(queue)):
            node = queue.popleft()
            level.append(node.val)
            if node.left:
                queue.append(node.left)
            if node.right:
                queue.append(node.right)
        result.append(level)

    return result
```

### Complexity
- **Time:** O(n)
- **Space:** O(w) where w is max width

---

## 5. Maximum Depth of Binary Tree

### Problem
Find the maximum depth of binary tree.

### Algorithm
```python
def max_depth(root):
    if not root:
        return 0
    return 1 + max(max_depth(root.left), max_depth(root.right))

# Iterative (BFS)
def max_depth_bfs(root):
    if not root:
        return 0

    depth = 0
    queue = deque([root])

    while queue:
        depth += 1
        for _ in range(len(queue)):
            node = queue.popleft()
            if node.left:
                queue.append(node.left)
            if node.right:
                queue.append(node.right)

    return depth
```

### Complexity
- **Time:** O(n)
- **Space:** O(h) recursive, O(w) BFS

---

## 6. Check if Binary Tree is Balanced

### Problem
Determine if tree is height-balanced (height diff of subtrees ≤ 1).

### Algorithm
```python
def is_balanced(root):
    def check(node):
        if not node:
            return 0

        left = check(node.left)
        if left == -1:
            return -1

        right = check(node.right)
        if right == -1:
            return -1

        if abs(left - right) > 1:
            return -1

        return 1 + max(left, right)

    return check(root) != -1
```

### Complexity
- **Time:** O(n)
- **Space:** O(h)

---

## 7. Lowest Common Ancestor

### Problem
Find lowest common ancestor of two nodes.

### Algorithm
```python
def lowest_common_ancestor(root, p, q):
    if not root or root == p or root == q:
        return root

    left = lowest_common_ancestor(root.left, p, q)
    right = lowest_common_ancestor(root.right, p, q)

    if left and right:
        return root
    return left if left else right
```

### Complexity
- **Time:** O(n)
- **Space:** O(h)

---

## 8. Serialize and Deserialize Binary Tree

### Problem
Convert tree to string and back.

### Algorithm
```python
class Codec:
    def serialize(self, root):
        if not root:
            return "null"

        return f"{root.val},{self.serialize(root.left)},{self.serialize(root.right)}"

    def deserialize(self, data):
        def build(nodes):
            val = next(nodes)
            if val == "null":
                return None

            node = TreeNode(int(val))
            node.left = build(nodes)
            node.right = build(nodes)
            return node

        nodes = iter(data.split(','))
        return build(nodes)
```

### Complexity
- **Time:** O(n)
- **Space:** O(n)

---

## 9. Path Sum

### Problem
Find if root-to-leaf path sums to target.

### Algorithm
```python
def has_path_sum(root, target_sum):
    if not root:
        return False

    if not root.left and not root.right:
        return root.val == target_sum

    remaining = target_sum - root.val
    return (has_path_sum(root.left, remaining) or
            has_path_sum(root.right, remaining))
```

### Complexity
- **Time:** O(n)
- **Space:** O(h)

---

## 10. Invert Binary Tree

### Problem
Mirror the binary tree.

### Algorithm
```python
def invert_tree(root):
    if not root:
        return None

    root.left, root.right = root.right, root.left
    invert_tree(root.left)
    invert_tree(root.right)

    return root
```

### Complexity
- **Time:** O(n)
- **Space:** O(h)

---

## 11. Symmetric Tree

### Problem
Check if tree is symmetric around center.

### Algorithm
```python
def is_symmetric(root):
    def is_mirror(left, right):
        if not left and not right:
            return True
        if not left or not right:
            return False

        return (left.val == right.val and
                is_mirror(left.left, right.right) and
                is_mirror(left.right, right.left))

    return is_mirror(root, root)
```

### Complexity
- **Time:** O(n)
- **Space:** O(h)

---

## 12. Path Sum II

### Problem
Find all root-to-leaf paths with given sum.

### Algorithm
```python
def path_sum(root, target):
    result = []

    def dfs(node, current_sum, path):
        if not node:
            return

        current_sum += node.val
        path.append(node.val)

        if not node.left and not node.right and current_sum == target:
            result.append(path[:])

        dfs(node.left, current_sum, path)
        dfs(node.right, current_sum, path)

        path.pop()

    dfs(root, 0, [])
    return result
```

### Complexity
- **Time:** O(n²) worst case
- **Space:** O(h)

---

## 13. Binary Tree Right Side View

### Problem
Return nodes visible from right side.

### Algorithm
```python
def right_side_view(root):
    if not root:
        return []

    result = []
    queue = deque([root])

    while queue:
        level_size = len(queue)
        for i in range(level_size):
            node = queue.popleft()
            if i == level_size - 1:
                result.append(node.val)
            if node.left:
                queue.append(node.left)
            if node.right:
                queue.append(node.right)

    return result
```

### Complexity
- **Time:** O(n)
- **Space:** O(w)

---

## 14. Binary Tree Maximum Path Sum

### Problem
Find maximum path sum (path can start/end at any nodes).

### Algorithm
```python
def max_path_sum(root):
    max_sum = float('-inf')

    def dfs(node):
        nonlocal max_sum
        if not node:
            return 0

        left = max(0, dfs(node.left))
        right = max(0, dfs(node.right))

        # Path through this node as highest point
        max_sum = max(max_sum, node.val + left + right)

        # Return max path extending upward
        return node.val + max(left, right)

    dfs(root)
    return max_sum
```

### Complexity
- **Time:** O(n)
- **Space:** O(h)

---

## 15. Diameter of Binary Tree

### Problem
Find length of longest path between any two nodes.

### Algorithm
```python
def diameter_of_binary_tree(root):
    diameter = 0

    def depth(node):
        nonlocal diameter
        if not node:
            return 0

        left = depth(node.left)
        right = depth(node.right)

        diameter = max(diameter, left + right)

        return 1 + max(left, right)

    depth(root)
    return diameter
```

### Complexity
- **Time:** O(n)
- **Space:** O(h)

---

## 16. Count Complete Tree Nodes

### Problem
Count nodes in complete binary tree in less than O(n).

### Algorithm
```python
def count_nodes(root):
    if not root:
        return 0

    def height_left(node):
        h = 0
        while node:
            h += 1
            node = node.left
        return h

    def height_right(node):
        h = 0
        while node:
            h += 1
            node = node.right
        return h

    left_h = height_left(root)
    right_h = height_right(root)

    if left_h == right_h:
        return (1 << left_h) - 1

    return 1 + count_nodes(root.left) + count_nodes(root.right)
```

### Complexity
- **Time:** O(log² n)
- **Space:** O(log n)

---

## 17. Construct Binary Tree from Preorder and Inorder

### Problem
Build tree from preorder and inorder traversals.

### Algorithm
```python
def build_tree(preorder, inorder):
    idx_map = {val: i for i, val in enumerate(inorder)}
    pre_idx = 0

    def build(left, right):
        nonlocal pre_idx
        if left > right:
            return None

        val = preorder[pre_idx]
        pre_idx += 1
        root = TreeNode(val)

        root.left = build(left, idx_map[val] - 1)
        root.right = build(idx_map[val] + 1, right)

        return root

    return build(0, len(inorder) - 1)
```

### Complexity
- **Time:** O(n)
- **Space:** O(n)

---

## 18. Construct Binary Tree from Inorder and Postorder

### Problem
Build tree from inorder and postorder traversals.

### Algorithm
```python
def build_tree(inorder, postorder):
    idx_map = {val: i for i, val in enumerate(inorder)}
    post_idx = len(postorder) - 1

    def build(left, right):
        nonlocal post_idx
        if left > right:
            return None

        val = postorder[post_idx]
        post_idx -= 1
        root = TreeNode(val)

        root.right = build(idx_map[val] + 1, right)
        root.left = build(left, idx_map[val] - 1)

        return root

    return build(0, len(inorder) - 1)
```

### Complexity
- **Time:** O(n)
- **Space:** O(n)

---

## 19. Flatten Binary Tree to Linked List

### Problem
Flatten tree to linked list in preorder order.

### Algorithm
```python
def flatten(root):
    if not root:
        return

    flatten(root.left)
    flatten(root.right)

    # Save right subtree
    right = root.right

    # Move left to right
    root.right = root.left
    root.left = None

    # Find end and attach saved right
    current = root
    while current.right:
        current = current.right
    current.right = right
```

### Complexity
- **Time:** O(n)
- **Space:** O(h)

---

## 20. Sum Root to Leaf Numbers

### Problem
Sum all root-to-leaf numbers.

### Algorithm
```python
def sum_numbers(root):
    def dfs(node, current_sum):
        if not node:
            return 0

        current_sum = current_sum * 10 + node.val

        if not node.left and not node.right:
            return current_sum

        return dfs(node.left, current_sum) + dfs(node.right, current_sum)

    return dfs(root, 0)
```

### Complexity
- **Time:** O(n)
- **Space:** O(h)

---

## 21. Populating Next Right Pointers

### Problem
Connect each node to its right neighbor.

### Algorithm
```python
def connect(root):
    if not root:
        return None

    leftmost = root

    while leftmost.left:
        head = leftmost
        while head:
            head.left.next = head.right
            if head.next:
                head.right.next = head.next.left
            head = head.next
        leftmost = leftmost.left

    return root
```

### Complexity
- **Time:** O(n)
- **Space:** O(1)

---

## 22. House Robber III

### Problem
Maximum money without robbing adjacent nodes.

### Algorithm
```python
def rob(root):
    def dfs(node):
        if not node:
            return (0, 0)

        left = dfs(node.left)
        right = dfs(node.right)

        # (rob_this, dont_rob_this)
        rob = node.val + left[1] + right[1]
        dont_rob = max(left) + max(right)

        return (rob, dont_rob)

    return max(dfs(root))
```

### Complexity
- **Time:** O(n)
- **Space:** O(h)

---

## 23. Find Distance K from Target

### Problem
Find all nodes at distance K from target.

### Algorithm
```python
def distance_k(root, target, k):
    # Build parent map
    parent = {}

    def build_parent(node, par):
        if node:
            parent[node] = par
            build_parent(node.left, node)
            build_parent(node.right, node)

    build_parent(root, None)

    # BFS from target
    result = []
    visited = set()
    queue = deque([(target, 0)])
    visited.add(target)

    while queue:
        node, dist = queue.popleft()

        if dist == k:
            result.append(node.val)
            continue

        for neighbor in [node.left, node.right, parent[node]]:
            if neighbor and neighbor not in visited:
                visited.add(neighbor)
                queue.append((neighbor, dist + 1))

    return result
```

### Complexity
- **Time:** O(n)
- **Space:** O(n)

---

## 24. Minimum Depth of Binary Tree

### Problem
Find minimum depth to leaf.

### Algorithm
```python
def min_depth(root):
    if not root:
        return 0

    if not root.left:
        return 1 + min_depth(root.right)
    if not root.right:
        return 1 + min_depth(root.left)

    return 1 + min(min_depth(root.left), min_depth(root.right))

# BFS approach
def min_depth_bfs(root):
    if not root:
        return 0

    queue = deque([(root, 1)])

    while queue:
        node, depth = queue.popleft()

        if not node.left and not node.right:
            return depth

        if node.left:
            queue.append((node.left, depth + 1))
        if node.right:
            queue.append((node.right, depth + 1))
```

### Complexity
- **Time:** O(n)
- **Space:** O(h) or O(w) for BFS
