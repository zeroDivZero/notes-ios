# EXPECTATION

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

## `isInverted`

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

## `expectedFulfillmentCount`

Requires fulfilling expectation specified number of times (default 1) to be considered complete.

```swift
func testPrimesUpTo100() {
    let max = 100
    let primes = [2, 3, 5, 7, 11, 13, 17, 19, 23, 29, 31, 37, 41,
                  43, 47, 53, 59, 61, 67, 71, 73, 79, 83, 89, 97]
    var primeCounter = 0

    let expectation = XCTestExpectation(description: "calculate primes up to \(max)")
    expectation.expectedFulfillmentCount = 25

    // returns each prime in order up to `max` in completion handler
    PrimeCalculator.calculateStreaming(upTo: max) { prime in
        XCTAssertEqual(primes[primeCounter], prime)
        expectation.fulfill()
        primeCounter += 1
    }

    wait(for: [expectation], timeout: 3)
}
```

Ignored if `isInverted` set.

## `assertForOverFulfill`

Test exits if expectation fulfilled more than `expectedFulfillmentCount` times.

## `XCTNSPredicateExpectation`

Subclass of `XCTestExpectation`, fulfilled with `NSPredicate`. To test async code using `Progress` API.

```swift
func testPrimesUpTo100WithProgress() {
    let max = 100

    let progress = PrimeCalculator.calculateWithProgress(upTo: max) {
        XCTAssertEqual($0.count, 25)
    }

    let predicate = NSPredicate(
        format: "%@.completedUnitCount == %@",
        argumentArray: [progress, max]
    )
    let expectation = XCTNSPredicateExpectation(predicate: predicate, object: progress)

    wait(for: [expectation], timeout: 10)
}
```

## `XCTNSNotificationExpectation`

Fulfilled when expected `Notification` received.

```swift
func testUserUpgradedPostsNotification() {
    let user = User()
    let expectation = XCTNSNotificationExpectation(
        name: User.upgradedNotification
    )

    user.upgrade()

    wait(for: [expectation], timeout: 3)
}
```

Can add optional `handler` for more detailed expectation eval, returns `true` if expectation matches.

```swift
expectation.handler = { notification -> Bool in
    guard let level = notification.userInfo?["level"] as? String else {
        return false
    }

    return level == "gold"
}
```

Since anyone can post notification, to keep test independent, use dependency injection to let test create own `NotificationCenter` to be used by test subject (which can still have `NotificationCenter.default` as default to keep API simple).

```swift
let center = NotificationCenter()
let user = User()
let expectation = XCTNSNotificationExpectation(
    name: User.upgradedNotification,
    object: nil,
    notificationCenter: center
)

// ...

user.upgrade(using: center)
```
