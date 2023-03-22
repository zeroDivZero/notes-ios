# `struct HStack`

View that arranges subviews in horizontal line.

```swift
@frozen struct HStack<Content> where Content : View
```

## Example

```swift
HStack(alignment: .top, spacing: 10) {
    ForEach(1...5, id: \.self) {
        Text("Item \($0)")
    }
}
```

## Notes

Renders all subviews at once, whether on-screen. Good for small number of subviews or don't want delayed rendering behavior of `LazyHStack`.

To conform to `Layout`, like when need conditional layout with `AnyLayout`, use `HStackLayout`.
