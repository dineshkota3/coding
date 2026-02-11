# Linked List - Key Concepts to Master

## 1. Node Structure and Pointers

### Singly Linked List Node
```python
class ListNode:
    def __init__(self, val=0, next=None):
        self.val = val
        self.next = next
```

### Doubly Linked List Node
```python
class DoublyListNode:
    def __init__(self, val=0, prev=None, next=None):
        self.val = val
        self.prev = prev
        self.next = next
```

### Basic Operations
```python
# Create nodes
head = ListNode(1)
head.next = ListNode(2)
head.next.next = ListNode(3)

# Traverse
current = head
while current:
    print(current.val)
    current = current.next
```

## 2. Singly vs Doubly Linked List

| Feature | Singly | Doubly |
|---------|--------|--------|
| Memory | Less | More (extra pointer) |
| Traversal | Forward only | Both directions |
| Deletion | O(n) to find prev | O(1) with pointer |
| Insertion | Need prev | Direct |

## 3. Dummy Node Technique

### Why Use Dummy Node?
- Simplifies edge cases (empty list, single node)
- Avoids special handling for head modifications
- Returns `dummy.next` as new head

### Example: Remove Elements
```python
def remove_elements(head, val):
    dummy = ListNode(0)
    dummy.next = head
    current = dummy

    while current.next:
        if current.next.val == val:
            current.next = current.next.next
        else:
            current = current.next

    return dummy.next
```

## 4. Fast and Slow Pointers

### Find Middle Element
```python
def find_middle(head):
    slow = fast = head
    while fast and fast.next:
        slow = slow.next
        fast = fast.next.next
    return slow
```

### Detect Cycle (Floyd's Algorithm)
```python
def has_cycle(head):
    slow = fast = head

    while fast and fast.next:
        slow = slow.next
        fast = fast.next.next
        if slow == fast:
            return True

    return False
```

### Find Cycle Start
```python
def detect_cycle(head):
    slow = fast = head

    # Detect cycle
    while fast and fast.next:
        slow = slow.next
        fast = fast.next.next
        if slow == fast:
            break
    else:
        return None

    # Find cycle start
    slow = head
    while slow != fast:
        slow = slow.next
        fast = fast.next

    return slow
```

## 5. Reversing Linked Lists

### Iterative Reverse
```python
def reverse_list(head):
    prev = None
    current = head

    while current:
        next_temp = current.next
        current.next = prev
        prev = current
        current = next_temp

    return prev
```

### Recursive Reverse
```python
def reverse_list_recursive(head):
    if not head or not head.next:
        return head

    new_head = reverse_list_recursive(head.next)
    head.next.next = head
    head.next = None

    return new_head
```

### Reverse Sublist
```python
def reverse_between(head, left, right):
    dummy = ListNode(0, head)
    prev = dummy

    # Move to position before left
    for _ in range(left - 1):
        prev = prev.next

    # Reverse sublist
    current = prev.next
    for _ in range(right - left):
        next_node = current.next
        current.next = next_node.next
        next_node.next = prev.next
        prev.next = next_node

    return dummy.next
```

## 6. Merging Sorted Lists

### Merge Two Sorted Lists
```python
def merge_two_lists(l1, l2):
    dummy = ListNode(0)
    current = dummy

    while l1 and l2:
        if l1.val <= l2.val:
            current.next = l1
            l1 = l1.next
        else:
            current.next = l2
            l2 = l2.next
        current = current.next

    current.next = l1 if l1 else l2
    return dummy.next
```

## Common Patterns

| Pattern | Use Case |
|---------|----------|
| Dummy node | Head modifications |
| Fast-slow | Cycle, middle |
| Two pointers | Intersection, nth from end |
| Reverse | Palindrome, reorder |
| Merge | Sort, combine |

## Time Complexity

| Operation | Time | Space |
|-----------|------|-------|
| Access | O(n) | O(1) |
| Search | O(n) | O(1) |
| Insert at head | O(1) | O(1) |
| Insert at tail | O(n) | O(1) |
| Delete | O(n) | O(1) |
| Reverse | O(n) | O(1) |
| Detect cycle | O(n) | O(1) |
