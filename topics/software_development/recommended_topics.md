# Recommended topics


## Table of contents

+ [Topics](#topics)
+ [Sources](#sources)
+ [Data structures and Algorithms](#data-structures-and-algorithms)


## Topics

- Data structures and Algorithms
- Design patterns
- Leetcode
- Video Polygonum > email > youtube
- STAR method
- C++ built-in DSs
- OOP definitions


## Sources

- Clifford A. Shaffer (2013) _**Data structures & Algorithm analysis**_. Department of Computer Science, Virginia Tech University. Retrieved from [here](https://people.cs.vt.edu/shaffer/Book/).
- Granville Barnett, Luca Del Tongo (2008) _**Data Structures and Algorithms: Annotated Reference with Examples**_ Dot.NetSlackers. Retrieved from [here](https://archive.org/details/pdfy-A-5D_dQU-sNJJHOB).
- [How to do problems](https://www.quora.com/When-should-I-start-doing-LeetCode-problems-I-haven-t-learned-data-structures-and-algorithms)
- [LeetCode](https://leetcode.com/)
- Gayle Laakmann McDowell (2015) _**Cracking the coding interview**_, 6th ed. CareerCup.
- Adnan Aziz, Tsung-Hsien Lee, Amit Prakash (2012) _**Elements of programming interviews C++**_. 2nd ed. CreateSpace Independent Publishing Platform.
- Adnan Aziz, Tsung-Hsien Lee, Amit Prakash (2016) _**Elements of programming interviews Python**_. CreateSpace Independent Publishing Platform.
- [Grokking the system design interview](https://www.designgurus.io/course/grokking-the-system-design-interview?aff=84Y9hP)
- [Grokking the modern system design interview](https://www.educative.io/courses/grokking-the-system-design-interview)
- Erich Gamma, Richard Helm, Ralph Johnson, John Vlissides (1994) _**Design patterns. Elements of object-oriented software**_. Addison-Wesley.
- STAR method: Check [this](https://capd.mit.edu/resources/the-star-method-for-behavioral-interviews/) and [this](https://www.vawizard.org/wiz-pdf/STAR_Method_Interviews.pdf).


## Data structures and Algorithms

For a C++ software engineering interview, you should have a strong grasp of **data structures** and **algorithms**, as these are commonly tested topics. Here’s a breakdown of what to focus on:

### Data Structures

You should be comfortable with the following data structures, their implementations, and use cases:

- **Arrays & Strings**  
  - Fixed-size vs. dynamic arrays (e.g., `std::vector`)
  - String manipulation and `std::string` operations

- **Linked Lists**  
  - Singly and doubly linked lists
  - Operations: insertion, deletion, reversing, detecting cycles (Floyd’s cycle detection)

- **Stacks & Queues**  
  - Implementing using arrays or linked lists
  - Applications: expression evaluation (postfix, prefix), undo/redo, BFS  
  - Special cases: **Deque (double-ended queue)**, **Priority Queue** (using `std::priority_queue`)

- **Hash Tables (Hash Maps & Sets)**  
  - Implementing using arrays + linked lists (chaining) or probing (open addressing)  
  - `std::unordered_map`, `std::unordered_set`  
  - Collision handling techniques

- **Trees**  
  - Binary Trees, Binary Search Trees (BST), Balanced Trees (AVL, Red-Black)  
  - Traversals: Inorder, Preorder, Postorder, BFS (level-order)  
  - Common problems: Lowest Common Ancestor (LCA), Tree Diameter, Depth calculation

- **Heaps**  
  - Min-Heap / Max-Heap implementation using a binary heap (array representation)  
  - `std::priority_queue` for efficient priority queue operations

- **Graphs**  
  - Representations: Adjacency matrix vs. adjacency list  
  - Traversal: BFS, DFS  
  - Cycle detection, Topological sorting (Kahn’s algorithm, DFS)  
  - Shortest paths (Dijkstra, Bellman-Ford, Floyd-Warshall)  
  - Minimum Spanning Trees (Kruskal, Prim)

- **Tries (Prefix Trees)**  
  - Applications: Autocomplete, Dictionary search  
  - Implementing insert, search, and delete

- **Segment Trees & Fenwick Trees (Binary Indexed Tree, BIT)**  
  - Range queries (sum, min, max)  
  - Lazy propagation (for range updates)

### Algorithms

Mastering key algorithmic techniques is crucial:

- **Sorting Algorithms**  
  - QuickSort, MergeSort, HeapSort, Counting Sort, Radix Sort  
  - `std::sort()` (IntroSort: Hybrid of QuickSort, HeapSort, and InsertionSort)

- **Searching Algorithms**  
  - Binary Search (and variations like lower bound, upper bound)  
  - Ternary Search (for unimodal functions)

- **Recursion & Backtracking**  
  - Generating permutations/combinations (N-Queens, Sudoku Solver)  
  - Subset Sum Problem, Knapsack Problem  
  - Word Search (DFS + backtracking)

- **Dynamic Programming (DP)**  
  - Bottom-up vs. Top-down (memoization)  
  - Classical problems: Fibonacci, Coin Change, Longest Common Subsequence (LCS), Knapsack  
  - DP on Trees, DP with Bitmasking

- **Greedy Algorithms**  
  - Huffman Encoding, Activity Selection  
  - Kruskal’s and Prim’s algorithm (Minimum Spanning Tree)

- **Graph Algorithms**  
  - BFS, DFS  
  - Dijkstra’s Algorithm (Shortest Path)  
  - Bellman-Ford Algorithm (Negative weights)  
  - Floyd-Warshall Algorithm (All-pairs shortest path)  
  - Union-Find (Disjoint Set) with Path Compression  
  - Topological Sorting (Kahn’s algorithm, DFS)

- **Bit Manipulation**  
  - XOR tricks (finding unique numbers)  
  - Bit masking (used in DP)  
  - Checking if a number is a power of 2

- **Mathematical Algorithms**  
  - Greatest Common Divisor (GCD) using Euclidean algorithm  
  - Modular arithmetic, Fast Exponentiation  
  - Sieve of Eratosthenes (Prime numbers)  

### C++ Standard Library (STL)

Many problems can be solved efficiently using STL:
- `std::vector`, `std::array`
- `std::deque`, `std::stack`, `std::queue`, `std::priority_queue`
- `std::set`, `std::unordered_set`
- `std::map`, `std::unordered_map`
- `std::algorithm` (sorting, searching, min/max, etc.)
- `std::bitset` (for efficient bit manipulation)

### System Design and Advanced Topics (if relevant)

For senior positions:
- Scalability of data structures and algorithms
- Memory and performance optimization
- Multi-threading concepts in C++ (Mutex, Condition Variables, Atomic operations)
- Design patterns (Singleton, Factory, Observer)
- Caching techniques (LRU Cache)

### Coding Practice

Practice coding problems on:
- **LeetCode** (Top 100 interview questions, Hard problems)
- **HackerRank** (C++ challenges, STL)
- **Codeforces** (Competitive programming)
- **GeeksforGeeks** (Theory + practice)

