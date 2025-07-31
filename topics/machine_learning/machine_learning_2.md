# Machine learning 2

## Table of Contents
+ [Introduction](#introduction)
+ [Linear regression (one variable)](#linear-regression-one-variable)
+ [Linear regression (multiple variables)](#linear-regression-multiple-variables)
+ [Polynomial regression](#polynomial-regression)
+ [Logistic regression](#logistic-regression)
+ [Regularization](#regularization)
+ [Neural networks](#neural-networks)
+ [Advices](#advices)
+ [Support vector machines](#support-vector-machines)
+ [Unsupervised learning](#unsupervised-learning)
+ [Anomaly detection](#anomaly-detection)
+ [Recommender systems](#recommender-systems)
+ [Large scale machine learning](#large-scale-machine-learning)
+ [Photo OCR](#photo-ocr)


## Introduction

**Mathematical model:** Simplified conceptual reconstruction of a more complex reality. It takes patterns from real-world scenarios and use them for rebuilding it. Then, we can use the model for making predictions. 

**Artificial Intelligence (AI):** Subdiscipline from computer science that want to create machines that can **imitate** intelligent behaviors. Examples: robotics, NLP, voice, vision...
  - **Weak:** It can do a very limited number of tasks.
  - **Strong:** It applies to a wide variety of tasks and domains.

**Machine learning (ML):** Field of AI that study that gives computers the ability to learn without being explicitly programmed. A computer program learns from experience E with respect to some task T and some performance measure P, if T, as measured by P improves with E. if the measured P improves with E. Main machine learning algorithms: Supervised, Unsupervised, Reinforced.

- **Supervised learning:** Most common. We teach the computer by giving the algorithm a data set (training set) in which the "right answers" are given, so it can learn the relation between them. A learning algorithm can deal with an infinite number of features/attributes with which make predictions. To deal with this infinite amount without running out of memory we use an algorithm called Support Vector Machine. Two types of problems: 
  - **Regression problem:** Predicts continuous valued output.
  - **Classification problem:** Predicts discrete valued output.
- **Unsupervised learning** (or clustering): We don't give the right answer to the algorithm, it learns by itself. Used to organize large computer clusters. The conceptual structures it learns are called latent spaces, which allows to learn if something is similar to another thing (like 2 words) and operate mathematically with concepts.
- **Reinforcement learning**
- **Recommender systems**

There are different techniques in ML: Decision trees, Regression models, Classification models, Clusterization, Neural networks, etc.
- **Neural networks:** They learn basic concepts at the beginning (screw, wheel, mirror...), and build on them to learn about more complex concepts (car, truck...). The more layers it has, the more abstract knowledge it can get.

**Training set:** Portion of a **data set** used to fit (train) a model for prediction or classification of values that are known in the training set, but unknown in other (future) data. Example:
- Training set of housing prices (we want to predict prices):
  - Size in feet<sup>2</sup> (x): 2104, 1416, 1534, 852
  - Price in $ (y): 460.000, 232.000, 315.000, 178.000
- m: number of training examples
- x's: input variable (features)
- y's: output variable (target)
- (x, y): One training example
- (x<sup>(i)</sup>, y<sup>(i)</sup>): i<sup>th</sup> training example

**Learning algorithm:** Algorithm that takes a **training set** (x<sup>(i)</sup>, y<sup>(i)</sup>) as input, and outputs a function (h, hypothesis) that, given an input (x), offers an output (y).


## Linear regression (one variable)

### Cost function

**Cost function:** Learning algorithm for **supervised learning**. The hypothesis (h) will be a linear function (straight line). Represented as: 

h<sub>&theta;</sub>(x) = &theta;<sub>0</sub> + &theta;<sub>1</sub>x

- &theta;<sub>0</sub>: ordinate in the origin
- &theta;<sub>1</sub>: slope

Given a training set, choose a value for each parameter (&theta;<sub>0</sub> and &theta;<sub>1</sub>x) so that h<sub>&theta;</sub>(x) is close to **y** for out training examples (x, y).

We want to make small this expression (minimization problem): 

(h<sub>&theta;</sub>(x) - y)<sup>2</sup>

**Square error cost function (J):** It's the most commonly used cost function in regression problems (though there are others). We want to find the values for the parameters (&theta;<sub>0</sub>, &theta;<sub>1</sub>...) that minimize J. 

J(&theta;<sub>0</sub>, &theta;<sub>1</sub>) = (1/2m) &sum;<sub>m,1</sub>(h<sub>&theta;</sub>(x<sup>(i)</sup>) - y<sup>(i)</sup>)<sup>2</sup>

- (1/2m) is used for calculating the average multiplied by 1/2, which makes the math easier.

Example: We want to find the function (h<sub>&theta;</sub>(x) = &theta;<sub>0</sub> + &theta;<sub>1</sub>x) that best models a scenario (like housing prices as a function of different parameters), which requires us to find the correct parameters. On a graph, it plots a straight line. There is also a cost function J(&theta;<sub>0</sub>, &theta;<sub>1</sub>) that plots a concave surface (if we only have one parameter, it's a parabola). The correct values of the parameters are those that make J = 0 (or close).

Note 2: Every h<sub>&theta;</sub>(x<sup>(i)</sup>) - y<sup>(i)</sup>)<sup>2</sup> is the vertical distance between (x<sup>(i)</sup>, y<sup>(i)</sup>) (computed output given our parameters) and the real output (given by a data set).

Note 2: Instead of 3D charts we can use contour plot/figures. They draw sets of points (&theta;<sub>0</sub>, &theta;<sub>0</sub>) that have the same value for J. Each point represents a unique h<sub>&theta;</sub>(x) function.

### Gradient descent

**Gradient descent (GD):** Algorithm for minimizing the cost funcion J. Used all over the place in machine learning (not only linear regression). We start with some parameters (&theta;<sub>0</sub>, &theta;<sub>1</sub>...) and keep changing their values to reduce J until we hopefully end up at a minimum. These changes are toward points that go downwards in J.

- **Batch GD:** Each step of GD uses all the training examples (other types may use a subset of training examples).

for(until convergence) {  &theta;<sub>j</sub> = &theta;<sub>j</sub> - &alpha;(&delta;J(&theta;<sub>0</sub>,&theta;<sub>1</sub>)/&delta;&theta;<sub>j</sub>)  }

- &alpha;: Learning rate. It controls how big a step we take downhill. If &alpha; is too small, GD can be slow. If &alpha; is too large, GD can overshoot the minimum (fail to converge, or even diverge). GD can converge to a local minimum even if &alpha; is kept fixed (as we approach to a local minimum, GD automatically takes smaller steps) so there's no need to decrease &alpha; over time.
- &delta;J(&theta;<sub>0</sub>,&theta;<sub>1</sub>)/&delta;&theta;<sub>j</sub>: Partial derivative (it represents the slope of J graph for component &theta;<sub>j</sub>). We look for a derivative = 0 or close.
- d: Non-partial derivative symbol.

We compute the algorithm simultaneouly for every &theta;<sub>j</sub> (i.e. for each &theta; parameter) in order to update every &theta;. Then we compute y again with the new values for &theta; (iteration). And so on.

Compute partial derivatives:
&delta;J(&theta;<sub>0</sub>,&theta;<sub>1</sub>) / &delta;&theta;<sub>j</sub> = (&delta;/&delta;&theta;<sub>j</sub>)(1/2m) &sum;<sup>m</sup><sub>i=1</sub>(&theta;<sub>1</sub>x<sup>(i)</sup><sub>1</sub> + &theta;<sub>0</sub>x<sup>(i)</sup><sub>0</sub> - y<sup>(i)</sup>)<sup>2</sup>
- &delta;J(&theta;<sub>0</sub>,&theta;<sub>1</sub>) / &delta;&theta;<sub>0</sub> = (1/m) &sum;<sup>m</sup><sub>i=1</sub>(h<sub>&theta;</sub>(x<sup>(i)</sup>) - y<sup>(i)</sup>)   (x<sub>0</sub>=1)
- &delta;J(&theta;<sub>0</sub>,&theta;<sub>1</sub>) / &delta;&theta;<sub>1</sub> = (1/m) &sum;<sup>m</sup><sub>i=1</sub>(h<sub>&theta;</sub>(x<sup>(i)</sup>) - y<sup>(i)</sup>)   (x<sub>0</sub>=1) · x<sup>(i)</sup><sub>1</sub>

Now we can introduce both derivatives in our algorithm and use it to minimize J. Cost function of linear regression is a convex function, and doesn't have local optima except for the one global optimum.

**Normal equation method:** Solution for numerically solving for the minimum of the cost function J without using an iterative algorithm like GD. However, GD scales better to larger data sets.


## Linear regression (multiple variables)

We can take into account more than one variable/feature (x<sub>1</sub>=size, x<sub>2</sub>=bedrooms, x<sub>3</sub>=floors, x<sub>4</sub>=age) for every result (y=price).

- n: number of features (previously we used n to denote the number fo examples in the training set).
- x<sup>(i)</sup>: Vector containing all the features in the i<sup>th</sup> training example.
- x<sup>(i)</sup><sub>j</sub>: Value of feature j in x<sup>(i)</sup>.

**Hypothesis:**  h<sub>&theta;</sub>(x) = &theta;<sub>0</sub>x<sub>0</sub> + &theta;<sub>1</sub>x<sub>1</sub> + &theta;<sub>2</sub>x<sub>2</sub> + &theta;<sub>3</sub>x<sub>3</sub> + &theta;<sub>4</sub>x<sub>4</sub>          (x<sub>0</sub>=1)

Now we have 2 vectors: 

x<sup>(i)</sup><sub>nx1</sub> = [ x<sub>0</sub>, x<sub>1</sub>, x<sub>2</sub>,... x<sub>n</sub> ]  (column vector)
&theta;<sub>nx1</sub> = [ &theta;<sub>0</sub>, &theta;<sub>1</sub>, &theta;<sub>2</sub>,... &theta;<sub>n</sub> ]  (column vector)

h<sub>&theta;</sub>(x<sup>(i)</sup>) = &theta;<sup>T</sup>·x<sup>(i)</sup>

**Cost function:** J(&theta;<sub>0</sub>,&theta;<sub>1</sub>...&theta;<sub>n</sub>) = J(&theta;) = (1/2m) &sum;<sup>m</sup><sub>i=1</sub>(h<sub>&theta;</sub>(x<sup>(i)</sup>) - y<sup>(i)</sup>)<sup>2</sup>

**Gradient descent:** The following is used for updating all parameters simultaneously.

for(until convergence) {  &theta;<sub>j</sub> = &theta;<sub>j</sub> - &alpha &delta;J(&theta;)/&delta;&theta;<sub>j</sub>;  }
for(until convergence) {  &theta;<sub>j</sub> = &theta;<sub>j</sub> - &alpha (1/m) &sum<sup>m</sup><sub>i=1</sub>(h<sub>&theta;</sub>(x<sup>(i)</sup>) - y<sup>(i)</sup>) · x<sup>(i)</sup><sub>j</sub>;  }

**Steps:**
1. Choose a type of **h(x)**
2. Obtain **J(&theta;)** using training examples and initial values for &theta;
3. Minimize J(&theta;) using **GD** (obtain all &theta; in every iteration simultaneously)
4. Now we have the optimal h(x)

**Normalization:**

- **Feature scaling:**
When using multiple features, if we make them have similar scale (similar ranges of values), then GD can converge faster. Otherwise, our contour plot may have sharp shapes that make GD longer to calculate the minimum. Make every feature into approximately a range of -1&le;x<sub>i</sub>&le;1 (x<sub>0</sub> is already in range since it's = 1). Divide by the range of x<sub>i</sub> (s<sub>i</sub>=max-min) (alternatively, by the Standard Deviation). Range values of [0, 3] or [-2, 0.5] are acceptable, but ranges [-100, 100] or [-0.0001, 0.0001] are poorly scaled.

- **Mean normalization:**
Used with feature scaling. Make features have approximetely zero mean by replacing x<sub>i</sub> with x<sub>i</sub>-&mu;<sub>i</sub> (don't apply to x<sub>0</sub>=1) (&mu;: mean of x<sub>i</sub> in the training set). It makes GD converge faster.
Combine mean normalization and feature scaling:  x<sub>i</sub> = (x<sub>i</sub>-&mu;<sub>i</sub>)/s<sub>i</sub>
To make predictions, we must first normalize x using the mean and standard deviation previously applied to the training set.

- **Learning rate (&alpha;):**

Two ways of selecting an &alpha; that makes GD work correctly; (debugging):
  - Plot J(&theta;) against the number of iterations. J should decrease with each iteration. The number of iterations till convergence (flat line) vary much among applications. If J increases or goes up and down, you should use a smaller &alpha;. A small &alpha; should decrease J on every iteration, but if it's too small, gradient descent can be slow to converge. Check different values of &alpha; to get good plot (recommendation: try values on a log-scale at about 3 times the previous value: 0.1, 0.03, 0.01, 0.003, 0.001).
  - Use an algorithm that tells if gradient descent has converged (example: declare convergence if J decreases by less than &epsilon; in one iteration). However, choosing &epsilon; is pretty difficult, so using plot may be preferable.

- **Feature edition:**
Sometimes we can combine some features to create a new feature (example: "terrain width" and "terrain depth" may be combined into "terrain area"), reducing the total amount of features.


## Polynomial regression

We may decide that a quadratic/cubic/etc. polynomial model fits better the data (rather than a linear one). 

h<sub>&theta;</sub>(x) = &theta;<sub>0</sub> + &theta;<sub>1</sub>x + &theta;<sub>2</sub>x<sup>2</sup> + ... + &theta;<sub>n</sub>x<sup>n</sup>

We can fit this model into our data introducing simple modifications to our multivariant linear regression algorithm. Example: if we have one feature (house size) for the price of houses, we can create 2 additional features:

h<sub>&theta;</sub>(x) = &theta;<sub>0</sub> + &theta;<sub>1</sub>x + &theta;<sub>2</sub>x<sup>2</sup> + &theta;<sub>3</sub>x<sup>3</sup>   where x<sub>1</sub>=size, x<sub>2</sub>=size<sup>2</sup>, x<sub>3</sub>=size<sup>3</sup>

Even though we have polynomial terms, we are still solving a linear regression optimization problem. The polynomial terms have turned into features we can use for linear regression.

Feature scaling becomes increasingly important because these features take very different ranges of values.

There exists many other choices of features (example: h<sub>&theta;</sub>(x) = &theta<sub>0</sub> + &theta<sub>1</sub>(size) + &theta<sub>2</sub>(&radic;size))

**Normal equation (NE):** 

Method for solving &theta; analytically in linear regression problems. Cost function J is a function of vector &theta;. If we take the partial derivative of J with respect to every parameter of &theta; and set these derivatives to 0, we obtain the values of &theta; to minimize J. 

Consider m=4 (examples) and n=4 (features). We create 2 matrices (X<sub>mx(n+1)</sub>, y<sub>mx1</sub>). To obtain the value of &theta; that minimizes J just compute:

&theta; = (X<sup>T</sup>X + &lambda;Z)<sup>-1</sup> X<sup>T</sup>·y
Code instruction: pinv(X'*X)*X'*y

Using NE we don't need iterating, choosing &alpha, or feature scaling. However, it's slow if n is very large, and we need to compute (X<sup>T</sup>·X)<sup>-1</sup> (the cost of inverting is about the cube of the dimension of the matrix). NE es acceptable for about n&le;10.000. 

Using GD, we need to iterate ad choose &alpha;, but it works well even when n is large. GD is good for n&ge;100.000.

If (X<sup>T</sup>·X) is not invertible (singular, degenerate) we can calculate the **pseudo-inverse** (instead of the normal inverse) which always get an inverse. It works well, but it's not clear that it would give you a very good hypothesis. The reasons why (X<sup>T</sup>·X) may not be invertible are:
- Reduntant features (linearly dependent). Example: if x<sub>1</sub>=size in feet<sup>2</sup>, and x<sub>2</sub>=size in m<sup>2</sup>, then x<sub>1</sub>=10.8x<sub>2</sub>
- Fewer examples than features (m&le;n). Delete some features or use Regularization.


## Logistic regression

## Regularization

## Neural networks

## Advices

## Support vector machines

## Unsupervised learning

## Anomaly detection

## Recommender systems

## Large scale machine learning

## Photo OCR