# CUSTOM SETUP AND TEARDOWN

## Creation Helpers

To test system that requires setup, tempting to include asserts on assumptions (such as initialization state) in tests. Should refactor those to helper methods (*creation methods* to create objects are common) to keep tests focused and easy to read.

Even though can add any data to `XCTestCase` subclass, avoid adding unnecessary state. Make sure each test creates/destroys its data in `setUp()`/`tearDown()`.

## `addTeardownBlock()`

Add `addTeardownBlock()` if teardown code specific to that test but not to others.

```swift
addTeardownBlock {
    // one-off teardown code like closing file
}
```

Can add multiple blocks, executed in reverse order (last block added first to run). All teardown blocks guaranteed to execute before `tearDown()`. Executed regardless of test result. Executed even if `continueAfterFailure` is `false`.
