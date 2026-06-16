# Technical patterns


## Table of Contents

* [References](#references)
* [Data structures and Algorithms](#data-structures-and-algorithms)
* [Basic patterns](#basic-patterns)
* [Technical patterns](#technical-patterns)

## References

- Gayle Laakmann McDowell (2015) _**Cracking the coding interview**_, 6th ed. CareerCup.


## Data structures and algorithms

Common Data Structures (DSs):

Linear DSs



- Lists:
  - Array
  - Linked list (singly, doubly)




Basic operations:

- Insert: Add element at any position.
- Delete: Delete element at any position
- Random access: Access any element.
- Lookup/Search: Look for an element.



### Array

Main operations:

- Insert: O(n) (last node is O(1))
- Delete: O(n) (last node is O(1))
- Random access: O(1)
- Search/Lookup: O(n) (if not sorted)

**Traversal**:

- **Linear** (O(n)): Go through each element one by one.
- **Binary search** (O(log n)): Requires sorted elements.

**Techniques**:

- **Two-pointers**: Traverse a DS using 2 pointers. There're different variations, depending on the directions (same, opposite) and width (fixed, variable). Use case examples:

  - Same direction, variable width: Remove duplicates from a sorted array.
  - Same direction, fixed width: 
  - Opposite direction, variable width: 
  - Opposite direction, fixed width: 

- **Circular array**: The two ends of the array are connected.

### Linked-list

**Types**:

- Singly linked list (SLL): Has link to `next` node.
- Doubly linked list (DLL): Has links to `next` and `prev` nodes.
- Multilevel SLL/DLL: Like a SLL or DLL, but its nodes have an additiona pointer (`child`) to another list.

#### SLL

**Operations**:

- Insert: O(1) (provided you have `prev`)
- Delete: O(n) (requires `prev` node) (first node is O(1))
- Random access: O(n)
- Search/Lookup: O(n)

**Techniques**:

- **Two pointers**: Same direction for SLLs. 
  - Different speed: Determine if a LL has a cycle. Determine the middle of a LL.
  - Same speed: Determine where 2 LLs intersect. Remove the nth node from the end of the LL.
  - Use both: Determine where the cycle begins.

- **Two pointers: Double fast**: A `slow` pointer goes one step at a time. A `fast` pointer goes two steps at a time. The following code moves `slow` pointer to the middle element (or one past the middle if size is odd).

```
ListNode *slow = head, *fast = head;
while (fast && fast->next)
{
  fast = fast->next->next;
  slow = slow->next;
}
```

Advices:
- Instead of copying elements to a temporal DS to process them (O(n) space), we can move the elements around and use them directly (O(1) space).
- When working with a LL, we can process it in a single LL or in different LLs.
- (SLL) In many cases, you need to track the previous node of the current node.
- Simplify computations using a sentinel node: header node (one-before-the-first node).

#### DLL

**Operations**:

- Insert: O(1) (provided you have `prev` or `next`)
- Delete: O(1) (provided you have `node` to delete)
- Random access: O(n)
- Search/Lookup: O(n)

Advices:
- Simplify computations using sentinel nodes: header node and a tailer node (one-past-the-last node).






## Basic patterns

- **In-place operations**: Operations applied on the target DS (instead of on a copy of it). They're not always possible (e.g., when we need the original array values again later). This can reduce space complexity from O(n) to O(1).

- A list of size n have indices in range [0, n-1].
- `n / 2` = Element in the middle ([0][1]**[2]**[3][4]) or right after the middle ([0][1]**[2]**[3]).
- `n - 1 - i` = Opposing index ([0]**[1]**[2]**[3]**[4]).
- Storing elements of a list in a stack gets the list reversed.
- Passing elements from one stack to another inverts the order of the elements.

- Sometimes it's easier to traverse a DSs from the end (or both sides if we use double pointer). 

Check parity of a value:

- Is odd: `val % 2`
- Is even: `!(val % 2)`


Random access
Lookup
Insert
Remove


Size of a DS:
  - Range = `[0, n-1]`, or `[0, n)`
  - `size/2`:
    - size is odd → central element
	- size is even → center right element


For-loop header (like `for(int i = 0; i < n; ++n)`) contains:
- Control variable creation and initialization
- Finish condition
- Advance action (increment, decrement…)

While-loop header (like `while(i < n)`) contains:
- Finish condition

Range-for header (like `for(auto& item : arr)` contains:
- Single element

Thus, for-loops can keep code more compact. While-loops usually require the control variable and the advance action to be elsewhere. Range-fors just provides the elements.



## Technical patterns

These patterns can handle roughly ~90% of common technical interview questions. Most questions are variations or combinations of these patterns.

- **Nested loop traversal** (O(n<sup>2</sup>)): One loop inside another loop.
  - When:
  - Sub-patterns:
  - Examples:
    - Palindromic substrings (O(n<sup>2</sup>))
	- All subarrays
	- All substrings

- **Pairwise comparison / All-pairs iteration** (O(n<sup>2</sup>)): Nested loop traversal where the outer loop iterates through each element, and the inner loop iterates over the elements after the current one. Brute-force all combinations.
  - When: Check for duplicates, find pairs with some property, compare all possible combinations.
  - Examples:
    - Closest pair of points
	- 2-sum brute force
	- Check duplicates in array
  
- **Two pointers / Runner technique**: Use two indices moving through a list to avoid nested loops.
  - When: Sorted arrays, find pairs with a sum, reverse strings in-place, remove duplicates.
  - Sub-patterns: Opposite ends, same-direction pointers, fast/slow pointers.
  - Examples:
    - Sorted array two-sum → Find if two numbers sum to a target.
	- Container with most water → Maximize area between two lines.
    - Remove duplicates from sorted array → In-place removal using read/write pointers.
	- Container with most water.
	- 3-sum problem.
	- Linked list cycle detection (Floyd's algorithm).
	
- **Sliding window**: Maintain a contiguous range (window) over data and slide it to track sums, counts, or max/min.
  - When: Substring/array problems involving a length or sum constraint.
  - Sub-patterns: Fixed-size window, dynamic-size window, string window problems.
  - Examples:
    - Longest substring without repeating characters → Variable-length window.
    - Minimum window substring → Dynamic shrinking and expanding window.
    - Longest repeating character replacement → Fixed-size window with char counts.
	- Maximum sum subarray of size k.
  
- **Fast & slow pointers** (or **Tortoise and hare**): Two pointers moving at different speeds to detect cycles or middle elements.
  - When: Linked-lists, circular arrays.
  - Sub-patterns: Cycle detection, middle finding, length of cycle.
  - Examples:
    - Linked list cycle detection → Floyd’s Tortoise and Hare.
    - Happy number → Detect loop in digit-sum transformation.
    - Find middle of linked list → Move one pointer twice as fast.
	- Reorder linked-list.
  
- **Hashing/Hash-map lookup**: Store visited elements or counts for O(1) lookups.
  - When: Detect duplicates, frequency counts, prefix sums.
  - Sub-patterns: Frequency maps, hash sets, rolling hash.
  - Examples:
    - Two sum
	- Group anagrams
	- Longest consecutive sequence
	
- **Binary search**: 
  - When:
  - Sub-patterns: Iterative, recursive, binary search on answer space.
  - Examples:
    - Search in Rotated Sorted Array
    - Find Minimum in Rotated Sorted Array
    - Median of Two Sorted Arrays  
	
- **BST (Binary Search Tree)**:
  - When:
  - Sub-patterns: In-order traversal, insertion/deletion, lowest common ancestor.
  - Examples:
    - Validate BST
    - Lowest Common Ancestor of BST
    - Convert Sorted Array to BST
  
- **Sorting + Binary search**: Sort data to apply binary search or fimplify constraints.
  - When: Search problems, interval merging, deduplication.
  
- **Graph traversal**: Explore data structures (graphs, grids, trees) systematically.
  - When: Connectivity, shortest path, tree processing.
  - Sub-patterns: BFS, DFS, Union-Find, Dijkstra's, Bellman-Ford.
  - Examples:
    - Number of connected components (islands) → Flood fill BFS/DFS.
    - Clone graph → BFS/DFS with visited map.
    - Word ladder → BFS shortest path on word graph.
	- Minimum spanning tree (Kruskal / Prim)
	
- **BFS (Breadth-First Search)**:
  - When:
  - Sub-patterns: Level-order traversal, shortest path in unweighted graphs.
  - Examples:
    - Binary tree level order traversal
	- Minimum depth of binary tree
	- Word ladder
	
- **DFS (Depth-First Search)**:
  - When:
  - Sub-patterns: Preorder/inorder/postorder, recursive vs. iterative.
  - Examples:
    - Binary tree path sum
	- Number of islands
	- Word search
  
- **Backtracking**: Try all possible choices, backtrack when a choice fails.
  - When: Combinatorics, permutations, constraint satisfaction.
  - Sub-patterns: DFS + decision-making, constraint-based recursion.
  - Examples:
    - N-Queens
	- Word search
	- Permutations/Combinations
  
- **Dynamic programming (DP)**: Break problems into overlapping subproblems and reuse results.
  - When: Optimization problems, sequences, combinatorics.
  - Sub-patterns: 1D DP (Fibonacci, Coin change), 2D DP (Knapsack, Grid paths), Interval DP (Palindromic substrings).
  - Examples:
    - Climbing stairs → Fibonacci DP.
    - Coin change → Min coins to reach amount.
    - Longest common subsequence → Classic DP table.
	- Longest common subsequence
	- House robber
	- Edit distance
  
- **Greedy algorithms**: Always take the locally optimal choice.
  - When: Interval scheduling, coin change (specific denominations), Huffman coding.
  - Sub-patterns: Interval scheduling, coin change (when greedy works), Huffma coding.
  - Examples:
    - Activity selection
	- Jump game
	- Huffman encoding
  
- **Union-Find / Disjoint set**: Keep track of connected components efficiently. Kruskal's algorithm.
  - When: Graph connectivity, Kruskal's algorithm.
  - Examples:
    - Redundant connection
	- Number of connected components
	- Accounts merge
  
- **Heap / Priority queue**: Always fetch min/max element efficiently.
  - When: Kth largest element, merging sorted lists.
  - Sub-patterns: Min-heap, max-heap, k-way merge.
  - Examples:
    - Kth largest element
	- Merge k sorted lists
	- Top K frequent elements.
  
- **Matrix traversal patterns**: Row/column scanning (row-by-row, column-by-column), spiral order, diagonal, boundary first, DFS/BFS on grids.
  - When: Board games, image processing.
  - Sub-patterns:
  - Examples:
    - Spiral matrix
	- Rotate image
	- Word search
  
- **Pairwise comparison / Nested loops**: Compare each element with the rest. Brute-force all combinations.
  - When: Closest points, brute-force matching.
  - Sub-patterns:
  - Examples:
    - Closest pair of points
	- 2-sum brute force
	- Check duplicates in array
  
- **Bit manipulation**: Use bitwise ops for compact storage or fast computation.
  - When: Flags, subsets, parity checks.
  - Sub-patterns: Masking, XOR tricks, bit DP.
  - Examples:
    - Single number → XOR to find unique element.
    - Find missing number → XOR all indices and elements.
    - Two single numbers → Partition by set bit.
	- Subsets using bitmask
	- Reverse bits
  
- **Prefix sum / Cumulative sum**: Precompute running sums to answer range queries fast.
  - When: Range sum queries, subarray sums.
  - Sub-patterns: 1D prefix sum, 2D prefix sum, difference array.
  - Example:
    - Subarray sum equals K
	- Range sum query (immutable)
	- 2D matrix sum region query
  
- **Merge intervals**: 
  - When:
  - Sub-patterns: Sorting by start time, merging, interval insertion.
  - Examples:
    - Merge intervals.
	- Insert interval.
	- Employee free time.
	
- **Cyclic sort**: 
  - When:
  - Sub-patterns: In-place index placement, missing number detection.
  - Examples:
    - Find all missing numbers.
	- First missing positive.
	- Find duplicate number.
	
- **Linked list reversal**: 
  - When:
  - Sub-patterns: Reverse entire list, reverse sublist, reverse k-group.
  - Examples:
    - Reverse linked list.
	- Reverse nodes in k-group.
	- Palindrome linked list.
	
- **Topological sort**:
  - When:
  - Sub-patterns: kahn's algorithm, DFS-based topo sort.
  - Examples:
    - Course schedule
	- Alien dictionary
	- Minimum height trees
	
- **Mathematical patterns**:
  - When:
  - Sub-patterns: GCD/LCM, modular arithmetic, combinatorics.
  - Examples:
    - Greatest common divisor
	- Modular exponentiation
	- Pascal's triangle
	
- **Recursion**:
  - When:
  - Sub-patterns:
  - Examples:
    - Divide & conquer (binary search, merge sort)
	- Tree recursion (traversing binary trees)
	- Backtracking (generating permutations, solving mazes)
	- Dynamic programming (top-down) (recursion + memoization)

The other ~10% are often:

- Math-heavy problems (number theory, probability)
- Specialized algorithms (suffix arrays, KMP)
- Domain-specific (low-level systems, graphics programming…)

I can map each pattern to 2–3 canonical problems so you’d have a training set that hits all the main scenarios. That’s how you get from “knowing patterns” to “recognizing them instantly.”

