# Unit Testing Best Practice

{{ page.date | date_to_string }} {% include readTime.html %}

{% include likeButton.html %}

We gathered as a team and brainstormed all the best and worst practices in testing from our very subjective viewpoint. We also brainstormed how we could give suggestions to highlight inconsistent or bad practice. Here they are presented to gather everyones additions, changes, and removals.

### Our test philosophy 
Is captured nicely by this quote:

```
"I get paid for code that works, not for tests,
so my philosophy is to test as little as possible
to reach a level of confidence"  
Kent Beck  
Author of "Test Driven Development"
```
---

### Tests cover the happy and unhappy path.

##### Description

Tests should not only cover expected operation but should also cover failure and unexpected inputs. This is particularly the case in systems where the input comes from the outside world.

##### Metrics

Coveralls can show coverage of both the happy and unhappy paths.

```
----------------
COV    FILE                                        LINES RELEVANT   MISSED
100.0% repository.cs                                  28        4        0
 75.0% api/client.cs                                  54        8        2
[TOTAL]  75.0%
----------------
```
---

### Test only one thing

##### Description

Tests should only assert on a single function from the system under test. If the path tested require multiple assertions this would be an exception rather than the rule.

---


### Fake all external interfaces.

##### Description

An external interface could be another service within our micro-service architecture, a database instance or a legacy API. In addition anything that hits the file system or can return non-deterministic data could qualify as an external interface.

---

### Test is worded consistently

##### Description

There are many conventions for test naming. Given the simplicity of xUnit I suggest.
```
  "In 'X' when 'Y' it should 'Z'"
```

---

### Use consistent variable naming convention

##### Description

The variable used to capture test data, actual data and the system under test could be

```
sut      : The module which is being tested.
expected : The expected result of the test.
actual   : variable containing the results from the function under test
```

##### Exceptions

When a test is under 5 lines of code expected and actual should be optional

---

### Asserts are ordered the same.

##### Description

```
assert actual == expected
  as opposed to the rather strange...
assert expected == actual
```

##### Exceptions

When a test is under 5 lines of code expected and actual should be optional

---

### Tests arrange, act and then assert.

##### Description

Assignments appear in order of expected followed by actual.

##### Exceptions

When a test is under 5 lines of code expected and actual should be optional

---

### Tests run quickly.

##### Description

A unit test should only be testing processing, not communication so it is absolutely fitting that a time cap is put on a single unit test.

---

### Tests should mock external dependencies.

##### Description

Mock the external dependcies modules, rather run them directly. Using fakes as opposed to mocks makes it explicit where the boundaries of the system lie.

---

### Tests should not confirm the operation of external libraries.

##### Description

External libraries should have their tests extended if coverage is poor, if we need to test an external library we should consider looking for an alternative. 

---

### Tests should not confirm the output of external services.

##### Description

We should develop contracts between our services that confirm the integrity of data moving between our services. These tests should not be repeated in all clients of a service.

---

### Test a whole unit of operation not the implementation details.

##### Description

In order to allow free refactoring of the implementation details of a module or cluster of modules only the public interface for those modules should be tested. For example for a prime number function we would want to test that a prime number is returned and not how that prime number was calculated.

---

### Test schema not data.

##### Description

Test that the schema of the data returned is correct instead of the actual values. If the data is extended with an array now containing say more entries we want tests to succeed provided that the schema for that returned data is correct.

---

### Long tests.

##### Description

Tests should be short and long tests should be schema tests.

---

Return to [Blogs](../index.md).