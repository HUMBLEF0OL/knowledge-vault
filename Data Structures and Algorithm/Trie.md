---
tags:
  - Data-Structure
  - Tree
Date: 2024-10-14
Title: Trie
References:
---
### Trie (Prefix Tree)

---

#### 1. **Introduction to Trie**

A **Trie** (pronounced "try") is a type of **tree data structure** that is used to store a dynamic set of strings, where the keys are usually strings. It is particularly well-suited for applications that involve **prefix matching**, such as autocomplete systems or spell checkers.

- **Trie** is also known as a **Prefix Tree** because it efficiently stores prefixes of strings and enables quick searches based on those prefixes.
- Each node in a Trie represents a single character of the string.

---

#### 2. **Characteristics of a Trie**

1. **Each node represents a character**:
   - A node in the Trie corresponds to a character in a word. Each path from the root node to a leaf node corresponds to a string or part of a string.
   
2. **Root node**:
   - The Trie has a single root node that doesn't store any character, and it serves as the starting point for all words.
   
3. **Child nodes**:
   - Each node has up to 26 child nodes (for lowercase English letters) or more depending on the character set (e.g., case-sensitive or Unicode characters).
   
4. **End marker**:
   - A boolean flag (`isEndOfWord`) is typically used to denote whether a node corresponds to the end of a valid word.

---

#### 3. **Operations in a Trie**

##### 3.1 **Insertion**

- **Objective**: Insert a word into the Trie.
- **Time Complexity**: O(m), where **m** is the length of the word being inserted.
- **Approach**:
  - Start at the root node and move down the Trie based on the characters in the word.
  - If a character node does not exist, create a new node.
  - Once all characters are inserted, mark the last node as the end of a word.

##### Example:
```java
class TrieNode {
    TrieNode[] children = new TrieNode[26];  // For lowercase English letters
    boolean isEndOfWord = false;
}

class Trie {
    TrieNode root = new TrieNode();
    
    // Insertion
    public void insert(String word) {
        TrieNode node = root;
        for (char ch : word.toCharArray()) {
            int index = ch - 'a';  // Calculate index (0 to 25 for 'a' to 'z')
            if (node.children[index] == null) {
                node.children[index] = new TrieNode();
            }
            node = node.children[index];
        }
        node.isEndOfWord = true;  // Mark the end of the word
    }
}
```

---

##### 3.2 **Search**

- **Objective**: Search for a word in the Trie.
- **Time Complexity**: O(m), where **m** is the length of the word being searched.
- **Approach**:
  - Start at the root and follow the character path in the Trie.
  - If any character in the word doesn't have a corresponding node, the word does not exist.
  - At the end of the word, check if the `isEndOfWord` flag is set to confirm the existence of the complete word.

##### Example:
```java
public boolean search(String word) {
    TrieNode node = root;
    for (char ch : word.toCharArray()) {
        int index = ch - 'a';
        if (node.children[index] == null) {
            return false;  // Word does not exist
        }
        node = node.children[index];
    }
    return node.isEndOfWord;  // Return true if it's a valid word
}
```

---

##### 3.3 **Starts With (Prefix Search)**

- **Objective**: Check if there is any word in the Trie that starts with a given prefix.
- **Time Complexity**: O(m), where **m** is the length of the prefix.
- **Approach**:
  - Similar to the search operation, except we don’t need to check the `isEndOfWord` flag.

##### Example:
```java
public boolean startsWith(String prefix) {
    TrieNode node = root;
    for (char ch : prefix.toCharArray()) {
        int index = ch - 'a';
        if (node.children[index] == null) {
            return false;  // No word starts with the prefix
        }
        node = node.children[index];
    }
    return true;  // Prefix exists in the Trie
}
```

---

##### 3.4 **Deletion**

- **Objective**: Remove a word from the Trie, ensuring that no invalid nodes are left after deletion.
- **Time Complexity**: O(m), where **m** is the length of the word.
- **Approach**:
  - Traverse the Trie and unmark the `isEndOfWord` flag. If the node becomes useless (i.e., no other words depend on it), remove it.

