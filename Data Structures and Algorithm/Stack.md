---
tags:
  - Data-Structure
Date: 2024-10-14
Title: Stack
References:
---
### 1. **Introduction to Stacks**

A **stack** is a linear data structure that operates on the **LIFO** (Last In, First Out) principle, meaning the last element added is the first one to be removed. This behavior is similar to stacking plates: you add plates to the top and remove the topmost plate first.

- **LIFO**: Last In, First Out.
- **Abstract Data Type (ADT)**: The stack defines operations without specifying their implementation.

---

### 2. **Key Operations**

| Operation    | Description                          | Time Complexity |
|--------------|--------------------------------------|-----------------|
| **Push**     | Adds an element to the top of the stack. | **O(1)** |
| **Pop**      | Removes the top element from the stack. | **O(1)** |
| **Top (Peek)** | Returns the top element without removing it. | **O(1)** |
| **Size**     | Returns the number of elements in the stack. | **O(1)** |
| **isEmpty**  | Checks if the stack is empty.            | **O(1)** |

- All operations run in **O(1)** time complexity, meaning their execution time does not depend on the size of the stack.

---

### 3. **Array-Based Stack Implementation**

In an **array-based stack**, elements are stored in an array. This implementation can suffer from **Stack Overflow** if the array is full, and resizing may be required for dynamic arrays.

```java
class StackUsingArray {
    int[] data;
    int nextIndex;
    int capacity;

    public StackUsingArray(int size) {
        data = new int[size];
        nextIndex = 0;
        capacity = size;
    }

    public void push(int element) {
        if (nextIndex == capacity) {
            System.out.println("Stack Overflow");
            return;
        }
        data[nextIndex++] = element;
    }

    public int pop() {
        if (isEmpty()) {
            System.out.println("Stack Underflow");
            return Integer.MIN_VALUE;
        }
        return data[--nextIndex];
    }

    public int top() {
        if (isEmpty()) {
            System.out.println("Stack is empty");
            return Integer.MIN_VALUE;
        }
        return data[nextIndex - 1];
    }

    public boolean isEmpty() {
        return nextIndex == 0;
    }

    public int size() {
        return nextIndex;
    }
}
```

---

### 4. **Linked List-Based Stack Implementation**

Stacks can also be implemented using **linked lists**, which allow dynamic resizing and avoid the issue of fixed array size.

```java
class Node {
    int data;
    Node next;
    Node(int data) {
        this.data = data;
        this.next = null;
    }
}

class StackUsingLinkedList {
    Node top;
    
    public StackUsingLinkedList() {
        this.top = null;
    }

    public void push(int data) {
        Node newNode = new Node(data);
        newNode.next = top;
        top = newNode;
    }

    public int pop() {
        if (top == null) {
            System.out.println("Stack Underflow");
            return Integer.MIN_VALUE;
        }
        int value = top.data;
        top = top.next;
        return value;
    }

    public int peek() {
        if (top == null) {
            System.out.println("Stack is empty");
            return Integer.MIN_VALUE;
        }
        return top.data;
    }

    public boolean isEmpty() {
        return top == null;
    }
}
```

---

### 5. **Inbuilt Stack in Java**

Java provides an inbuilt `Stack` class in the `java.util` package, which offers common stack operations like `push()`, `pop()`, `peek()`, `isEmpty()`, and `size()`.

```java
import java.util.Stack;

Stack<Integer> stack = new Stack<>();
stack.push(10);
stack.push(20);
System.out.println(stack.pop());  // Output: 20
System.out.println(stack.peek()); // Output: 10
System.out.println(stack.isEmpty()); // Output: false
```

---

### 6. **Performance Analysis**

#### **Time Complexity**:
All core stack operations (`push()`, `pop()`, `peek()`, `isEmpty()`) have a **time complexity of O(1)** because they involve a single element and do not depend on the size of the stack.

#### **Space Complexity**:
- **Array-based Stack**: O(n), where `n` is the number of elements. It can be inefficient if over-allocated, leading to space wastage.
- **Linked List-based Stack**: O(n), but each node uses extra space for pointers, making it less space-efficient than an array.

---

### 7. **Common Applications of Stacks**

- **Function Call Stack**: Used by programming languages to track function calls. Each call is pushed onto the stack, and once the function completes, it is popped.
- **Expression Evaluation**: Used in postfix/prefix expression evaluation and conversion from infix notation.
- **Backtracking Algorithms**: Depth-first search (DFS), solving mazes, undo/redo operations.
- **Balanced Parentheses Problem**: Checking if a string of parentheses is properly balanced using a stack.
  
#### **Balanced Parentheses Example**:
```java
public boolean isBalanced(String expr) {
    Stack<Character> stack = new Stack<>();
    for (char ch : expr.toCharArray()) {
        if (ch == '(' || ch == '{' || ch == '[') {
            stack.push(ch);
        } else {
            if (stack.isEmpty()) return false;
            char open = stack.pop();
            if (!isMatchingPair(open, ch)) return false;
        }
    }
    return stack.isEmpty();
}

private boolean isMatchingPair(char open, char close) {
    return (open == '(' && close == ')') ||
           (open == '{' && close == '}') ||
           (open == '[' && close == ']');
}
```

---

### 8. **Limitations and Overflow**
- **Stack Overflow** occurs when trying to add an element to a full stack (in array-based implementations).
- **Stack Underflow** occurs when trying to pop from an empty stack.

---

### 9. **Stack and Recursion**
- Each recursive call adds a new frame to the call stack, and these frames are popped as the recursion unwinds.
- **Recursive Depth**: Excessive recursion can cause a **stack overflow** if the function call stack exceeds its limit.

---

### 10. **Real-World Applications**
- **Browser Back Button**: Browsers use stacks to allow users to go back to previous pages.
- **Text Editor Undo**: Undo mechanisms rely on stacks to store previous states.

---

### 11. **Advanced Stack Topics**

- **Dynamic Stack**: Implemented using dynamic arrays, which resize themselves when the stack exceeds its current capacity. This allows for **amortized O(1)** time complexity for `push` operations.
- **Postfix Expression Evaluation**: Stacks are used to evaluate expressions in postfix notation. Each operand is pushed onto the stack, and operators pop operands, evaluate, and push the result back.

---

### 12. **Stack vs. Queue**
- **Stack**: Follows **LIFO** (Last In, First Out).
- **Queue**: Follows **FIFO** (First In, First Out).

| Feature         | Stack (LIFO)           | Queue (FIFO)           |
|-----------------|------------------------|------------------------|
| **Insertion/Removal** | Last element inserted is the first to be removed. | First element inserted is the first to be removed. |
| **Use Case**     | Function call stacks, backtracking algorithms, undo mechanisms. | Task scheduling, breadth-first search, buffering. |

---

### Summary of Key Points:
- **Efficient Operations**: Push, pop, and peek are O(1) operations.
- **Different Implementations**: Can be implemented using arrays or linked lists.
- **Applications**: Used in function call management, expression evaluation, balanced parentheses checking, and more.
- **Limitations**: Stack overflow and underflow can occur in certain implementations.

---

These notes now cover **all essential concepts** related to the **stack data structure**, including implementations, applications, performance analysis, and limitations. Let me know if you'd like further clarifications or deeper insights on any topic!