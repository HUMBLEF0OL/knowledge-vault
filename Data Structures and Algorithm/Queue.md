---
tags:
  - Data-Structure
Date: 2024-10-14
Title: Queue
References:
---
### Comprehensive Notes on Queue Data Structure

---

### 1. **Introduction to Queues**

A **queue** is a linear data structure that operates on the **FIFO** (First In, First Out) principle. This means that the first element added to the queue will be the first one to be removed. It’s like a line of people waiting to be served: the first person in line is the first person to be served.

- **FIFO**: First In, First Out.
- **Abstract Data Type (ADT)**: Defines the operations, but not the implementation.

---

### 2. **Key Operations**

| Operation    | Description                                  | Time Complexity |
|--------------|----------------------------------------------|-----------------|
| **Enqueue**  | Adds an element to the end (rear) of the queue. | **O(1)**        |
| **Dequeue**  | Removes and returns the element from the front of the queue. | **O(1)**        |
| **Front/Peek** | Returns the element at the front without removing it. | **O(1)**        |
| **Size**     | Returns the number of elements in the queue.  | **O(1)**        |
| **isEmpty**  | Checks if the queue is empty.                | **O(1)**        |

- All operations run in **O(1)** time complexity, making the queue a very efficient structure for sequential access.

---

### 3. **Array-Based Queue Implementation**

In an array-based queue, elements are added at the rear and removed from the front. However, after multiple `dequeue` operations, the front of the queue may shift, causing inefficiency if the entire array is shifted every time.

#### Circular Queue:
To avoid shifting, a **circular queue** is used where the rear wraps around to the front if there is space.

```java
class QueueUsingArray {
    int[] data;
    int front;
    int rear;
    int size;
    int capacity;

    public QueueUsingArray(int capacity) {
        this.capacity = capacity;
        data = new int[capacity];
        front = 0;
        rear = -1;
        size = 0;
    }

    public void enqueue(int element) {
        if (size == capacity) {
            System.out.println("Queue Overflow");
            return;
        }
        rear = (rear + 1) % capacity;
        data[rear] = element;
        size++;
    }

    public int dequeue() {
        if (isEmpty()) {
            System.out.println("Queue Underflow");
            return Integer.MIN_VALUE;
        }
        int result = data[front];
        front = (front + 1) % capacity;
        size--;
        return result;
    }

    public int peek() {
        if (isEmpty()) {
            System.out.println("Queue is empty");
            return Integer.MIN_VALUE;
        }
        return data[front];
    }

    public boolean isEmpty() {
        return size == 0;
    }

    public int size() {
        return size;
    }
}
```

---

### 4. **Linked List-Based Queue Implementation**

A queue can also be implemented using a **linked list**, where the `rear` points to the last node and the `front` points to the first node.

```java
class Node {
    int data;
    Node next;

    public Node(int data) {
        this.data = data;
        this.next = null;
    }
}

class QueueUsingLinkedList {
    Node front, rear;

    public QueueUsingLinkedList() {
        this.front = this.rear = null;
    }

    public void enqueue(int element) {
        Node newNode = new Node(element);
        if (rear == null) {
            front = rear = newNode;
            return;
        }
        rear.next = newNode;
        rear = newNode;
    }

    public int dequeue() {
        if (front == null) {
            System.out.println("Queue Underflow");
            return Integer.MIN_VALUE;
        }
        int result = front.data;
        front = front.next;
        if (front == null) {
            rear = null;
        }
        return result;
    }

    public int peek() {
        if (front == null) {
            System.out.println("Queue is empty");
            return Integer.MIN_VALUE;
        }
        return front.data;
    }

    public boolean isEmpty() {
        return front == null;
    }
}
```

---

### 5. **Types of Queues**

1. **Simple Queue (FIFO)**: 
   - The basic queue where elements are inserted at the rear and removed from the front.

2. **Circular Queue**: 
   - In a circular queue, the last position is connected back to the first position to make a circle. This avoids memory wastage when the queue is implemented using arrays.

