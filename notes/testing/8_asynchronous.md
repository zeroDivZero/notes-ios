# ASYNCHRONOUS

Problem: test ends as soon as test func returns, not waiting for async operation.

Not fast and often not reliable. Even if reliable, not easy to run. Common practice to create new test bundle to group async tests, so to run as necessary, not affecting day-to-day.

## Expectation

```swift
let expectation = expectation(description: "Long Op")
var results: [Result]?

obj.longOperation(param) {
    results = $0
    expectation.fulfill()
}

waitForExpectations(timeout: 5.0)  // wait until all expectations fulfilled, or timeout (always fail)
XCTAssertEqual(results?.count, 10)
```

Description used to create expectation is displayed in test log to help diagnose failure. Can pass optional handler to `waitForExpectations()`, called when expectations fulfilled or timed out. Alternatively, use `wait(for:timeout:)`.

### Inverted Expectation

Expectation can also verify when something didn't happen. Set property `isInverted` to `true`.

Example: Class `Debouncer` delays closure and cancels previous one (say, for search-as-user-types UI).

```swift
class DebouncerTests: XCTestCase {
    func testPreviousClosureCanceled() {
        let debouncer = Debouncer(delay: 0.25)

        // expectation for closure that should be canceled
        let cancelExpectation = expectation(description: "Cancel")
        cancelExpectation.isInverted = true

        // expectation for closure that should be completed
        let completedExpectation = expectation(description: "Completed")

        debouncer.schedule {
            cancelExpectation.fulfill()
        }

        // when scheduling new closure, previous one should be canceled
        debouncer.schedule {
            completedExpectation.fulfill()
        }

        // add 0.05 seconds to reduce flakiness
        waitForExpectations(timeout: 0.3)
    }
    // no assertion needed; test fails if expectations not met
}
```

## Dispatch Queue

Sometimes no completion handler or callback to hook into, such as "fire and forget" preload content function. Can enable `DispatchQueue` from outside and use `sync()` to issue synchronous closure on said queue, so it waits for operation to finish.

```swift
classFileLoaderTests: XCTestCase {
    func testPreloadingFiles() {
        let loader = FileLoader()
        let queue = DispatchQueue(label: "FileLoaderTests")

        loader.preloadFiles(named: ["One", "Two", "Three"], on: queue)

        // issue empty closure on queue and wait for it to be executed
        queue.sync {}

        let preloadedFileNames = loader.preloadedFiles.map { $0.name }
        XCTAssertEqual(preloadedFileNames, ["One", "Two", "Three"])
    }
}
```

## Turn Synchronous

Use mock. For example, `UNUserNotificationCenter`'s `requestAuthorization()` is async method to request permission for push notifications. Class interacting with it has to be async too. Use mock to turn it sync:

```swift
// abstraction
protocol UserNotificationCenter {
    func requestAuthorization(options: UNAuthorizationOptions,
                              completionHandler: @escaping (Bool, Error?) -> Void)
}

// protocol requirements exactly match UNUserNotificationCenter's API, can conform easily
extension UNUserNotificationCenter: UserNotificationCenter {}

// mock
classUserNotificationCenterMock: UserNotificationCenter {
    var grantAuthorization = false
    var error: Error?

    func requestAuthorization(options: UNAuthorizationOptions,
                              completionHandler: @escaping (Bool, Error?) -> Void) {
        // execute completion handler synchronously
        completionHandler(grantAuthorization, error)
    }
}

// test
classPushNotificationManagerTests: XCTestCase {
    func testSuccessfulAuthorization() {
        let center = UserNotificationCenterMock()
        let manager = PushNotificationManager(notificationCenter: center)

        center.grantAuthorization = true

        var status: PushNotificationManager.Status?
        manager.enableNotifications { status = $0 }

        XCTAssertEqual(status, .enabled)
    }
}
```