##### Example:
```java
public boolean delete(TrieNode node, String word, int depth) {
    if (node == null) return false;

    // Base case: we've reached the end of the word
    if (depth == word.length()) {
        if (!node.isEndOfWord) return false;
        node.isEndOfWord = false;
        return node.children.length == 0;  // Return true if node has no children
    }

    int index = word.charAt(depth) - 'a';
    if (delete(node.children[index], word, depth + 1)) {
        node.children[index] = null;  // Remove the child node
        return !node.isEndOfWord && node.children.length == 0;  // Remove the current node if it has no children
    }
    return false;
}
```

---

#### 4. **Advantages of a Trie**

1. **Efficient Prefix Searches**:
   - Tries are optimal for searching prefixes in O(m) time, making them well-suited for applications like autocomplete and dictionary lookups.

2. **Space Optimization**:
   - By sharing common prefixes, tries save space compared to storing each word individually.

3. **Time Complexity**:
   - Searching, insertion, and deletion all have **O(m)** time complexity, where **m** is the length of the word or prefix. This is efficient compared to hash-based structures like HashMaps or HashSets that may degrade in performance with longer words or collisions.

---

#### 5. **Disadvantages of a Trie**

1. **Space Consumption**:
   - Tries can consume more memory than other data structures like HashMaps, especially if the character set is large (for example, using Unicode characters).

2. **Overhead for Sparse Data**:
   - If the Trie stores many short or sparse words, there can be wasted space for nodes that are not used.

---

#### 6. **Applications of Tries**

1. **Autocomplete Systems**:
   - Tries are used to implement **autocomplete** features, where users are shown possible word completions based on their input prefix.
   
2. **Spell Checkers**:
   - Tries can be used to implement **spell checkers**, allowing fast lookups of valid words based on prefix or approximate matches.
   
3. **IP Routing**:
   - Tries are used in **longest prefix matching** algorithms for **IP routing**, where routers need to find the longest matching prefix for a destination IP address.
   
4. **Dictionary Implementation**:
   - Tries are commonly used to implement **dynamic dictionaries**, where words can be added, deleted, and searched quickly.

5. **Search Engines**:
   - Tries are used in search engines to efficiently index and search text data based on prefixes.

---

#### 7. **Variants of Trie**

1. **Compressed Trie (Radix Tree)**:
   - A compressed version of a Trie where long chains of single-child nodes are merged into a single node to reduce space.
   
2. **Suffix Trie**:
   - A Trie built for all **suffixes** of a string. It is used in substring searches, DNA sequencing, and text compression.
   
3. **Ternary Search Trie**:
   - Similar to a Trie but each node has three children: left, middle, and right. It combines the efficiency of binary search trees with the space-saving of Tries.

---

#### 8. **Complexity Analysis**

| Operation      | Time Complexity    | Space Complexity   |
|----------------|--------------------|--------------------|
| **Insertion**  | O(m)               | O(m * n)           |
| **Search**     | O(m)               | O(m * n)           |
| **Deletion**   | O(m)               | O(m * n)           |
| **Prefix Search** | O(m)            | O(m * n)           |

- **m**: Length of the word/prefix.
- **n**: Number of words stored in the Trie.

---

### Summary of Trie:

- **Trie (Prefix Tree)**: A specialized tree data structure that stores strings, where each node represents a single character.
- **Operations**: Insertion, Search, Deletion, and Prefix Search, all with time complexity of O(m), where **m** is the length of the word.
- **Applications**: Autocomplete, spell check, IP routing, dictionary implementation, and search engines.
- **Variants**: Compressed Trie, Suffix Trie, and Ternary Search Trie.
- **Advantages**: Efficient prefix matching and fast lookups for large sets of strings.
- **Disadvantages**: High space consumption due to large character sets.

---

This concludes the comprehensive notes on the **Trie (Prefix Tree)** data structure. Let me know if you need further