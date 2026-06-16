# Game systems

<br>![computer graphics image](https://raw.githubusercontent.com/AnselmoGPP/know_base/master/resources/computer_graphics.jpg)

## Table of Contents

+ [Bounding boxes](#bounding-boxes)

## Bounding boxes

To allow objects to collide between each other, each object has one or more **bounding boxes** (BBs) assigned, and we evaluate the collision between boxes of different objects. For efficiency, we need to implement **spacial partitioning** (SP), which avoids checking every object against every other object (an O(N<sup>2</sup>) disaster). SP is also useful for frustum culling.

### Box representation:

- **AABB** (Axis-Aligned Bounding Box): Box faces are aligned with world axes.
  - Storage: Two vectors (bottom-left-front and top-right-back).
  - Pros: Intersection tests are very fast.
  - Cons: If the object rotates, the AABB must be recalculated and expanded.
- **OOB** (Oriented Bounding Box): Box rotates with the object.
  - Storage: Center point + extents (half-widths) + 3x3 rotation matrix
  - Pros: Tight fit around rotating objects.
  - Cons: More expensive intersection math (Separating Axis theorem).

**Standard:** Use AABBs for broad-phase spacial queries and world partitioning. Use OBBs or raw mesh triangles only for narrow-phase, precise collision detection.

### Structural pipeline

- **Local space**: When you import a 3D model, automatically compute the local-space AABB (`localAABB`) by scanning all vertices once to find the minimum and maximum coordinates.

- **World space**: When the entity moves/scales/rotates, transform its `localAABB` into `worldAABB`. For efficiency, don't transform all 8 corners with the transformation matrix, just compute the new AABB directly using the old AABB and the absolute values of the rotation matrix (Jim Arvo's method).

### Spatial partitioning (SP)

Checking all objects in a scene against each other takes O(N<sup>2</sup>). SP reduces this to O(N log N) or O(N). There are different possible data structures, depending on your style: BVH, Octree/Quadtree, and Spatial hashing.

**Octree** (3D) or **Quadtree** (2D): It partitions space. Recursively divides 3D space into 8 equal cubes (or 2D space into 4 squares). The boxes never overlap. If a large object crosses the boundaries of multiple cubes, the octree must either store a reference to it in all those cubes, or push the dragon up to a giant parent node.
- Objects are assigned to the specific nodes they physically occupy.
- Moving objects is more painful than BVH. That requires deleting an object from one square and figure it out which new squares it now touches.
- Best for static environments (terrain, static buildings, sparse worlds, voxels, frustum culling…).

**BVH** (Bounding Volume Hierarchy): It partitions geometry. Tree structure where smaller BBs are wrapped inside larger BBs. The root box wraps the entire world. It groups a cluster of nearby objects together and draws a tight bounding box around around just them. Then it groups those boxes into bigger boxes. These boxes change shape based o where objects go. Two parent boxes can overlap in world space. An object belongs to exactly one leaf node in the tree, no matter how big it is or where it crosses lines.
- If a camera frustum or a raycast misses a parent box, you discard all children inside.
- Requires dynamically updating or re-fitting the tree when objects move.
- Moving objects is easier to implement and maintain than in octree/quadtree. You just adjust the dimensions of its parent boxes (refitting).
- Best for general 3D engines, dynamic characters, ray-tracing, dense meshes, etc.

**Spatial hashing**: Space is divided into a regular mathematical grid. A hash function maps an object's position to a grid cell ID. Best for dynamic, uniform objects.
- Very fast insertion and lookups (O(1)). No trees to balance.
- Performance degrades if object sizes vary wildly.

### Implementation

- AABB math: `AABB`, `test_intersection(AABB a, AABB b)`, `get_world_aabb(LocalAABB, Transform)`.
- Frustum culling: Use your AABBs to optimize rendering. Don't render the `WorldAABB`s that are not inside the camera view frustum.
- Static objects: Build a static tree (BVH or Octree) for static objects only. Group your environment meshes into an Octree or a BVHon scene load.
- Dynamic objects: Add moving entities into the spacial structure. For BVH, implement box "refitting". For octrees/grids, remove and re-insert entities into their new cells whenever their positions change significantly.

### BVH

It starts creating a single massive box containing all your entities. It then chooses a cutting plane, splits the objects into two groups (left and right), and wraps a smaller box around each group. This process repeats recursively until each group contains only one object (a leaf node).

**SAH** (Surface Area Heuristic): Mathematical formula that predicts the computational "cost" of a split. It assumes that the probability of a ray or camera frustum hitting a bounding box is proportional to its surface area. When dividing a node, we test a few hypothetical split planes along X, Y, and Z axes and choose the split with the lowest cost (smallest surface areas with the cleanest separation of objects).

- Cost = C<sub>traverse</sub> + (Area(Left) / Area(Parent)) · N<sub>Left</sub> · C<sub>isect</sub> + (Area(Right) / Area(Parent)) · N<sub>Right</sub> · C<sub>isect</sub>

  - C<sub>traverse</sub>: Fixed cost of checking a box
  - C<sub>isect</sub>: Cost of checking a single object
  - N: Number of objects in that sub-group

**Pipeline:**

- Initialize root: Calculate world-space AABB for every single object. Create a root BVHNode that encloses all of them. Put all objects into a master list assigned to this root.
- Pick best axis: Find the longest axis of the parent box. Sort the object list along that axis based on their center points (centroids).
- Apply split: Use SAH algorithm to find the optimal index in your sorted list to split the objects into two groups.
- Recursion: Create two child nodes and allocate the two groups. Re-calculate tight bounding boxes for both children. Repeat steps 2 and 3 for each child until a node contains only 1 object (leaf).

**Node:** It should be as small as possible. A common optimization is using an anonymous union so a node is either an internal branch (pointing to two children) or a leaf (pointing to a 3D data), but never both.

```
struct BVHNode
{
  AABB bounds;
  bool isLeaf;
  
  union
  {
    struct  // internal node data
	{
	  BVHNode* leftChild;
	  BVHNode* rightChild;
	};
	
	struct   // leaf node data
	{
	  unsigned int firstEntityIndex;
	  unsigned int entityCount;
	};
  };
};
```

**Traversal:** When checking a raycast, bullet, or camera frustum against the BVH, we use a stack-based traversal instead of a standard function recursion to save memory and performance.

```
void intersectBVH(BVHNode* root, Ray ray)
{
  BVHNode* stack[64];
  int stackPtr = 0;
  stack[stackPtr++] = root;
  
  while (stackPtr > 0)
  {
    BVHNode* node = stack[--stackPtr];
	if (!rayIntersectsAABB(ray, node->bound)) continue;
	if (node->isLeaf)
	  checkObjectCollision(node->firstEntityIndex, node->entityCount);
	else
	{
	  stack[stackPtr++] = node->leftChild;
	  stack[stackPtr++] = node->rightChild;
	}
  }
}
```

Don't sort arrays raw. Sorting structures containing heavy elements can be expensive. Instead, sort an array of small pointer structures or integer indices (ObjectAttributes) containing just the object's ID, its centroid, and its bounding box.

### LBVH

SAH can be too slow for rebuilding the BVH tree rapidly at runtime for many moving objects. This requires constantly searching, sorting, and calculating areas at every single branch (O(N log N)). LBVH solves this by turning a complex 3D problem into a simple 1D sorting problem.

**LBVH** (Linear BVH): LBVH maps 3D coordinates onto a 1D line using **Morton Codes**. Once your objects have a Morton code, you can sort them using ultra-fast **Radix Sort** and generate the tree instantly.

**Morton codes** (Z-order curves): Mathematical trick that maps 3D coordinates down into a single 1D number (integer) while preserving spatial locality. Thus, if two objects are close in our 3D world, their 1D Morton codes will be very close numerically. To find the Morton code of a 3D point, take the binary representation of its X, Y, Z coordinates and interleave their bits (starting with the first bit of Z, then Y, then X). Example:

- 3D point: (X,Y,Z) = (2, 3, 1) = (010, 011, 001)
- Morton code: 000011110

**Radix sort**: Standard sorting algorithms like `std::sort` (QuickSort/IntroSort) rely on comparisons and take O(N log N) time. Radix sort is a non-comparative sorting algorithm that groups integers by their individual digits (or bits) from the least significant to the most significant.
- Time complexity = O(N). Actually, it's O(N·K), but K is the number of bits (constant).

Once you have all your objects sorted by their Morton codes in an array, this represents the leaf nodes of your BVH from left to right. Thus, you no longer have to guess where to split the objects. 






Is a box inside the frustum?
Same object in different parent AABBs?
Difference between BVH and octree.
Why spatial hashing degrades performance with varying object sizes?