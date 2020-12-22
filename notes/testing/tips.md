# TIPS

## `sut`

Often see variable declared as `sut`, which stands for *system under test*, that refers to subject to test.

```swift
let sut = MyClass()
sut.doSomething()
XCTAssertTrue(sut.doneSomething)
```

## `continueAfterFailure`

`XCTestCase` property to indicate test method should continue after failure occurs. Default `true`. May want to set to `false` in `setUp()` (typically for UI tests) if after failure state no longer valid, to avoid *assertion roulette*.

```swift
continueAfterFailure = false
```
