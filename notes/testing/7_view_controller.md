# VIEW CONTROLLER

If VC simple and inert - only connects model to view, handle view lifecycle events (`viewDidLoad()`, `viewWillAppear()`, etc.), and maybe stores outlets - hardly need unit tests.

## Pipe

Connecting model to view, like pipe. No knowledge encapsulated. Push as much logic into model layer as possible.

## Lifecycle

If doing configuration in `viewDidLoad()` (e.g., hiding components based on state), need to test. Can create VC, make sure `view` is created, then call function directly:

```swift
let sut = ViewController()
sut.loadViewIfNeeded()
sut.viewWillAppear(false)
```

## Navigation

Does ViewControllerA show ViewControllerB when button tapped? Use coordinator pattern to test without ViewControllerB.

## Outlet

Easy smoke test, ensuring outlet not accidentally disconnected. Load view and:

```swift
XCTAssertNotNil(sut.submitButton)
```

## Advice

Adding `import UIKit` to file makes it harder to test. May prefer UI tests. Always better to move logic into smaller, pure data models.
