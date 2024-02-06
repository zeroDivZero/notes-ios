# ENTRY POINT

SwiftUI app life cycle has structure conforming to `App` protocol. Its `body` property returns one or more `Scene`s, which in turn provide content for display. `@main` attribute identifies app's entry point.

Auto-generated code in `MyApp.swift`:

```swift
import SwiftUI

@main
struct MyApp: App {
    var body: some Scene {
        WindowGroup {
            ContentView()
        }
    }
}
```
