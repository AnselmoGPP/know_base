# GoogleTest basics


## Table of Contents

+ [References](#references)
+ [Introduction](#introduction)
+ [Assertions](#assertions)
+ [Simple tests](#simple-tests)
+ [Test fixtures](#test-fixtures)
+ [Invoking tests](#invoking-tests)
+ [Writing main()](#writing-main)


## References

- [GoogleTest primer](https://google.github.io/googletest/primer.html)
- [User's guide](https://google.github.io/googletest/)
- [Generic build instructions](https://github.com/google/googletest/blob/main/googletest/README.md)
- [Repository](https://github.com/google/googletest)


## Introduction

**GoogleTest**: Testing framework for C++ that supports any kind of tests (not just unit tests) and many platforms (Linux, Windows, Mac). Developed by Google. Based on the xUnit architecture. Some properties of its tests are:

- Independent & repeatable: Tests are isolated by running each one on a different object. Useful for debugging.
- Well organized: Test groups are related into test suits that can share data and subroutines. Useful for maintainability.
- Portable & reusable: The code is platform-neutral different OSs, compilers, and with or without exceptions).
- Provide as much information about a test fail as possible: If a test fails, it stops and continues with the next (instead of stop at the first test failure).
- Focus on testing: It automatically keeps track of all tests (no need to enumerate them in order to run them).
- Fast: You can reuse shared resources across tests.

**Assertions**: Statements that check whether a condition is true. Possible results: `success`, `nonfatal`, `failure`, `fatal failure` (this one aborts the current function).

**Test case**: A single test. Exercises a particular program path with specific input values and verifies the results. It uses assertions to verify the tested code's behavior. It suceeds if it neither crash nor has a failed assertion.

**Test suite**: Group of related tests. They reflect the structure of the tested code. Objects and subroutines shared by multiple tests in a test suite can be put into a **test fixture** class.

**Test program**: Can contains multiple test suites.


### Assertions

Assertions are macros that resemble function calls. You test a class or function by making assertions about its behavior. When an assertion fails, it's printed the source file, line number, and a failure message, and you can append a custom message.

Two types of assertions:

- `ASSERT_*`: Generates fatal failures when they fail and abort the current function. Useful when it doesn't make sense to continue the test after a failure. An abortion may cause a space leak.
- `EXPECT_*`: Generates nonfatal failures. This is usually preferred since it allows more than one failure to be reported in a test. Useful for letting the test continue to revealing more errors after the assertion failure.

To provide a custom failure message, use `<<` to stream it into the macro. Anything that can be streamed to an `ostream` can be streamed to an assertion macro (like C-string and `std::string`). Wide strings (like `wchar_t*`, `TCHAR*`, and `std::wstring`)

- `ASSERT_EQ(x.size(), y.size()) << "Vectors of unequal length"`.

GoogleTest provides different assertions for verifying your code's behavior in various ways. For a complete list, see the [Assertions Reference](https://google.github.io/googletest/reference/assertions.html):

- Explicit success/failure:
  - `SUCCEED`
  - `FAIL`
  - `ADD_FAILURE`
  - `ADD_FAILURE_AT`
- Generalized assertion:
  - `EXPECT_THAT`
- Boolean conditions:
  - `EXPECT_TRUE`
  - `EXPECT_FALSE`
- Binary comparison:
  - `EXPECT_EQ`
  - `EXPECT_NE`
  - `EXPECT_LT`
  - `EXPECT_LE`
  - `EXPECT_GT`
  - `EXPECT_GE`
- String comparison:
  - `EXPECT_STREQ`
  - `EXPECT_STRNE`
  - `EXPECT_STRCASEEQ`
  - `EXPECT_STRCASENE`
- Floating-point comparison:
  - `EXPECT_FLOAT_EQ`
  - `EXPECT_DOUBLE_EQ`
  - `EXPECT_NEAR`
- Exception assertions:
  - `EXPECT_THROW`
  - `EXPECT_ANY_THROW`
  - `EXPECT_NO_THROW`
- Predicate assertions:
  - `EXPECT_PRED*`
  - `EXPECT_PRED_FORMAT*`
- Windows HRESULT assertions:
  - `EXPECT_HRESULT_SUCCEEDED`
  - `EXPECT_HRESULT_FAILED`
- Death assertions:
  - `EXPECT_DEATH`
  - `EXPECT_DEATH_IF_SUPPORTED`
  - `EXPECT_DEBUG_DEATH`
  - `EXPECT_EXIT`


### Simple tests

To create a test:

- Define and name a test function using the `TEST()` macro (ordinary C++ function that doesn't return a value).
- `TEST()` arguments (test suite name, and test name) should not contain underscores (`_`). Logically related tests should be in the same test suite.
- Inside, include your C++ code and assertions to check values.
- The test's result is determined by the assertions.

```
TEST(TestSuiteName, TestName)
{
  ... test body ...
}
```

Example: Test `int factorial(int i);`

```
TEST(FactorialTest, HandlesZeroInput)
{
  EXPECT_EQ(factorial(0), 1);
}

TEST(FactorialTest, HandlesPositiveInput)
{
  EXPECT_EQ(factorial(1), 1);
  EXPECT_EQ(factorial(2), 2);
  EXPECT_EQ(factorial(3), 6);
  EXPECT_EQ(factorial(8), 40320);
}
```


### Test fixtures

Text fixtures allow to reuse the same configuration of objects for several different tests. To create a fixture:

- Derive a class from `testing::Test`. Start its body with `protected:` (we want to access fixture members from sub-classes).
- Inside the class, declare any objects you plan to use.
- If necessary, write a default constructor or `SetUp()` function (use `override`) to prepare the objects for each test.
- If necessary, write a desctructor or `TearDown()` function to release resources allocated in `SetUp()`. Learn more in [FAQ](https://google.github.io/googletest/faq.html#CtorVsSetUp).
- If needed, define subroutines for your tests to share.

When using a fixture, use `TEST_F()` instead of `TEST()` as it allows you to access objects and subroutines in the test fixture:

```
TEST_F(TestFixtureClassName, TestName)
{
  ... test body ...
}
```

You must first define a test fixture class before using it in a `TEST_F()`, or you'll get the compiler error `virtual outside class declaration`.

For each test defined with `TEST_F()`, GoogleTest creates a fresh new test fixture at runtime, immediately initializes it via `SetUp()`, runs the test, cleanups via `TearDown()`, and deletes the test fixture. Different tests in the same test suite have different test fixture objects. The same test fixture is not reused for multiple tests. Any changes one test makes to the fixture don't affect other tests.

- Example: Test fixture

```
class QueueTest : public testing::Test
{
protected:
  QueueTest()
  {
    // q0 remains empty
    q1.enqueue(1);
	q2.enqueue(2);
	q2.enqueue(3);
  }
  // ~QueueTest() override = default;

  Queue<int> q0;
  Queue<int> q1;
  Queue<int> q2;
};
```

- Example: Using a test fixture

```
TEST_F(QueueTest, IsEmptyInitially)
{
  EXPECT_EQ(q0_.size(), 0);
}

TEST_F(QueueTest, DequeueWorks)
{
  int* n = q0_.Dequeue();
  EXPECT_EQ(n, nullptr);

  n = q1_.Dequeue();
  ASSERT_NE(n, nullptr);
  EXPECT_EQ(*n, 1);
  EXPECT_EQ(q1_.size(), 0);
  delete n;

  n = q2_.Dequeue();
  ASSERT_NE(n, nullptr);
  EXPECT_EQ(*n, 2);
  EXPECT_EQ(q2_.size(), 1);
  delete n;
}
```

GoogleTest constructs a `QueueTest` object for test `IsEmptyInitially`, runs the test, and destroys the object. Then, another `QueueTest` object is created for test `DequeueWorks`, the test is run, and the object destroyed.


### Invoking tests

`TEST()` and `TEST_F()` implicitly register their tests with GoogleTest, so you don't have to re-list all your defined tests in order to run them. After defining the tests, you can run them with `RUN_ALL_TESTS()`, which returns `0` if all tests are successful, or `1` otherwise. This runs all tests in your link unit (they can be from different test suits or source files). 

`RUN_ALL_TESTS()` process:

- Saves state of all GoogleTest flags
- Creates a test fixture object for the first test
- Initializes it via `SetUp()`
- Runs the test on the fixture object
- Cleans up the fixture via `TearDown()`
- Deletes the fixture
- Restores the state of all GoogleTest flags
- Repeat the above steps for the next test, until all tests have run

If a fatal failure happens, the subsequent steps will be skipped.

Don't ignore the return value of `RUN_ALL_TESTS()` or you will get a compiler error. The automated testing service determines whether a test has passed based on its exit code, so your `main()` function must return the value of `RUN_ALL_TESTS()`.

Call `RUN_ALL_TESTS()` only once, or it will create conflicts with some advanced GoogleTest features.


### Writing main()

Most users should not need to write their own `main` function and instead link with `gtest_main`, which defines a suitable entry point.

Writing your own `main` function applies when you need to do something custom before the test run that cannot be expressed within the framework of fixtures and test suites. Your own `main`function should return the value of `RUN_ALL_TESTS()`.

```
#include <gtest/gtest.h>

namespace my {
namespace project {
namespace {

// Fixture for testing class Foo
class FooTest : public testing::Test
{
protected:
  FooTest() { /* Do set-up work for each test here */ }
  ~FooTest() override { /* Do clean-up work that doesn't throw exceptions here */ }
  
  // If contructor and destructor are not enough for setting up and cleaning up each test, you can define the following methods:
  
  void SetUp() override { /* Called immediately after constructor, right before each test */ }
  void TearDown() override { /* Called immediately after each test, right before destructor */ }
}

TEST_F(FooTest, MethodBarDoesAbc)
{
  const std::string input_filepath = "this/package/testdata/myinputfile.dat";
  const std::string output_filepath = "this/package/testdata/myoutputfile.dat";
  Foo f;
  EXPECT_EQ(f.Bar(input_filepath, output_filepath), 0);
}

TEST_F(FooTest, DoesXyz) { /* ... */ }

}   // namespace
}   // namespace project
}   // namespace my

int main(int argc, char **argv)
{
  testing::InitGoogleTest(&argc, argv);
  return RUN_ALL_TESTS();
}
```

The `testing::InitGoogleTest()` function parses the command line for GoogleTest flags, and removes all recognized flags, allowing the user control a test program's behavior via various flags (see [more](https://google.github.io/googletest/advanced.html)). You must call this function before calling `RUN_ALL_TESTS()`, or the flags won't be properly initialized.

GoogleTest provides a basic implementation of `main()`. If it fits your needs, then just link your test with the `gtest_main` library.