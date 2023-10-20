# `HStack`

View that arranges subviews in horizontal line.

```swift
@frozen struct HStack<Content> where Content : View
```

## Initializer

```swift
init(
    alignment: VerticalAlignment = .center,
    spacing: CGFloat? = nil,
    @ViewBuilder content: () -> Content
)
```

* `alignment`: To align subviews. `.center`, `.top`, `.bottom`, `.lastTextBaseline`, etc.
* `spacing`: Distance between adjacent subviews, `nil` to let stack choose default.

## Example

```swift
var body: some View {
    HStack(
        alignment: .top,
        spacing: 10
    ) {
        ForEach(
            1...5,
            id: \.self
        ) {
            Text("Item \($0)")
        }
    }
}
```

## Notes

Renders all subviews at once, whether on-screen. Good for small number of subviews or don't want delayed rendering behavior of `LazyHStack`.

To conform to `Layout`, like when need conditional layout with `AnyLayout`, use `HStackLayout`.
