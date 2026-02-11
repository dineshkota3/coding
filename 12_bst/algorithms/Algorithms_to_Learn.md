# BST - Algorithms to Learn

## 1. Search in BST

### Problem
Search for a value in BST.

### Algorithm
```python
def search_bst(root, val):
    if not root or root.val == val:
        return root

    if val < root.val:
        return search_bst(root.left, val)
    else:
        return search_bst(root.right, val)

# Iterative
def search_bst_iterative(root, val):
    while root and root.val != val:
        if val < root.val:
            root = root.left
        else:
            root = root.right
    return root
```

### Complexity
- **Time:** O(h) where h is height
- **Space:** O(h) recursive, O(1) iterative

---

## 2. Insert into BST

### Problem
Insert a value into BST.

### Algorithm
```python
def insert_into_bst(root, val):
    if not root:
        return TreeNode(val)

    if val < root.val:
        root.left = insert_into_bst(root.left, val)
    else:
        root.right = insert_into_bst(root.right, val)

    return root

# Iterative
def insert_into_bst_iterative(root, val):
    if not root:
        return TreeNode(val)

    current = root
    while True:
        if val < current.val:
            if not current.left:
                current.left = TreeNode(val)
                break
            current = current.left
        else:
            if not current.right:
                current.right = TreeNode(val)
                break
            current = current.right

    return root
```

### Complexity
- **Time:** O(h)
- **Space:** O(h) recursive, O(1) iterative

---

## 3. Delete from BST

### Problem
Delete a node from BST.

### Algorithm
```python
def delete_node(root, key):
    if not root:
        return None

    if key < root.val:
        root.left = delete_node(root.left, key)
    elif key > root.val:
        root.right = delete_node(root.right, key)
    else:
        # Found node to delete
        if not root.left:
            return root.right
        if not root.right:
            return root.left

        # Two children: replace with inorder successor
        successor = find_min(root.right)
        root.val = successor.val
        root.right = delete_node(root.right, successor.val)

    return root

def find_min(node):
    while node.left:
        node = node.left
    return node
```

### Complexity
- **Time:** O(h)
- **Space:** O(h)

---

## 4. Validate BST

### Problem
Determine if tree is a valid BST.

### Algorithm
```python
def is_valid_bst(root):
    def validate(node, low, high):
        if not node:
            return True

        if node.val <= low or node.val >= high:
            return False

        return (validate(node.left, low, node.val) and
                validate(node.right, node.val, high))

    return validate(root, float('-inf'), float('inf'))
```

### Complexity
- **Time:** O(n)
- **Space:** O(h)

---

## 5. Kth Smallest Element in BST

### Problem
Find kth smallest element in BST.

### Algorithm
```python
def kth_smallest(root, k):
    count = 0
    result = None

    def inorder(node):
        nonlocal count, result
        if not node or result is not None:
            return

        inorder(node.left)

        count += 1
        if count == k:
            result = node.val
            return

        inorder(node.right)

    inorder(root)
    return result

# Using stack (iterator approach)
def kth_smallest_iterative(root, k):
    stack = []
    current = root

    while True:
        while current:
            stack.append(current)
            current = current.left

        current = stack.pop()
        k -= 1
        if k == 0:
            return current.val

        current = current.right
```

### Complexity
- **Time:** O(h + k)
- **Space:** O(h)

---

## 6. Convert Sorted Array to BST

### Problem
Convert sorted array to height-balanced BST.

### Algorithm
```python
def sorted_array_to_bst(nums):
    def build(left, right):
        if left > right:
            return None

        mid = (left + right) // 2
        root = TreeNode(nums[mid])
        root.left = build(left, mid - 1)
        root.right = build(mid + 1, right)

        return root

    return build(0, len(nums) - 1)
```

### Complexity
- **Time:** O(n)
- **Space:** O(log n) for recursion

---

## 7. Floor in BST

### Problem
Find largest value ≤ target.

### Algorithm
```python
def floor_bst(root, target):
    result = None

    while root:
        if root.val == target:
            return root.val
        elif root.val > target:
            root = root.left
        else:
            result = root.val
            root = root.right

    return result
```

### Complexity
- **Time:** O(h)
- **Space:** O(1)

---

## 8. Ceil in BST

### Problem
Find smallest value ≥ target.

### Algorithm
```python
def ceil_bst(root, target):
    result = None

    while root:
        if root.val == target:
            return root.val
        elif root.val < target:
            root = root.right
        else:
            result = root.val
            root = root.left

    return result
```

### Complexity
- **Time:** O(h)
- **Space:** O(1)

---

## 9. Lowest Common Ancestor of BST

### Problem
Find LCA of two nodes in BST.

### Algorithm
```python
def lowest_common_ancestor(root, p, q):
    if p.val < root.val and q.val < root.val:
        return lowest_common_ancestor(root.left, p, q)
    if p.val > root.val and q.val > root.val:
        return lowest_common_ancestor(root.right, p, q)
    return root

# Iterative
def lca_iterative(root, p, q):
    while root:
        if p.val < root.val and q.val < root.val:
            root = root.left
        elif p.val > root.val and q.val > root.val:
            root = root.right
        else:
            return root
```

### Complexity
- **Time:** O(h)
- **Space:** O(h) recursive, O(1) iterative

---

## 10. BST Iterator

### Problem
Implement iterator over BST in-order.

### Algorithm
```python
class BSTIterator:
    def __init__(self, root):
        self.stack = []
        self._push_left(root)

    def _push_left(self, node):
        while node:
            self.stack.append(node)
            node = node.left

    def next(self):
        node = self.stack.pop()
        self._push_left(node.right)
        return node.val

    def hasNext(self):
        return len(self.stack) > 0
```

### Complexity
- **Time:** O(1) amortized for next/hasNext
- **Space:** O(h)
