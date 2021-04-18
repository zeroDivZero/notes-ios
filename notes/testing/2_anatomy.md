# ANATOMY

## Import `XCTest`

```swift
#import XCTest
```

Framework of all testing functionality.

## Import Module to Test

```swift
@testable import MyApp
```

Import module to test, typically main app. Since tests are in separate module, `@testable` gives tests access control of tested module at `internal` level, so no need to change source to add `public`.

## Test Class

```swift
class MyAppTests: XCTestCase {
```

Defines tests logically grouped together. Typically one test class per class or entity to be tested.

Must extend `XCTestCase`. Xcode automatically scans test bundle for all `XCTestCase` subclasses to find tests to run.

## Test Class Methods

Can override instance methods `setUp()` and `tearDown()` (or `setUpWithError()` and `tearDownWithError()` if need to throw errors), which are called before and after each test.

Can override class methods `setUp()` and `tearDown()` called before and after running all tests.

Order of execution:

```swift
class func setUp()
setUp()
testMethodOne()
tearDown()
setUp()
testMethodThree()
tearDown()
setUp()
testMethodTwo()
tearDown()
class func tearDown()
```

Tests executed in alphabetical order, hence `testMethodThree()` before `testMethodTwo()`, regardless of order in `MyAppTests`. Important to keep tests independent (to avoid `test001AddUser()`).

Xcode creates instance of test class for _each_ test. If there are 3 tests, 3 instances of `MyAppTests` are created. If test needs any object, best declared as optional property, created in `setUp()`, and destroyed in `tearDown()`.

## Test Methods

Each test method must:

1. Have name starting with word "test".
2. Accept no params.
3. Return nothing.

After Xcode finds all `XCTestCase` subclasses, it scans each for matching methods with above rules, treating them as tests.

Typical naming convention:
**UnitOfWork_StateUnderTest_ExpectedBehavior**

E.g.:

```swift
func test_Balloon_AfterNeedlePoke_ShouldPop() {
```

## Assertion

Use one (or more, but usually one per test) of assert funcs to verify result of test matches expectation. Examples:

```swift
XCTAssert()
XCTAssertTrue(), XCTAssertFalse()
XCTAssertNil(), XCTAssertNotNil()
XCTAssertEqual(), XCTAssertNotEqual()
XCTAssertThrowsError(), XCTAssertNoThrow()
```

May be tempted to use only `XCTAssert()` or `XCTAssertTrue()`, but more specific assert makes test more readable, and error message more descriptive if test fails.

Every assert func allows custom error message:

```swift
XCTAssertFalse(ballon.popped, "Balloon should not be
popped.")
XCTAssertEqual(correctLengthInMeters, testedLengthInMeters,
"meters")
```

## Structure of Test Method

Typically structured with **Arrange, Act, Assert** paradigm, which breaks test into 3 steps:

1. Set things up for test.
2. Execute code to be tested.
3. Evaluate result of test.

Also referred to as *Given, When, Then* (common to see these steps as comments in test).
