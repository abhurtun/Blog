---
layout: default
title: Test Quality
subtitle:
date: April 12, 2018
author: Arvin Bhurtun
---
{% seo %}


# Unit Testing Best Practice

{{ page.date | date_to_string }} {% include readTime.html %}

{% include likeButton.html %}

## Test philosophy

Is captured nicely by this quote:

```

I get paid for code that works, not for tests,
so my philosophy is to test as little as possible
to reach a level of confidence
Kent Beck
Author of "Test Driven Development

```

### Tests cover the happy and unhappy path

Tests should not only cover expected operation but should also cover failure and unexpected inputs. This is particularly the case in systems where the input comes from the outside world.

##### Metrics

Coveralls can show coverage of both the happy and unhappy paths.

![](../img/test.png)

### Test only one thing

Tests should only assert on a single function from the system under test. If the path tested require multiple assertions this would be an exception rather than the rule.

### Fake/Mock all external interfaces.

An external interface could be another service within our micro-service architecture, a database instance or a legacy API. In addition anything that hits the file system or can return non-deterministic data could qualify as an external interface.

### Test is worded consistently

There are many conventions for test naming. Given the simplicity of nUnit I suggest.
```

"Returns 'X' Given 'Y'"

```

### Use consistent variable naming convention

The variable used to capture test data, actual data and the system under test could be

```

sut      : The module which is being tested.
expected : The expected result of the test.
actual   : variable containing the results from the function under test

```

### Asserts are ordered the same

```

assert actual == expected
  as opposed to the rather strange...
assert expected == actual

```

### Tests arrange, act and then assert

Assignments appear in order of expected followed by actual.

### Tests run quickly

A unit test should only be testing processing, not communication so it is absolutely fitting that a time cap is put on a single unit test.

### Tests should mock external dependencies

Mock the external dependencies modules, rather run them directly. Using fakes as opposed to mocks makes it explicit where the boundaries of the system lie.

### Tests should not confirm the operation of external libraries

External libraries should have their tests extended if coverage is poor, if we need to test an external library we should consider looking for an alternative. 

### Tests should not confirm the output of external services.

We should develop contracts between our services that confirm the integrity of data moving between our services. These tests should not be repeated in all clients of a service.

### Test a whole unit of operation not the implementation details

In order to allow free refactoring of the implementation details of a module or cluster of modules only the public interface for those modules should be tested. For example for a prime number function we would want to test that a prime number is returned and not how that prime number was calculated.

### Test behavior and assert your expectation not data

Test that the expected behavior based on the data returned is correct instead of the actual values.

### Long tests

Tests should be short and long tests are code smells as the test are only reflect the design and implementation of the code. Short tests improve the feedback cycles and reduce over engineered solutions.

---

Return to [Blogs](../index.md).