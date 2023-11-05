# `@State`

Typically for property inside struct.

```swift
@State private var userName = ""
```

Effectively moves storage out of struct to SwiftUI-managed shared storage, so structs can be destroyed without losing state. Allows modifying values inside struct.

Should be used with simple struct types like `String`, `Int`, and arrays, and generally shouldn't be shared with other views. To share values across views, use `@ObservedObject` or `@EnvironmentObject` – ensuring views to be refreshed when data changes.

To re-enforce local nature of `@State` properties, Apple recommends marking them `private`.

Can be used to track reference types, but won't be notified when they change. Helpful for classes that don't conform to `ObservableObject`.

**Tip:** When getting error about something isn't mutable, use this for quick testing and work on proper state management later.
