# CUSTOM SETUP AND TEARDOWN

To test system that requires some setup, tempting to include asserts on assumptions (such as initialization state) in tests. Should refactor those to helper methods (*creation methods* to create objects are common) to keep tests focused and easy to read.

Even though can add any data to `XCTestCase` subclass, avoid adding unnecessary state. Make sure each test creates/destroys its data in `setUp()`/`tearDown()`.
