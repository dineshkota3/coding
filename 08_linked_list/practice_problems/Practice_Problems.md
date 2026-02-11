# Linked List - Practice Problems

## Easy Problems

### 1. Reverse Linked List
**LeetCode:** #206

**Description:**
Given the head of a singly linked list, reverse the list, and return the reversed list.

**Example:**
```
Input: head = [1, 2, 3, 4, 5]
Output: [5, 4, 3, 2, 1]
```

**Approach Hint:** Use iterative approach with prev, current pointers, or recursion.

---

### 2. Merge Two Sorted Lists
**LeetCode:** #21

**Description:**
Merge two sorted linked lists and return it as a sorted list.

**Example:**
```
Input: l1 = [1, 2, 4], l2 = [1, 3, 4]
Output: [1, 1, 2, 3, 4, 4]
```

**Approach Hint:** Use dummy node and compare values iteratively.

---

### 3. Linked List Cycle
**LeetCode:** #141

**Description:**
Given head of a linked list, determine if it has a cycle.

**Example:**
```
Input: head = [3, 2, 0, -4], pos = 1
Output: true
Explanation: There is a cycle at index 1.
```

**Approach Hint:** Use Floyd's cycle detection with slow and fast pointers.

---

### 4. Remove Nth Node From End of List
**LeetCode:** #19

**Description:**
Remove the nth node from the end of the list and return its head.

**Example:**
```
Input: head = [1, 2, 3, 4, 5], n = 2
Output: [1, 2, 3, 5]
```

**Approach Hint:** Use two pointers with n+1 gap.

---

### 5. Middle of the Linked List
**LeetCode:** #876

**Description:**
Given head of singly linked list, return the middle node.

**Example:**
```
Input: head = [1, 2, 3, 4, 5]
Output: [3, 4, 5]
Explanation: Middle node is node 3.
```

**Approach Hint:** Use fast-slow pointers.

---

## Medium Problems

### 6. Reorder List
**LeetCode:** #143

**Description:**
Reorder the list: L0 → Ln → L1 → Ln-1 → L2 → Ln-2 → ...

**Example:**
```
Input: head = [1, 2, 3, 4]
Output: [1, 4, 2, 3]
```

**Approach Hint:** Find middle, reverse second half, merge alternately.

---

### 7. Add Two Numbers
**LeetCode:** #2

**Description:**
Add two numbers represented by linked lists (digits stored in reverse order).

**Example:**
```
Input: l1 = [2, 4, 3], l2 = [5, 6, 4]
Output: [7, 0, 8]
Explanation: 342 + 465 = 807
```

**Approach Hint:** Iterate both lists, track carry.

---

### 8. Reverse Nodes in k-Group
**LeetCode:** #25

**Description:**
Reverse nodes in groups of k. If remaining < k, don't reverse.

**Example:**
```
Input: head = [1, 2, 3, 4, 5], k = 2
Output: [2, 1, 4, 3, 5]
```

**Approach Hint:** Count k nodes, reverse, recurse for rest.

---

### 9. Rotate List
**LeetCode:** #61

**Description:**
Rotate the list to the right by k places.

**Example:**
```
Input: head = [1, 2, 3, 4, 5], k = 2
Output: [4, 5, 1, 2, 3]
```

**Approach Hint:** Make circular, find new head, break.

---

### 10. Sort List
**LeetCode:** #148

**Description:**
Sort linked list in O(n log n) time and O(1) space.

**Example:**
```
Input: head = [4, 2, 1, 3]
Output: [1, 2, 3, 4]
```

**Approach Hint:** Use merge sort - find middle, sort halves, merge.

---

### 11. Palindrome Linked List
**LeetCode:** #234

**Description:**
Determine if linked list is a palindrome. O(n) time, O(1) space.

**Example:**
```
Input: head = [1, 2, 2, 1]
Output: true
```

**Approach Hint:** Find middle, reverse second half, compare.

---

## Hard Problems

### 12. Merge K Sorted Lists
**LeetCode:** #23

**Description:**
Merge k sorted linked lists into one sorted linked list.

**Example:**
```
Input: lists = [[1,4,5],[1,3,4],[2,6]]
Output: [1,1,2,3,4,4,5,6]
```

**Approach Hint:** Use min-heap or divide and conquer.

---

## Additional Practice

### Delete Node in a Linked List (Easy) - #237
Delete node when only given access to that node.

### Remove Linked List Elements (Easy) - #203
Remove all elements with given value.

### Intersection of Two Linked Lists (Easy) - #160
Find intersection node.

### Design Linked List (Easy) - #707
Implement linked list with add, delete, get operations.

### Odd Even Linked List (Medium) - #328
Group odd nodes then even nodes.

### Swap Nodes in Pairs (Medium) - #24
Swap every two adjacent nodes.

### Remove Duplicates from Sorted List II (Medium) - #82
Remove all duplicates (keep only distinct).

### Partition List (Medium) - #86
Partition around value x.

### Copy List with Random Pointer (Medium) - #138
Deep copy with random pointer.

### Reverse Linked List II (Medium) - #92
Reverse between positions left and right.

---

## Problem-Solving Tips

1. **Use dummy node:**
   - When head might change
   - Simplifies edge cases
   - Return `dummy.next`

2. **Fast-slow pointers:**
   - Find middle
   - Detect cycle
   - Find nth from end

3. **Common patterns:**
   - Reverse: prev, current, next
   - Merge: compare and advance
   - Two passes: count, then act

4. **Edge cases:**
   - Empty list
   - Single node
   - Two nodes
   - All same values