3. **Double-ended Queue (Deque)**: 
   - In a deque, elements can be added or removed from both ends (front and rear).
   
4. **Priority Queue**:
   - A priority queue is a special type of queue where each element has a priority. Elements with higher priority are dequeued before elements with lower priority, regardless of their insertion order.

---

### 6. **Applications of Queues**

- **Task Scheduling**: Queues are used in scheduling tasks in operating systems (like CPU scheduling, disk scheduling).
- **Breadth-First Search (BFS)**: In graph traversal algorithms, queues are used to explore nodes layer by layer.
- **Asynchronous Data Transfer**: In IO buffers, queues manage data being transferred asynchronously.
- **Print Queue**: Printing jobs are stored in a queue before being sent to the printer.
- **Call Center Systems**: Calls are placed in a queue and handled on a first-come, first-served basis.
- **Round Robin Scheduling**: Time-sharing systems use queues to schedule tasks in a round-robin manner.

---

### 7. **Performance Analysis**

#### **Time Complexity**:
All queue operations (`enqueue()`, `dequeue()`, `peek()`, `isEmpty()`) have a **time complexity of O(1)** as they only involve modifying the head or tail of the queue.

#### **Space Complexity**:
- **Array-based Queue**: O(n), where `n` is the capacity of the queue.
- **Linked List-based Queue**: O(n), where `n` is the number of elements. Each element has a small additional memory overhead for storing the pointer to the next node.

---

### 8. **Queue vs. Stack**

| Feature         | Queue (FIFO)                        | Stack (LIFO)                       |
|-----------------|-------------------------------------|------------------------------------|
| **Insertion/Removal** | Elements are inserted at the rear and removed from the front (FIFO). | Elements are inserted and removed from the top (LIFO). |
| **Use Case**     | Task scheduling, breadth-first search, print queues. | Function call stacks, undo operations. |
| **Typical Operations** | `enqueue()`, `dequeue()`      | `push()`, `pop()`                  |

---

### 9. **Real-World Applications of Queue**

- **Printer Spooling**: Print jobs are added to a queue and processed in order.
- **CPU Scheduling**: Processes waiting for CPU time are managed in a queue.
- **Customer Support Lines**: Calls or requests are queued and handled on a first-come, first-served basis.
- **Network Packet Buffering**: Data packets in networking are buffered in queues before processing.
- **Messaging Services**: Messages in systems like Kafka or RabbitMQ are queued for delivery.

---

### 10. **Circular Queue**

A **circular queue** is a more efficient version of a regular queue where the last position connects back to the first position, allowing for more efficient use of space in an array implementation. This prevents unused space after multiple `dequeue` operations.

#### Example of Circular Queue:
```java
rear = (rear + 1) % capacity;
front = (front + 1) % capacity;
```

In this way, the queue's rear wraps around to the front when it reaches the end of the array, allowing for continuous use of the available space.

---

### 11. **Double-ended Queue (Deque)**

A **deque** (Double-ended Queue) allows insertion and removal of elements from both the front and rear. This structure is more flexible than a simple queue or stack.

```java
Deque<Integer> deque = new LinkedList<>();
deque.addFirst(1);  // Adds 1 to the front
deque.addLast(2);   // Adds 2 to the rear
deque.removeFirst();  // Removes from the front
deque.removeLast();   // Removes from the rear
```

---

### Summary of Key Points:
- **Efficient Operations**: Queue operations like `enqueue` and `dequeue` are performed in O(1) time.
- **Multiple Implementations**: Can be implemented using arrays (with circular logic) or linked lists.
- **Variants**: Includes circular queue, double-ended queue (deque), and priority queue.
- **Applications**: Queues are widely used in scheduling systems, task management, BFS algorithms, and real-time processing.

---

These notes now cover all essential concepts related to the **queue data structure**, including its operations, types, implementations, performance analysis, and applications. Let me know if you'd like further clarifications or deeper insights on any topic!