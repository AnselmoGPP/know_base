# Random numbers

## Table of Contents
+ [Random-number engines and distributions](#random-number-engines-and-distributions)
  + [Random-number engines operations](#random-number-engines-operations)
  + [Distribution types](#distribution-types)
  + [Engines generate a sequence of numbers](#engines-generate-a-sequence-of-numbers)
  + [Seeding a generator](#seeding-a-generator)
+ [Other kinds of distributions](#other-kinds-of-distributions)
  + [Distribution operations](#distribution-operations)
  + [Generating random real numbers](#generating-random-real-numbers)
  + [Using the distribution’s default result type](#using-the-distribution’s-default-result-type)
  + [Generating numbers that are not uniformly distributed](#generating-numbers-that-are-not-uniformly-distributed)
  + [bernoulli_distribution class](#bernoulli_distribution-class)
+ [Appendix](#appendix)
  + [Random number engines](#random-number-engines)
  + [Random number distributions](#random-number-distributions)


## Random-number engines and distributions

Prior to the new C++11, both C and C++ relied on a simple library function called `rand()` that produces pseudorandom integers in the range from 0 to a system-dependent maximum (`RAND_MAX`) (at least, 32767). However, programmers often introduce non-randomness when trying to transform the range, type or distribution of numbers that it generates.

The random-number library defined in `random` header solves this with a set of cooperating classes:

- **Random-number engines**: Types that generate a sequence of unsigned random numbers.
- **Random number distribution classes**: Types that use an engine to generate random numbers (of a specified type, in a given range) distributed according to a particular probability distribution.

C++ programs should not use `rand()`, they should use `default_random_engine` along with an appropriate distribution object

### Random-number engines operations

**Random-number engines** are **function-object classes (functors)** that define a call operator () that takes no arguments and returns a random **unsigned number**. Generate a raw number by calling an object of a random-number engine type:

```
default_random_engine e;
for(size_t i = 0; i ≺ 10; ++i) std::cout << e() << " ";
```

```
Output: 3484061932 93475 89725894 ...
```

The library defines several random-number engines (see Appendix) with different performance and quality of randomness. Each compiler designates one of them as the `default_random_engine`.

**Random number engine operations**:

- `Engine e`: Default constructor. Uses the default seed for the engine type.
- `Engine e(s)`: Uses the integral value s as seed.
- `e.seed(s)`: Reset the state of the engine using the seed s.
- `e.min()`, `e.max()`: Smallest and largest number this generator will generate.
- `Engine::result_type`: The unsigned integral type this engine generates.
- `e.discard(u)`: Advance the engine by u steps (u has type unsigned long long).

### Distribution types

The engine outputs raw random numbers that usually span a range different than the one we need. To get a number in a specified range, we use a **distribution type** (which are also functors [function-object classes]). We pass an engine to the distribution type and then it uses the engine to produce random numbers that maps to the specified distribution.

```
uniform_int_distribution u(0,9);
default_random_engine e;
for(size_t i = 0; i ≺ 10; ++i) std::cout << u(e) << " ";
```

```
Output: 6 8 0 2 9 ...
```

**Random-number generator (RNG)**: Combination of a distribution object with an engine.

**RN engine + RN distribution = RN generator**


### Engines generate a sequence of numbers

A given random-number generator always produces the same sequence of numbers. A function with a local random-number generator should make that generator (both the engine and distribution objects) `static`, so they hold their state across calls to the function. Otherwise, the function will generate the identical sequence on each call.

```
vector randvec()
{
    static default_random_engine e;
    static uniform_int_distribution u(0,9);
    vector result;
    for(size_t i = 0; i ≺ 100; ++i) result.push_back(u(e));
    return result;
}
```

### Seeding a generator

By providing a seed, an engine can use it to start generating numbers at a new point in its sequence. We can provide the seed when we create an engine object or when we call the engine’s seed member. Engines with the same seed will generate the same sequence.

```
default_random_engine e1;
default_random_engine e2(2340974549);
e1.seed(2340974549);
```

Picking a good seed is hard. It’s common to call the system `time()` function, defined in the header `ctime` (Argument: pointer to a structure where to write the time. If null, it just returns the time. Return value: number of seconds since a given epoch). This seed is useful only for applications that generate the seed at second-level, or longer, intervals.

```
default_random_engine e(time(0));
```


## Other kinds of distributions

The engines produce random unsigned numbers in the engine’s range. Combining an engine with a distribution we can get numbers of different types or distributions.

### Distribution operations

- `Dist d`: Default constructor; makes d ready to use. Other constructors depend on the type of `Dist`. The distribution constructors are `explicit`.
- `d(e)`: Successive calls with the same `e` (random-number engine object) produce a sequence of random numbers according to the distribution type of `d`.
- `d.min()`, `d.max()`: Return the smallest and largest numbers `d(e)` will generate.
- `d.reset()`: Reestablish the state of `d` so that subsequent uses of `d` don’t depend on values `d` has already generated.

### Generating random real numbers

It’s common to obtain a random floating-point in the range [0, 1] from `rand()/RAND_MAX`. However, this is incorrect because random integers usually have less precision than floating-point numbers, so some floating-point values will never be output. The correct way is:

```
default_random_engine e;
uniform_real_distribution u(0,1);
for(int i = 0; i ≺ 10; ++i) std::cout << u(e) << " ";
```

### Using the distribution’s default result type

With one exception, the distribution types are templates that have a single template type parameter that represents the type of the numbers that the distribution generates. These types always generate either a floating-point type or an integral type. Each distribution template has a default template argument, depending on which types they generate:

- Floating-point values  →  double by default
- Integral values →  int by default

When you want to use the default, follow the template’s name with empty angle brackets.

```
uniform_real_distribution≺≻ u(0,1);
```

### Generating numbers that are not uniformly distributed

Example: Generate 100 numbers centered around a mean of 4, with a standard deviation of 1.5. In a normal distribution we can expect all but ~1% of the results to be in the range [0, 8].

```
default_random_engine e;
normal_distribution≺≻ n(4,1.5);
vector≺unsigned≻ vals(9);
for(int i = 0; i != 200; ++i)
{
    unsigned v = lround(n(e));       // Round to nearest integer
    if(v ≺ vals.size()) ++vals[v];
}
```

```
vals = { 3, 8, 20, 38, 58, 42, 23, 7, 1 }
```

### bernoulli_distribution class

This is the only distribution that doesn’t take a template parameter, because it’s a class. It returns a bool value: returns true with a given probability (.5 by default).

```
bernoulli_distribution b(.60);
```

```
string resp;
default_random_engine e;
bernoulli_distribution b;
do{ 
    bool first_player = b(e); 
    // Play the game...
    std::cout << "Play again?" << std::endl;
} while (cin >> resp && resp[0] == 'y');
```

Engines should be declared outside loops to avoid generating the same sequences. Distributions should also be declared outside, so they retain state.


## Appendix

The library defines a collection of:

- **Random number engine classes** (3) and **adaptors** (3) that use differing mathematical approaches to generating pseudorandom numbers. Adaptors modify the sequences produced by a given engine.
- **Distribution templates** that provide numbers according to various probability distributions

Both have names that correspond to their mathematical properties.

### Random number distributions

The distribution types are templates (except `bernouilli_distribution`, which always generates bool values). They take a single type parameter, and produces a result of same type. Unlike other class templates, they place restrictions on the types we can specify for the template type (some distribution templates can only generate floating-point numbers; others, only integers, etc.). We indicate which type a distribution generates by specifying the type as `template_name`:

- _RealT_: float, double, long double
- _IntT_: Any integral type (except bool or char) (i.e. short, int, long, long long, unsigned short, unsigned int, unsigned long, unsigned long long)

The distribution templates define a default template type parameter. The default for the integral distributions is int; the default for the classes that generate floating-point number is double.

The constructors for each distribution has parameters that are specific to the kind of distribution. Some of these parameters specify the range of the distribution. These ranges are always inclusive, unlike iterator ranges.

- **Uniform distributions**

  - `uniform_int_distribution≺IntT≻ u(m,n);`
  - `uniform_real_distribution≺RealT≻ u(x,y);`

Generates values of the specified type in the inclusive range [m, n] (default: [0, max. value for IntT]) or [x, y] (default: [0, 1]).

- **Bernoulli distributions**

  - `bernoulli_distribution b(p)` → Yields true with probability p (default: p = 0.5)
  - `binomial_distribution≺IntT≻ b(t,p)` → Computed for a sample of size t, with probability p (default: t=1, p=0.5)
  - `geometric_distribution≺IntT≻ g(p)` → Per-trial probability of success p (default: p=0.5)
  - `negative_binomial_distribution≺IntT≻ nb(k,p);` → k trials with probability p (default: k=1, p=0.5)

- **Poisson distributions**

  - `poisson_distribution<IntT> p(x)` → Distribution around mean x (double)
  - `exponential_distribution<RealT> e(lam)` → Floating-point valued lambda lam (default: lam=1.0)
  - `gamma_distribution≺RealT≻ g(a,b)` → With alpha a (shape) and beta b (scale) (default: a=b=1.0)
  - `weibull_distribution≺RealT≻ w(a,b)` → With shape a and scale b (default: a=b=1.0)
  - `extreme_value_distribution≺RealT≻ e(a,b)` → (default: a=0.0, b=1.0)

- **Normal distributions**

  - `normal_distribution≺RealT≻ n(m,s)` → Mean m and standard deviation s (default: m=0.0, s=1.0)
  - `lognormal_distribution≺RealT≻ ln(m,s)` → (default: m=0.0, s=1.0)
  - `chi_squared_distribution≺RealT≻ c(x)` → x degrees of freedom (default: x=1.0)
  - `cauchy_distribution≺RealT≻ c(a,b)` → Location a and scale b (default: a=0.0, b=1.0)
  - `fisher_f_distribution≺RealT≻ f(m,n)` → m and n degrees of freedom (default: m=1, n=1)
  - `student_t_distribution≺RealT≻ s(n)` → (default: n=1)

- **Sampling distributions**

  - `discrete_distribution≺IntT≻ d(i,j)` → i and j are input iterators to a sequence of weights
  - `discrete_distribution≺IntT≻ d{il}` → il is a braced list of weights. Weights must be convertible to double
  - `piecewise_constant_distribution≺RealT≻ pc(b,e,w)` → b, e, w are input iterators
  - `piecewise_linear_distribution≺RealT≻ pl(b,e,w)` → b, e, w are input iterators

### Random number engines

The engine and engine adaptor classes are templates. Its parameters are complex and require detailed understanding of the math used.

_Linear congruential_: Old, fast, and with minimal memory requirements ( **multiplier * seed + increment (mod modulus)** ). 

_Subtract with carry_: Based on a generalization of the Fibonacci sequence. Improvement over the linear congruential generator.

_Mersenne twister_: By far, the most widely used general-purpose PRNG. Its period length is chosen to be a Mersenne prime. Implementations generally create random numbers faster than other methods. It requires some amount of memory.

- **Engines**

  - `default_random_engine` → Type alias for one of the other engines
  - [`linear_congruential_engine`](https://en.cppreference.com/w/cpp/numeric/random/linear_congruential_engine)
    - `minstd_rand0` has a multiplier 16807, modulus 2147483647, and increment 0
    - `minstd_rand` has a multiplier 48271, modulus 2147483647, and increment 0
  - [`mersenne_twister_engine`](https://en.cppreference.com/w/cpp/numeric/random/mersenne_twister_engine)
    - `mt19937`: 32-bit unsigned Mersenne twister generator
    - `mt19937_64`: 64-bit unsigned Mersenne twister generator
  - [`subtract_with_carry_engine`](https://en.cppreference.com/w/cpp/numeric/random/subtract_with_carry_engine)
    - `ranlux24_base`: 32-bit unsigned subtract with carry generator
    - `ranlux48_base`: 64-bit unsigned subtract with carry generator
  - [`random_device`](https://en.cppreference.com/w/cpp/numeric/random/random_device) is a uniformly-distributed integer random number generator that produces non-deterministic random numbers.

- **Adaptors**

  - `discard_block_engine` → Engine adaptor that discards results from its underlying engine. Parameterized by the underlying engine to use the block size, and ize of the used blocks.
    - `ranlux24`: Uses the `ranlux24_base` engine with a block size of 223 and a used block size of 23
    - `ranlux48`: Uses the `ranlux48_base` engine with a block size of 389 and a used block size of 11
  - `independent_bits_engine` → Generates numbers with a specified number of bits. Parameterized by the underlying engine to use, the number of bits to generate in its results, and an unsigned integral type to use to hold the generated bits. The number of bits specified must be less than the number of digits that the specified unsigned type can hold.
  - `shuffle_order_engine` → Returns the same numbers as its underlying engine but delivers them in a different sequence. Parameterized by the underlying engine to use and the number of elements to shuffle. `knuth_b` uses the `minstd_rand0` engine with a table size of 256.


## References

- [Pseudo-random number generation](https://en.cppreference.com/w/cpp/numeric/random)
- [std::rand](https://en.cppreference.com/w/cpp/numeric/random/rand)