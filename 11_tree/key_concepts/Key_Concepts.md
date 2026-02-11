# Tree - Key Concepts to Master

## 1. Tree Terminology

### Basic Terms
- **Root:** Topmost node
- **Leaf:** Node with no children
- **Parent/Child:** Direct relationship
- **Sibling:** Nodes with same parent
- **Depth:** Distance from root (root has depth 0)
- **Height:** Distance to deepest leaf (leaf has height 0)
- **Subtree:** Tree formed by any node and its descendants

### Binary Tree Types
- **Full:** Every node has 0 or 2 children
- **Complete:** All levels filled except possibly last (left to right)
- **Perfect:** All levels completely filled
- **Balanced:** Height difference of subtrees at most 1

## 2. Binary Tree Properties

### TreeNode Definition
```python
class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right
```

### Height vs Depth
```python
# Height (bottom-up)
def height(root):
    if not root:
        return -1
    return 1 + max(height(root.left), height(root.right))

# Depth (top-down, usually passed as parameter)
def depth(root, d=0):
    if not root:
        return
    print(f"Node {root.val} has depth {d}")
    depth(root.left, d + 1)
    depth(root.right, d + 1)
```

## 3. Tree Traversals

### Inorder (Left, Root, Right)
```python
# Recursive
def inorder(root):
    if root:
        inorder(root.left)
        print(root.val)
        inorder(root.right)

# Iterative
def inorder_iterative(root):
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

### Preorder (Root, Left, Right)
```python
# Recursive
def preorder(root):
    if root:
        print(root.val)
        preorder(root.left)
        preorder(root.right)

# Iterative
def preorder_iterative(root):
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

### Postorder (Left, Right, Root)
```python
# Recursive
def postorder(root):
    if root:
        postorder(root.left)
        postorder(root.right)
        print(root.val)

# Iterative
def postorder_iterative(root):
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

    return result[::-1]  # Reverse
```

### Level Order (BFS)
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

## 4. Tree Construction from Traversals

### From Preorder and Inorder
```python
def build_tree(preorder, inorder):
    if not preorder or not inorder:
        return None

    root_val = preorder[0]
    root = TreeNode(root_val)
    mid = inorder.index(root_val)

    root.left = build_tree(preorder[1:mid+1], inorder[:mid])
    root.right = build_tree(preorder[mid+1:], inorder[mid+1:])

    return root

# Optimized with hash map
def build_tree_optimized(preorder, inorder):
    idx_map = {val: i for i, val in enumerate(inorder)}
    pre_idx = 0

    def build(left, right):
        nonlocal pre_idx
        if left > right:
            return None

        root_val = preorder[pre_idx]
        root = TreeNode(root_val)
        pre_idx += 1

        mid = idx_map[root_val]
        root.left = build(left, mid - 1)
        root.right = build(mid + 1, right)

        return root

    return build(0, len(inorder) - 1)
```

## 5. Tree Properties

### Maximum Depth
```python
def max_depth(root):
    if not root:
        return 0
    return 1 + max(max_depth(root.left), max_depth(root.right))
```

### Check Balanced
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

### Lowest Common Ancestor
```python
def lca(root, p, q):
    if not root or root == p or root == q:
        return root

    left = lca(root.left, p, q)
    right = lca(root.right, p, q)

    if left and right:
        return root
    return left if left else right
```

## Time Complexity

| Operation | Time |
|-----------|------|
| Traversal | O(n) |
| Search (BST) | O(h) |
| Insert | O(h) |
| Delete | O(h) |
| Height | O(n) |

## Space Complexity
- Recursive: O(h) call stack
- Iterative: O(h) explicit stack
- Level order: O(w) where w is max width
