# Simple PHP Test Harness

## 0. Concept

A minimal PHP testing utility using native `assert()` and a custom `assert_throws()` to register and run named tests. Tests are collected via the `test()` function and executed together with `tests()`, which reports pass/fail counts and exits with a non-zero status if any fail.

## 1. Features

- **Named Tests**  
  Register tests with a descriptive name and a callback.
- **Automatic Collection**  
  Calling `test($name, $callback)` accumulates tests in a static registry.
- **Assertion-Based**  
  Uses PHP’s built‑in `assert()` for boolean checks.
- **Exception Testing**  
  `assert_throws($func, $exceptionClass = '', $expectedMessage = '')` verifies that a callback throws the expected exception type and message.
- **Console Output**  
  Prints a summary: list of passed (`|`) and failed (`x`) tests, plus totals.
- **Exit Code**  
  Exits with status `1` if any test fails, suitable for CI pipelines.

## 2. Usage

```php
<?php
require 'path/to/test.php';

test('dummy passes', function () {
    assert(true, 'This should not fail');
});

test('throws InvalidArgumentException', function () {
    assert_throws(function () {
        throw new InvalidArgumentException('Bad value');
    }, InvalidArgumentException::class, 'Bad value');
});

// Run all registered tests and output results.
// Exits with code 1 if any test fails.
tests();
