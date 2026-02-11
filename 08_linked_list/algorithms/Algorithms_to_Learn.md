# Linked List - Algorithms to Learn

## 1. Reverse Linked List (Iterative and Recursive)

### Problem
Reverse a singly linked list.

### Algorithm (Iterative)
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

### Algorithm (Recursive)
```python
def reverse_list_recursive(head):
    if not head or not head.next:
        return head

    new_head = reverse_list_recursive(head.next)
    head.next.next = head
    head.next = None

    return new_head
```

### Complexity
- **Time:** O(n)
- **Space:** O(1) iterative, O(n) recursive

---

## 2. Detect Cycle (Floyd's Algorithm)

### Problem
Determine if linked list has a cycle.

### Algorithm
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

### Complexity
- **Time:** O(n)
- **Space:** O(1)

---

## 3. Find Cycle Start Node

### Problem
Return the node where cycle begins.

### Algorithm
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

### Complexity
- **Time:** O(n)
- **Space:** O(1)

---

## 4. Merge Two Sorted Lists

### Problem
Merge two sorted linked lists into one sorted list.

### Algorithm
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

### Complexity
- **Time:** O(n + m)
- **Space:** O(1)

---

## 5. Middle of Linked List

### Problem
Find the middle node of linked list.

### Algorithm
```python
def middle_node(head):
    slow = fast = head

    while fast and fast.next:
        slow = slow.next
        fast = fast.next.next

    return slow
```

### Complexity
- **Time:** O(n)
- **Space:** O(1)

---

## 6. Remove Nth Node From End

### Problem
Remove the nth node from end of list.

### Algorithm
```python
def remove_nth_from_end(head, n):
    dummy = ListNode(0, head)
    fast = slow = dummy

    # Move fast n+1 steps ahead
    for _ in range(n + 1):
        fast = fast.next

    # Move both until fast reaches end
    while fast:
        fast = fast.next
        slow = slow.next

    # Remove node
    slow.next = slow.next.next

    return dummy.next
```

### Complexity
- **Time:** O(n)
- **Space:** O(1)

---

## 7. Reorder Linked List

### Problem
Reorder list: L0 → Ln → L1 → Ln-1 → L2 → Ln-2 → ...

### Algorithm
```python
def reorder_list(head):
    if not head or not head.next:
        return

    # Find middle
    slow = fast = head
    while fast.next and fast.next.next:
        slow = slow.next
        fast = fast.next.next

    # Reverse second half
    second = slow.next
    slow.next = None
    prev = None
    while second:
        next_temp = second.next
        second.next = prev
        prev = second
        second = next_temp

    # Merge two halves
    first, second = head, prev
    while second:
        temp1, temp2 = first.next, second.next
        first.next = second
        second.next = temp1
        first, second = temp1, temp2
```

### Complexity
- **Time:** O(n)
- **Space:** O(1)

---

## 8. Palindrome Linked List

### Problem
Determine if linked list is a palindrome.

### Algorithm
```python
def is_palindrome(head):
    # Find middle
    slow = fast = head
    while fast and fast.next:
        slow = slow.next
        fast = fast.next.next

    # Reverse second half
    prev = None
    while slow:
        next_temp = slow.next
        slow.next = prev
        prev = slow
        slow = next_temp

    # Compare
    left, right = head, prev
    while right:
        if left.val != right.val:
            return False
        left = left.next
        right = right.next

    return True
```

### Complexity
- **Time:** O(n)
- **Space:** O(1)

---

## 9. Intersection of Two Linked Lists

### Problem
Find the node where two linked lists intersect.

### Algorithm
```python
def get_intersection_node(headA, headB):
    if not headA or not headB:
        return None

    pA, pB = headA, headB

    while pA != pB:
        pA = headB if not pA else pA.next
        pB = headA if not pB else pB.next

    return pA
```

### Complexity
- **Time:** O(n + m)
- **Space:** O(1)

### Key Insight
Two pointers traverse both lists. They meet at intersection or both become None.

---

## 10. Add Two Numbers

### Problem
Add two numbers represented as linked lists.

### Algorithm
```python
def add_two_numbers(l1, l2):
    dummy = ListNode(0)
    current = dummy
    carry = 0

    while l1 or l2 or carry:
        val1 = l1.val if l1 else 0
        val2 = l2.val if l2 else 0
        total = val1 + val2 + carry

        carry = total // 10
        current.next = ListNode(total % 10)
        current = current.next

        if l1:
            l1 = l1.next
        if l2:
            l2 = l2.next

    return dummy.next
```

### Complexity
- **Time:** O(max(m, n))
- **Space:** O(max(m, n))

---

## 11. Reverse Nodes in k-Group

### Problem
Reverse nodes in groups of k.

### Algorithm
```python
def reverse_k_group(head, k):
    def reverse(head, k):
        prev = None
        current = head
        while k > 0:
            next_temp = current.next
            current.next = prev
            prev = current
            current = next_temp
            k -= 1
        return prev

    def get_kth(node, k):
        while node and k > 0:
            node = node.next
            k -= 1
        return node

    dummy = ListNode(0, head)
    prev_group = dummy

    while True:
        kth = get_kth(prev_group, k)
        if not kth:
            break

        next_group = kth.next
        # Reverse group
        prev, curr = kth.next, prev_group.next
        while curr != next_group:
            temp = curr.next
            curr.next = prev
            prev = curr
            curr = temp

        temp = prev_group.next
        prev_group.next = kth
        prev_group = temp

    return dummy.next
```

