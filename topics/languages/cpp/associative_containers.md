# Associative containers

## Table of Contents
+ [Keywords](#keywords)
+ [Identifiers](#identifiers)
+ [Preprocessor directives](#preprocessor-directives)
+ [References](#references)


Associative containers hold elements whose positions depend on a key associated with each element.


**Associative containers**:

- **Ordered**: Elements sorted based on a key. Lookup, insert, and delete operations take O(log n). The internal structure is a self-balancing binary search tree (usually a red-black tree), with nodes stored in sorted order based on keys.

  - `std::set`: Stores unique elements in sorted order.
  - `std::multiset`: Similar to `std::set`, but allows duplicate elements.
  - `std::map`: Stores key-value pairs, where keys are unique and sorted.
  - `std::multimap`: Similar to `std::map`, but allows multiple values for the same key.

- **Unordered**: Elements stored in arbitrary order using hash tables for faster lookups. Lookup, insert, and delete operations take O(1) on average and O(n) on worst case (if many elements collide). The internal structure is a hash table with buckets + linked lists. A hash function converts the key into an index/bucket. Elements are stored in buckets. If 2 keys have same hash (collision), they are stored in a linked list (chaining) in the same bucket. Rehashing (doubling the number of buckets) prevents performance drops.

  - `std::unordered_set`: Similar to `std::set`, but unordered and uses hashing.
  - `std::unordered_multiset`: Similar to `std::multiset`, but unordered.
  - `std::unordered_map`: Similar to `std::map`, but unordered and uses hashing.
  - `std::unordered_multimap`: Similar to `std::multimap`, but unordered.




