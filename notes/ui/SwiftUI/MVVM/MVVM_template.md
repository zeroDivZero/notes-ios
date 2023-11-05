# MVVM TEMPLATE

## Model

```swift
struct MyModel {
  // ...
}
```

Use `private(set)` to make fields read-only publicly. `mutating func` for functions that alter state.

## View Model

```swift
class MyViewModel: ObservableObject {
  @Published private var model = MyModel()

  // ...
}
```

View Model conforms to `ObservableObject` to notify when something (Model) changes.

By default `ObservableObject` synthesizes `objectWillChange` publisher that emits changed value before any of its `@Published` properties changes.

Make Model publisher with `@Published`.

## View

```swift
struct MyView: View {
    @ObservedObject var viewModel: MyViewModel

    var body: some View {
      // ...
    }

    // ...
}
```

Mark View Model as `@ObservedObject`, so when it changes, view is redrawn.

Observed object should always be passed in, never created by view. If view needs own state, declare with [`@State`](../Property%20Wrappers/State%20Management/@State.md) (value types like `String`, `Int`, etc.) or `@StateObject` (for reference types).

State should always have single source of truth, be it in parent view or at app root (`App` object).
