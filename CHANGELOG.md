### 0.12.0-beta.2

* Rename the package to `test`. The `unittest` package will continue to exist
  through the `0.12.0` cycle, but it's deprecated and will just export the
  `test` package.

* Remove the deprecated members from `test`. These members will remain in
  `unittest` for now.

### 0.12.0-beta.1

* Add a `--name` (shorthand `-n`) flag to the test runner for selecting which
  test to run.

* Ensure that `print()` in tests always prints on its own line.

* Forward `print()`s from browser tests to the command-line reporter.

* Add a missing dependency on `string_scanner`.

## 0.12.0-beta.0

* Added support for a test runner, which can be run via `pub run
  test:test`. By default it runs all files recursively in the `test/`
  directory that end in `_test.dart` and aren't in a `packages/` directory.

* As part of moving to a runner-based model, most test configuration is moving
  out of the test file and into the runner. As such, many ancillary APIs are
  stubbed out and marked as deprecated. They still exist to make adoption
  easier, but they're now no-ops and will be removed before the stable 0.12.0
  release. These APIs include `skip_` and `solo_` functions, `Configuration` and
  all its subclasses, `TestCase`, `TestFunction`, `testConfiguration`,
  `formatStacks`, `filterStacks`, `groupSep`, `logMessage`, `testCases`,
  `BREATH_INTERVAL`, `currentTestCase`, `PASS`, `FAIL`, `ERROR`, `filterTests`,
  `runTests`, `ensureInitialized`, `setSoloTest`, `enableTest`, `disableTest`,
  and `withTestEnvironment`.

* Removed `FailureHandler`, `DefaultFailureHandler`,
  `configureExpectFailureHandler`, and `getOrCreateExpectFailureHandler` which
  used to be exported from the `matcher` package. They existed to enable
  integration between `test` and `matcher` that has been streamlined.

* Moved a number of APIs from `matcher` into `test`, including:
  `completes`, `completion`, `ErrorFormatter`, `expect`,`fail`, `prints`,
  `TestFailure`, `Throws`, and all of the `throws` methods.

    * `expect` no longer has a named `failureHandler` argument.

    * `expect` added an optional `formatter` argument.

    * `completion` argument `id` renamed to `description`.

* Removed several members from `SimpleConfiguration` that relied on removed
  functionality: `onExpectFailure`, `stopTestOnExpectFailure`, and 'name'.

##0.11.5+1

* Internal code cleanups and documentation improvements.

##0.11.5

* Bumped the version constraint for `matcher`.

##0.11.4

* Bump the version constraint for `matcher`.

##0.11.3

* Narrow the constraint on matcher to ensure that new features are reflected in
  unittest's version.

##0.11.2

* Prints a warning instead of throwing an error when setting the test
  configuration after it has already been set. The first configuration is always
  used.

##0.11.1+1

* Fix bug in withTestEnvironment where test cases were not reinitialized if
  called multiple times.

##0.11.1

* Add `reason` named argument to `expectAsync` and `expectAsyncUntil`, which has
  the same definition as `expect`'s `reason` argument.
* Added support for private test environments.

##0.11.0+6

* Refactored package tests.

##0.11.0+5

* Release test functions after each test is run.

##0.11.0+4

* Fix for [20153](https://code.google.com/p/dart/issues/detail?id=20153)

##0.11.0+3

* Updated maximum `matcher` version.

##0.11.0+2

*  Removed unused files from tests and standardized remaining test file names.

##0.11.0+1

* Widen the version constraint for `stack_trace`.

##0.11.0

* Deprecated methods have been removed:
    * `expectAsync0`, `expectAsync1`, and `expectAsync2` - use `expectAsync`
      instead
    * `expectAsyncUntil0`, `expectAsyncUntil1`, and `expectAsyncUntil2` - use
      `expectAsyncUntil` instead
    * `guardAsync` - no longer needed
    * `protectAsync0`, `protectAsync1`, and `protectAsync2` - no longer needed
* `matcher.dart` and `mirror_matchers.dart` have been removed. They are now in
  the `matcher` package.
* `mock.dart` has been removed. It is now in the `mock` package.

##0.10.1+2

* Fixed deprecation message for `mock`.

##0.10.1+1

* Fixed CHANGELOG
* Moved to triple-slash for all doc comments.

##0.10.1

* **DEPRECATED**
    * `matcher.dart` and `mirror_matchers.dart` are now in the `matcher`
      package.
    * `mock.dart` is now in the `mock` package.
* `equals` now allows a nested matcher as an expected list element or map value
  when doing deep matching.
* `expectAsync` and `expectAsyncUntil` now support up to 6 positional arguments
  and correctly handle functions with optional positional arguments with default
  values.

##0.10.0

* Each test is run in a separate `Zone`. This ensures that any exceptions that
occur is async operations are reported back to the source test case.
* **DEPRECATED** `guardAsync`, `protectAsync0`, `protectAsync1`,
and `protectAsync2`
    * Running each test in a `Zone` addresses the need for these methods.
* **NEW!** `expectAsync` replaces the now deprecated `expectAsync0`,
    `expectAsync1` and `expectAsync2`
* **NEW!** `expectAsyncUntil` replaces the now deprecated `expectAsyncUntil0`,
    `expectAsyncUntil1` and `expectAsyncUntil2`
* `TestCase`:
    * Removed properties: `setUp`, `tearDown`, `testFunction`
    * `enabled` is now get-only
    * Removed methods: `pass`, `fail`, `error`
* `interactive_html_config.dart` has been removed.
* `runTests`, `tearDown`, `setUp`, `test`, `group`, `solo_test`, and
  `solo_group` now throw a `StateError` if called while tests are running.
* `rerunTests` has been removed.
