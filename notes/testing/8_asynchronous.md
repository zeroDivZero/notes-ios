# ASYNCHRONOUS

Problem: test ends as soon as test func returns, not waiting for async operation.

Not fast and often not reliable. Even if reliable, not easy to run. Common to create new test bundle to group async tests, so to run as necessary, not affecting day-to-day.

## Expectation

Fulfill instance of `XCTestExpectation` asynchronously when condition met (or time out) to complete test. See [8a_expectation](./8a_expectation.md).

## Dispatch Queue

Sometimes no completion handler or callback to hook into, such as "fire and forget" preload content function. Can enable `DispatchQueue` from outside and use `sync()` to issue synchronous closure on said queue, so it waits for operation to finish.

```swift
class FileLoaderTests: XCTestCase {
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
class UserNotificationCenterMock: UserNotificationCenter {
    var grantAuthorization = false
    var error: Error?

    func requestAuthorization(options: UNAuthorizationOptions,
                              completionHandler: @escaping (Bool, Error?) -> Void) {
        // execute completion handler synchronously
        completionHandler(grantAuthorization, error)
    }
}

// test
class PushNotificationManagerTests: XCTestCase {
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
