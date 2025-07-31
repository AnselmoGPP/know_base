# Machine learning

## Table of Contents
+ [Introduction](#introduction)
+ [Applied math](#applied-math)
    + [Linear algebra](#linear-algebra)


## Introduction

Abstrac and formal problems, easily described by formal and mathematical rules, are usually difficult for human beings to solve, but straightforward for computers. However, intuitive problems, difficult to describe formally, are easy for humans to solve, but difficult for computers because it's difficult to articulate them formally. A solution to intuitive problems is to allow computers to learn from experience and understand the world in terms of a hierarchy of concepts, with each concept defined in terms of its relation to simpler concepts. This allows the computer to learn complicated concepts by building them out of simpler ones (**deep learning**). By gathering knowledge from experience, we avoid the need for human operators to formally specify all of the knowledge that the computer needs. Human's life require an immense amount of amount of knowledge about the world, which is subjective and intuitive, and therefore difficult to articulate formally. Computers need to capture this same knowledge in order to behave intelligently.

**Knowledge base approach:** Many AI projects (like Cyc) tried to hard-code knowledge about the world in formal languages, but none of them led to a major success.

**Machine learning (ML):** AI capability of acquiring its own knowledge by extracting patterns from raw data. Examples: logistic regression (for recommending cesarean delivery), Bayes (for separating spam emails). 
  - Logistic regression: Its performance depends heavily on the **representation** of data (set of chosen features extracted from data). Each piece of data included in the representation is a **feature**. It learns how each feature correlates with various outcomes. However, sometimes it's difficult to know what features to extract (e.g. how to describe how a chair looks like in pixel values?).

**Representation learning (RL):** Machine learning approach that discovers not only the mapping from representation to output, but also the representation itself (i.e. to discover a good set of features). This improves performance and allows quick adaptation to new tasks. Example: autoencoder (it converts input data into different representation [encoder] and converts it back in the original format with new properties [decoder], preserving as much information as possible). The features should separate the **factors of variation** that explain the observed data (color, position, shape...), which refer to separate sources of influence not usually combined by multiplication. Factors are often not directly observed quantities (invisible forces, abstractions that explain observed data in a simpler way, etc.). However, often, many factors influence every piece of data (the color depends on the amount of light, the shape depends on the viewing angle...), so we need to disentangle the factors and discard those that we don't care about. Sometimes it's very difficult to extract such high-level, abstract features from raw data to obtain a representation.

**Deep learning (DL) or Artificial neural networks (ANNs):** Machine learning approach that solves the problem of representation learning (of getting a disentangled representation) by introducing representations expressed in terms of other, simpler representations. It builds complex concepts (high abstractions) out of simpler concepts (lower abstractions). It studies models that involve a greater amount of composition of learned functions or learned concepts than traditional machine learning does. Examples: 
- The complex concept of a human image is represented by combining simpler concepts (corners, contours...), which are in turn defined in terms of even simpler concepts (edges...). 
- **Multilayer perceptron (MLP) (or Feedforward deep network):** Mathematical function mapping some set of input values to output values. This function is composed by many simpler functions, each one providing a new representation of the input.
Furthermore, depth allows the computer to learn a multi-step program, where one layer is executed after another. The more depth, the more sequential instructions. This helps the model organize its processing.

There are 2 main ways of measuring the depth of a model:
- Depth of the computational graph: Number of sequential instructions executed to evaluate the architecture. Length of the longest path through a flow chart describing how to compute each of the model's outputs given its inputs. It may vary between 2 equivalent programs. 
- Depth of the probabilistic modeling graph: Graph of the concepts. 
The first may be much deeper than the second because the flowchart of the computations needed to compute the representation of each concept may be much deeper (detect eye > detect face > detect second eye in the shadow) than the graph of the concepts (detect eyes > detect face). This is so because the system's understanding of the simpler concepts can be refined given information about the more complex concepts.

Sets and subsets:
AI:[ML:[RL:[DL:[...], ...], ...], ...]


## Applied math

### Linear algebra

**Scalar:** Single number. 

**Vector:** It's an array of numbers (represented as a column enclosed in brackets), each one identified with one index. We can consider it a point in space (each element is the coordinate along a different axis). It's a matrix with one column.
- **Set** of elements x<sub>1</sub>, x<sub>3</sub> and x<sub>6</sub> = S = {1,3,6} = x<sub>S</sub>. 
- **Complement** of a set. Examples: x<sub>-2</sub> = vector x without element 2.  x<sub>-S</sub> = vector x without set S.
- **Dot product** (xy) = x<sup>T</sup> * y

**Matrix: ** It's a 2D array of numbers, each one identified 2 indices (height/row m, width/column n)
- A<sub>i,j</sub> = element at position (i,j) | A<sub>m,n</sub> = bottom right entry
- A<sub>i,:</sub> = all numbers with vertical coordinate i (use : to refer to all elements in that line)
- A<sup>T</sup> = Transpose of A = Mirror image of A across the **main diagonal** (from upper left corner to lower right).
  - (A<sup>T</sup>)<sub>i,j</sub> = A<sub>j,i</sub>
  - Transpose of a vector = matrix with one row
  - Transpose of a scalar = that same scalar
- A + B = C (A<sub>i,j</sub> + B<sub>i,j</sub> = C<sub>i,j</sub>) (A and B must have same shape)
- A * a (multiply/add scalar a to each element in the matrix)
- **Broadcasting:** Implicit copy of a vector to many locations. A + v = C (add vector v to each row) (A<sub>i,j</sub> + v<sub>j</sub> = C<sub>i,j</sub>)
- Product of 2 matrices: A<sub>mxn</sub> * B<sub>nxp</sub> = C<sub>mxp</sub> (AB = C) (C<sub>mxp</sub> = &sum;<sub>k</sub>(A<sub>i,k</sub> * B<sub>k,j</sub>))
- Element-wise (or Hadamard) product of 2 matrices: A · B = matrix containing the product of the individual elements)
**Dot product** (A, B) = compute C<sub>i,j</sub> as the dot product between row i of A and column j of B

**Tensor:** Array with more than 2 axes (A<sub>i,j,k</sub> = element at position (i,j,k)).

Matrix product operations properties:
- Distributive: A(B + C) = AB + AC
- Associative: A(BC) = (AB)C
- Not commutative: AB $NotEqual; BA (but dot product of 2 vectors is commutative: x<sup>T</sup> y = y<sup>T</sup> x)
- Transpose of a matrix product: (AB)<sup>T</sup> = A<sup>T</sup> B<sup>T</sup>
- And more...

**Identity matrix (I<sub>n</sub>):** Matrix that doesn't change any vector when both are multiplied (I<sub>n</sub> x = x). All the elements along the main diagonal are 1, while the others are zero.

**Inverse matrix (A<sup>-1</sup>):** Matrix that results in the identity when multiplied with the original (A<sup>-1</sup> A = I<sub>n</sub>). 

Use example: Solve **Ax = b** for x (assuming A<sup>-1</sup> exists)
1. Ax = b
2. A<sup>-1</sup>Ax = A<sup>-1</sup>b
3. I<sub>n</sub>x = A<sup>-1</sup>b
4. x = A<sup>-1</sup>b 

The inverse of A may not exist (the equation above must have exactly 1 solution for every value of b). It should not be used in practice for most software applications. A<sup>-1</sup> can only be represented with limited precision on a digital computer, so algorithms that use b can get more accurate estimates of x.

**Linear combination:** Operation that takes a set of vectors, multiplies each one by a corresponding scalar coefficient, and adds the results (&sum;<sub>i</sub>(c<sub>i</sub>v<sup>(i)</sup>)).

Ac = &sum;<sub>i</sub>(c<sub>i</sub>A<sub>:,i</sub>)

**Span:** Set of all vectors obtainable by linear combination of the original vectors. 

Determining whether the system **Ax = b** has a solution amount to testing wheter b is in the span of the columns of A (this span is called column space, or range of A). In order for that system to have solution for all values of b &isin; R<sup>m</sup> we require the column space of A to be all of R<sup>m</sup> (otherwise, any excluded point is a value of b that may have no solution). This means that A must have at leas m columns (n &ge; m); otherwise, the dimensionality of the column space would be lest than m. Example: 

**Linear independence:** A set of vectors are linearly independent if no vector in the set is a linear combination of the other vectors. Adding a vector that is a linear combination of the others doesn't add any points to the set's span. For the column space of a matrix to encompass all of R<sup>m</sup>, the matrix must contain at least one set of m linearly independent columns. In order for a matrix to have an inverse we also need to ensure that Ax=b has at most one solution for each value of b, which requires the matrix to have at most m columns (otherwise, there's more than one way of parametrizing each solution). Thus, the matrix must be square (m=n) and all its columns must be linearly independent (**singular matrix**).

In order for a matrix to have an inverse it has to be **square** (m=n) and all the columns must be linearly independent. If the matrix is not square or if it's singular, it can still be inverted, but not through the method of matrix inversion. 

**Singular matrix:** Square matrix with linearly dependent columns. 

It's also possible to define an inverse that is multiplied on the right (AA<sup>-1</sup> = I). For square matrices, the left and right inverse are equal.

**Norm:** Function used for measuring the size of a vector (distance from origin to x).
- **L<sup>2</sup>** (||x||<sub>p</sub> = (&sum;<sub>i</sub>|x<sub>i</sub>|<sup>p</sup>)<sup>1/p</sup>) (Euclidean norm): It measures the Euclidean distance. It's more convenient to use the squared L<sup>2</sup> (which is = x<sup>T</sup>x), since it has simpler derivatives and less computation. However, it increases very slowly near the origin.
- **L<sup>1</sup>** (||x||<sub>1</sub> = &sum;<sub>i</sub>|x<sub>i</sub>|): It grows at the same rate in all locations while still being simple enough. This is used when the differences between zero and nonzero elements is important (when x moves away from 0 by a, L<sup>1</sup> norm increases by a).
- Sometimes we measure the size of a vector by counting its number of nonzero elements. The L<sup>1</sup> norm is often used as a substitute for the number of nonzero entries.
- **L<sup>&infin;</sup>** (||x||<sub>&infin;</sub> = max<sub>i</sub>|x<sub>i</sub>|) (Max norm): It simplifies to the absolute value of the element with the largest magnitude in the vector.
- **Frobenius norm** (||A||<sub>F</sub> = &radic;(&sum;<sub>i,j</sub>A<sup>2</sup><sub>i,j</sub>)): Used for measuring the size of a matrix. Analogous to L<sup>2</sup>.

The dot product of 2 vectors can be rewritten in terms of norms (&Phi; = angle between x and y):   x<sup>T</sup>y = ||x||<sub>2</sub>||y||<sub>2</sub>cos&Phi;).

**Diagonal matrix:** 


