### Complexity
- **Time:** O(n)
- **Space:** O(1)

---

## 12. Rotate List

### Problem
Rotate list to right by k places.

### Algorithm
```python
def rotate_right(head, k):
    if not head or not head.next or k == 0:
        return head

    # Find length and last node
    length = 1
    tail = head
    while tail.next:
        tail = tail.next
        length += 1

    k = k % length
    if k == 0:
        return head

    # Find new tail
    new_tail = head
    for _ in range(length - k - 1):
        new_tail = new_tail.next

    new_head = new_tail.next
    new_tail.next = None
    tail.next = head

    return new_head
```

### Complexity
- **Time:** O(n)
- **Space:** O(1)

---

## 13. Sort List

### Problem
Sort linked list in O(n log n) time.

### Algorithm
```python
def sort_list(head):
    if not head or not head.next:
        return head

    # Find middle
    slow, fast = head, head.next
    while fast and fast.next:
        slow = slow.next
        fast = fast.next.next

    mid = slow.next
    slow.next = None

    # Sort halves
    left = sort_list(head)
    right = sort_list(mid)

    # Merge
    return merge(left, right)

def merge(l1, l2):
    dummy = ListNode()
    tail = dummy

    while l1 and l2:
        if l1.val < l2.val:
            tail.next = l1
            l1 = l1.next
        else:
            tail.next = l2
            l2 = l2.next
        tail = tail.next

    tail.next = l1 if l1 else l2
    return dummy.next
```

### Complexity
- **Time:** O(n log n)
- **Space:** O(log n) for recursion

---

## 14. Copy List with Random Pointer

### Problem
Deep copy linked list with random pointer.

### Algorithm
```python
def copy_random_list(head):
    if not head:
        return None

    # Create copy nodes
    current = head
    while current:
        copy = Node(current.val, current.next, None)
        current.next = copy
        current = copy.next

    # Set random pointers
    current = head
    while current:
        if current.random:
            current.next.random = current.random.next
        current = current.next.next

    # Separate lists
    current = head
    copy_head = head.next
    while current:
        copy = current.next
        current.next = copy.next
        if copy.next:
            copy.next = copy.next.next
        current = current.next

    return copy_head
```

### Complexity
- **Time:** O(n)
- **Space:** O(1)

---

## 15. Remove Duplicates from Sorted List

### Problem
Remove duplicates from sorted list.

### Algorithm
```python
def delete_duplicates(head):
    current = head
    while current and current.next:
        if current.val == current.next.val:
            current.next = current.next.next
        else:
            current = current.next
    return head
```

### Complexity
- **Time:** O(n)
- **Space:** O(1)

---

## 16. Remove Duplicates II (Keep Only Distinct)

### Problem
Remove all nodes that have duplicates.

### Algorithm
```python
def delete_duplicates_ii(head):
    dummy = ListNode(0, head)
    prev = dummy

    while head:
        if head.next and head.val == head.next.val:
            while head.next and head.val == head.next.val:
                head = head.next
            prev.next = head.next
        else:
            prev = prev.next
        head = head.next

    return dummy.next
```

### Complexity
- **Time:** O(n)
- **Space:** O(1)

---

## 17. Partition List

### Problem
Partition list around value x.

### Algorithm
```python
def partition(head, x):
    less_head = less_tail = ListNode(0)
    greater_head = greater_tail = ListNode(0)

    while head:
        if head.val < x:
            less_tail.next = head
            less_tail = less_tail.next
        else:
            greater_tail.next = head
            greater_tail = greater_tail.next
        head = head.next

    greater_tail.next = None
    less_tail.next = greater_head.next

    return less_head.next
```

### Complexity
- **Time:** O(n)
- **Space:** O(1)

---

## 18. Reverse Linked List II

### Problem
Reverse between positions left and right.

### Algorithm
```python
def reverse_between(head, left, right):
    if not head or left == right:
        return head

    dummy = ListNode(0, head)
    prev = dummy

    for _ in range(left - 1):
        prev = prev.next

    current = prev.next

    for _ in range(right - left):
        next_node = current.next
        current.next = next_node.next
        next_node.next = prev.next
        prev.next = next_node

    return dummy.next
```

### Complexity
- **Time:** O(n)
- **Space:** O(1)

---

## 19. Odd Even Linked List

### Problem
Group odd-indexed then even-indexed nodes.

### Algorithm
```python
def odd_even_list(head):
    if not head or not head.next:
        return head

    odd = head
    even = head.next
    even_head = even

    while even and even.next:
        odd.next = even.next
        odd = odd.next
        even.next = odd.next
        even = even.next

    odd.next = even_head
    return head
```

### Complexity
- **Time:** O(n)
- **Space:** O(1)

---

## 20. Remove Nth Node From End

### Problem
Remove nth node from end.

### Algorithm
```python
def remove_nth_from_end(head, n):
    dummy = ListNode(0, head)
    fast = slow = dummy

    for _ in range(n):
        fast = fast.next

    while fast.next:
        fast = fast.next
        slow = slow.next

    slow.next = slow.next.next
    return dummy.next
```

### Complexity
- **Time:** O(n)
- **Space:** O(1)
