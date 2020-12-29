# TIPS

## `sut`

Often see variable declared as `sut`, which stands for *system under test*, that refers to subject to test.

```swift
let sut = MyClass()
sut.doSomething()
XCTAssertTrue(sut.doneSomething)
```

## `XCTUnwrap()`

Asserts expression not `nil`, and returns unwrapped value. Saves having to do optional binding with `guard` or `if let`.

```swift
let myInt = try XCTUnwrap(myIntOptional)
```

## `XCTSkip`

Error to cause test to stop and be marked as skipped when thrown. Allows skipping test based on runtime info (e.g., not testing iPad-specific feature on iPhone sim, network down, etc.).

```swift
guard #available(iOS 13.4, *) else {
    throw XCTSkip("Pointer tests can only be run on iOS 13.4+.")
}
```

Xcode marks test with "skip" icon different from pass or fail.

`XCTSkipIf()` and `XCTSkipUnless()` are functions that skip based on condition.

```swift
try XCTSkipIf(UIDevice.current.userInterfaceIdiom != .pad,
              "Pointer tests are for iPad only.")

try XCTSkipUnless(UIDevice.current.userInterfaceIdiom == .pad,
                  "Pointer tests are for iPad only.")
```

May be preferable to prepending prefix like "DISABLED_" to test method name, since those tests do not show up in Xcode test log.

## Floating-Point Accuracy

Typically not desirable to assert exact equality of float-points due to rounding error. Can use assertion function with `accuracy` param:

```swift
XCTAssertEqual(CGFloat.pi, 3.14, accuracy: 0.01)
```

## `continueAfterFailure`

`XCTestCase` property to indicate test method should continue after failure occurs. Default `true`.

May want to set to `false` in `setUp()` (typically for UI tests) if after failure state no longer valid, to avoid *assertion roulette*.

```swift
continueAfterFailure = false
```

## `executionTimeAllowance`

`XCTestCase` property for number of seconds, rounded up to minute, for test to run before timeout error. Default 600 (10 min).

Requires timeout enabled: set **Test Timeouts** to **On** in test plan, or set `-test-timeouts-enabled` to `YES` with `xcodebuild`.

May be less if set **Maximum Test Execution Time Allowance** in test plan, or set `-maximum-test-execution-time-allowance` with `xcodebuild`.

## `#filePath`

If using helper to assert, may want to add `file` and `line` so failure is annotated at test and not helper function.

`#file` expands to absolute path, which causes bloat and security leaks (it's used throughout toolchain, not just tests), so it has been shortened to relative path. To get full path, use `#filePath`.

```swift
func testDivisionIsValid() {
    let divisor = 0
    verifyNotZero(divisor)
}

private func verifyNotZero(_ val: Int, file: StaticString = #file, line: UInt = #line) {
    XCTAssertNotEqual(val, 0, file: file, line: line)
}
```
