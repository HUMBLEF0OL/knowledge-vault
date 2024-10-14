---
tags:
  - Data-Structure
  - Binary-Tree
  - Tree
Date: 2024-10-12
Title: Dummy Title
References:
---
### 3. **Binary Search Tree (BST)**

---

#### 3.1 **Introduction to Binary Search Tree**

A **Binary Search Tree (BST)** is a special kind of **binary tree** that maintains a sorted order of its elements. In a BST, each node follows a specific property:

- **Left Subtree**: All nodes in the left subtree of a node must contain values **less than** the node's value.
- **Right Subtree**: All nodes in the right subtree of a node must contain values **greater than** the node's value.

This property allows **efficient searching, insertion, and deletion** operations, typically used in scenarios requiring dynamic sets of ordered data.

---

#### 3.2 **Properties of a Binary Search Tree**

1. **Sorted Structure**:
   - The left subtree of a node contains elements smaller than the node’s value.
   - The right subtree contains elements greater than the node’s value.
   
2. **Inorder Traversal**:
   - Performing an **inorder traversal** of a BST gives the elements in **sorted (ascending) order**.
   
3. **Uniqueness**:
   - In a typical BST, duplicate values are not allowed. However, variants exist where duplicates can be stored (e.g., counting the number of times a value appears).

---

#### 3.3 **Operations in a Binary Search Tree**

##### 3.3.1 **Search Operation**

- **Objective**: Find a specific value in the BST.
- **Time Complexity**: O(log n) for balanced trees, but can degrade to O(n) for unbalanced trees (like a skewed tree).
- **Approach**:
  - Start at the root.
  - If the value is less than the root, search the left subtree.
  - If the value is greater, search the right subtree.
  - If the value matches the root, return the node.

##### Example:
```java
public Node search(Node root, int key) {
    if (root == null || root.data == key) {
        return root;
    }
    if (key < root.data) {
        return search(root.left, key);
    }
    return search(root.right, key);
}
```

---

##### 3.3.2 **Insertion Operation**

- **Objective**: Insert a new value into the BST while maintaining its properties.
- **Time Complexity**: O(log n) for balanced trees, O(n) for unbalanced trees.
- **Approach**:
  - Start at the root and recursively find the correct position.
  - Insert the new value as a leaf node.

##### Example:
```java
public Node insert(Node root, int key) {
    if (root == null) {
        return new Node(key);
    }
    if (key < root.data) {
        root.left = insert(root.left, key);
    } else if (key > root.data) {
        root.right = insert(root.right, key);
    }
    return root;
}
```

---

##### 3.3.3 **Deletion Operation**

- **Objective**: Remove a node from the BST while maintaining its structure.
- **Time Complexity**: O(log n) for balanced trees, O(n) for unbalanced trees.
- **Approach**:
  - There are three possible cases for deletion:
    1. **Node with no children**: Simply remove the node.
    2. **Node with one child**: Remove the node and replace it with its child.
    3. **Node with two children**: Replace the node with its **inorder successor** (the smallest node in the right subtree) or **inorder predecessor** (the largest node in the left subtree), then recursively delete the successor or predecessor.

##### Example:
```java
public Node delete(Node root, int key) {
    if (root == null) {
        return null;
    }

    // Traverse to find the node to delete
    if (key < root.data) {
        root.left = delete(root.left, key);
    } else if (key > root.data) {
        root.right = delete(root.right, key);
    } else {
        // Node with only one child or no child
        if (root.left == null) {
            return root.right;
        } else if (root.right == null) {
            return root.left;
        }

        // Node with two children: Get inorder successor
        root.data = minValue(root.right);
        root.right = delete(root.right, root.data);
    }
    return root;
}

public int minValue(Node root) {
    int minVal = root.data;
    while (root.left != null) {
        minVal = root.left.data;
        root = root.left;
    }
    return minVal;
}
```

---

#### 3.4 **BST Traversals**

Traversal of a BST is the same as with any binary tree, but the **inorder traversal** of a BST gives the elements in **sorted order**.

##### Example Tree:
```
        50
       /  \
     30    70
    /  \   /  \
  20   40 60  80
```

- **Inorder** (Sorted Order): 20, 30, 40, 50, 60, 70, 80
- **Preorder**: 50, 30, 20, 40, 70, 60, 80
- **Postorder**: 20, 40, 30, 60, 80, 70, 50
- **Level Order**: 50, 30, 70, 20, 40, 60, 80

---

#### 3.5 **Performance and Complexity of BST**

| Operation  | Average Case Time Complexity | Worst Case Time Complexity |
|------------|------------------------------|----------------------------|
| **Search** | O(log n)                     | O(n)                       |
| **Insert** | O(log n)                     | O(n)                       |
| **Delete** | O(log n)                     | O(n)                       |
| **Space**  | O(n)                         | O(n)                       |

- **Average Case**: If the BST is balanced, all operations take O(log n) time.
- **Worst Case**: If the tree is unbalanced (e.g., a skewed tree), the time complexity degrades to O(n).

---

#### 3.6 **Balanced Binary Search Trees**

To overcome the issue of unbalanced BSTs (where performance degrades), there are self-balancing trees:
1. **AVL Tree**: Ensures that the heights of the left and right subtrees differ by at most one.
2. **Red-Black Tree**: A balanced BST that guarantees the tree remains balanced after insertions and deletions.

Both types of balanced BSTs maintain O(log n) time complexity for all operations.

---

#### 3.7 **Applications of Binary Search Trees**

1. **Search Algorithms**: BSTs are used in search-based applications where sorted data is required.
2. **Database Indexing**: Self-balancing BSTs like AVL and Red-Black trees are used in database indexing to maintain fast search, insert, and delete operations.
3. **Dictionary/Set Implementations**: Many programming languages use balanced BSTs to implement ordered collections (e.g., Java’s `TreeSet`, `TreeMap`).
4. **Network Routing Algorithms**: Used in routing table algorithms to find paths efficiently.

---

### Summary of Binary Search Trees (BSTs):

- **BST**: A binary tree where the left subtree contains values smaller than the root, and the right subtree contains values greater than the root.
- **Operations**: Search, Insert, Delete, and Traversals (Inorder, Preorder, Postorder, Level Order).
- **Complexity**: O(log n) in balanced trees but can degrade to O(n) in unbalanced trees.
- **Balanced BSTs**: AVL and Red-Black trees ensure O(log n) time complexity for all operations.
- **Applications**: Search algorithms, database indexing, dictionary/set implementations, and more.

---

This completes the detailed notes on **Binary Search Trees (BSTs)**. Next, we will cover **Generic Trees**. Let me know when you're ready to proceed!