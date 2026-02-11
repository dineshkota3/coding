# BST - Key Concepts to Master

## 1. BST Property

### Definition
For every node:
- All values in left subtree < node value
- All values in right subtree > node value
- Both subtrees are also BSTs

### Implication
In-order traversal of BST gives sorted output.

```python
def inorder(root):
    if root:
        inorder(root.left)
        print(root.val)  # Sorted order
        inorder(root.right)
```

## 2. Search, Insert, Delete Operations

### Search
```python
def search(root, val):
    if not root or root.val == val:
        return root

    if val < root.val:
        return search(root.left, val)
    else:
        return search(root.right, val)
```

### Insert
```python
def insert(root, val):
    if not root:
        return TreeNode(val)

    if val < root.val:
        root.left = insert(root.left, val)
    else:
        root.right = insert(root.right, val)

    return root
```

### Delete
```python
def delete(root, val):
    if not root:
        return None

    if val < root.val:
        root.left = delete(root.left, val)
    elif val > root.val:
        root.right = delete(root.right, val)
    else:
        # Case 1: No child or one child
        if not root.left:
            return root.right
        if not root.right:
            return root.left

        # Case 2: Two children
        # Find inorder successor (smallest in right subtree)
        successor = find_min(root.right)
        root.val = successor.val
        root.right = delete(root.right, successor.val)

    return root

def find_min(root):
    while root.left:
        root = root.left
    return root
```

## 3. BST vs Sorted Array

| Operation | BST (balanced) | BST (skewed) | Sorted Array |
|-----------|----------------|--------------|--------------|
| Search | O(log n) | O(n) | O(log n) |
| Insert | O(log n) | O(n) | O(n) |
| Delete | O(log n) | O(n) | O(n) |
| Min/Max | O(log n) | O(n) | O(1) |
| Space | O(n) | O(n) | O(n) |

## 4. Validate BST

### Using Range
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

### Using Inorder
```python
def is_valid_bst_inorder(root):
    prev = float('-inf')

    def inorder(node):
        nonlocal prev
        if not node:
            return True

        if not inorder(node.left):
            return False

        if node.val <= prev:
            return False
        prev = node.val

        return inorder(node.right)

    return inorder(root)
```

## 5. Floor and Ceil

### Floor (largest value ≤ target)
```python
def floor(root, target):
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

### Ceil (smallest value ≥ target)
```python
def ceil(root, target):
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

## 6. Convert Sorted Array to BST

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

## 7. BST Iterator

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

## Time Complexity

| Operation | Balanced | Worst |
|-----------|----------|-------|
| Search | O(log n) | O(n) |
| Insert | O(log n) | O(n) |
| Delete | O(log n) | O(n) |
| Min/Max | O(log n) | O(n) |
| Successor | O(log n) | O(n) |

## Space Complexity
- O(h) for recursive operations
- O(h) for iterator
- O(n) for tree storage
