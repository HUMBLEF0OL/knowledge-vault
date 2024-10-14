---
tags:
  - Data-Structure
  - Tree
  - Binary-Tree
Date: 2024-10-14
Title: Binary Tree
References:
---
### 2. **Binary Tree**

---

#### 2.1 **Introduction to Binary Tree**

A **Binary Tree** is a special type of tree where each node has **at most two children**, referred to as the **left child** and **right child**. The binary tree is one of the most commonly used tree structures and forms the basis of more advanced trees such as Binary Search Trees, AVL Trees, and Heaps.

##### Characteristics of a Binary Tree:
- **Maximum Degree**: Each node has at most two children.
- **Left and Right Subtrees**: Each node has a left and right subtree.
- **Depth**: The number of edges from the root to a particular node.
- **Height**: The number of edges from the node to the deepest leaf.

---

#### 2.2 **Types of Binary Trees**

1. **Full Binary Tree**:
   - A binary tree where each node has either **0 or 2 children**. No node has only one child.
   
   ##### Example:
   ```
         A
        / \
       B   C
      / \
     D   E
   ```

2. **Complete Binary Tree**:
   - A binary tree in which all levels are completely filled except possibly the last, and the last level is filled from left to right.

   ##### Example:
   ```
         A
        / \
       B   C
      / \   \
     D   E   F
   ```

3. **Perfect Binary Tree**:
   - A binary tree in which all internal nodes have two children, and all leaf nodes are at the same level.
   
   ##### Example:
   ```
         A
        / \
       B   C
      / \ / \
     D  E F  G
   ```

4. **Balanced Binary Tree**:
   - A binary tree where the height difference between the left and right subtree of every node is at most 1. Commonly used in AVL and Red-Black Trees.
   
5. **Degenerate (Skewed) Tree**:
   - A binary tree where each parent node has only one child, leading to a structure similar to a linked list. It can be **left-skewed** or **right-skewed**.
   
   ##### Example (Right-Skewed):
   ```
     A
      \
       B
        \
         C
          \
           D
   ```

---

#### 2.3 **Properties of Binary Trees**

1. **Maximum Nodes at Level `l`**:
   - The maximum number of nodes at any level `l` of a binary tree is `2^l`.
   
2. **Maximum Nodes in a Binary Tree of Height `h`**:
   - The maximum number of nodes in a binary tree of height `h` is `2^(h+1) - 1`.
   
3. **Minimum Height of a Binary Tree with `n` Nodes**:
   - The minimum height (or minimum number of levels) of a binary tree with `n` nodes is `log2(n+1)`.
   
4. **Number of Leaf Nodes in a Full Binary Tree**:
   - A full binary tree with `n` internal nodes has `n + 1` leaf nodes.

5. **Height of a Perfect Binary Tree**:
   - The height of a perfect binary tree with `n` nodes is `log2(n + 1) - 1`.

---

#### 2.4 **Binary Tree Representation**

Binary trees can be represented in multiple ways:

1. **Linked Representation**:
   Each node in a binary tree is represented by an object with pointers to its `left` and `right` children.

   ##### Example in Java:
   ```java
   class Node {
       int data;
       Node left, right;

       public Node(int data) {
           this.data = data;
           left = right = null;
       }
   }
   ```

2. **Array Representation**:
   A binary tree can be represented as an array where:
   - The **root** is at index 0.
   - For any node at index `i`, the **left child** is at `2*i + 1` and the **right child** is at `2*i + 2`.
   - The **parent** of any node at index `i` is at `(i-1) / 2`.
   
   ##### Example:
   For the tree:
   ```
        A
       / \
      B   C
   ```
   The array representation is: `['A', 'B', 'C']`

---

#### 2.5 **Binary Tree Traversals**

There are four primary ways to traverse a binary tree:

1. **Preorder Traversal** (Root → Left → Right):
   - Visit the root node first, then recursively visit the left subtree, followed by the right subtree.
   
   ##### Example:
   ```
        A
       / \
      B   C
     / \
    D   E
   ```
   - Preorder: A, B, D, E, C

   ##### Code:
   ```java
   public void preorder(Node node) {
       if (node == null) return;
       System.out.print(node.data + " ");
       preorder(node.left);
       preorder(node.right);
   }
   ```

2. **Inorder Traversal** (Left → Root → Right):
   - Recursively visit the left subtree, then the root, and finally the right subtree. This traversal visits the nodes in **sorted order** for binary search trees.
   
   ##### Example:
   ```
        A
       / \
      B   C
     / \
    D   E
   ```
   - Inorder: D, B, E, A, C

   ##### Code:
   ```java
   public void inorder(Node node) {
       if (node == null) return;
       inorder(node.left);
       System.out.print(node.data + " ");
       inorder(node.right);
   }
   ```

3. **Postorder Traversal** (Left → Right → Root):
   - Recursively visit the left subtree, the right subtree, and finally the root.
   
   ##### Example:
   ```
        A
       / \
      B   C
     / \
    D   E
   ```
   - Postorder: D, E, B, C, A

   ##### Code:
   ```java
   public void postorder(Node node) {
       if (node == null) return;
       postorder(node.left);
       postorder(node.right);
       System.out.print(node.data + " ");
   }
   ```

4. **Level Order Traversal** (Breadth-First Traversal):
   - Visit nodes level by level, starting from the root and moving to the deepest level.
   - Typically implemented using a queue.
   
   ##### Example:
   ```
        A
       / \
      B   C
     / \
    D   E
   ```
   - Level Order: A, B, C, D, E

   ##### Code:
   ```java
   public void levelOrder(Node root) {
       if (root == null) return;
       Queue<Node> queue = new LinkedList<>();
       queue.add(root);
       while (!queue.isEmpty()) {
           Node temp = queue.poll();
           System.out.print(temp.data + " ");
           if (temp.left != null) queue.add(temp.left);
           if (temp.right != null) queue.add(temp.right);
       }
   }
   ```

---

#### 2.6 **Applications of Binary Trees**

1. **Expression Trees**:
   - Used in compilers to represent arithmetic expressions. Internal nodes represent operators, and leaf nodes represent operands.
   
2. **Huffman Coding Trees**:
   - Used in data compression algorithms like Huffman coding to represent variable-length codes.
   
3. **Binary Heaps**:
   - Implemented as binary trees to support efficient access to the minimum or maximum element (used in priority queues).
   
4. **Binary Search Trees**:
   - A special kind of binary tree used for efficient searching, insertion, and deletion of elements.

---

### Summary of Binary Trees:

- **Binary Tree**: A hierarchical data structure where each node has at most two children (left and right).
- **Types**: Full, Complete, Perfect, Balanced, Skewed Trees.
- **Traversals**: Preorder, Inorder, Postorder, and Level Order.
- **Applications**: Expression evaluation, Huffman coding, priority queues, and binary search trees.

---

This completes the detailed notes on **Binary Trees**. Next, we will cover **Binary Search Trees (BSTs)**. Let me know if you'd like to proceed!