# `ZStack`

View that overlays its subviews, aligning them in both axes. Assigns each successive subview higher z-axis value than one before -- later subviews appear "on top" of earlier ones.

```swift
@frozen struct ZStack<Content> where Content : View
```

## Initializer

```swift
init(
    alignment: Alignment = .center,
    @ViewBuilder content: () -> Content
)
```

* `alignment`: To align subviews on both x and y-axes.
![Alignment](/assets/alignment.png)

## Example

```swift
var body: some View {
    ZStack(alignment: .bottomLeading) {
        Rectangle()
            .fill(.red)
            .frame(width: 100, height: 50)
        Rectangle()
            .fill(.blue)
            .frame(width:50, height: 100)
    }
    .border(.green, width: 1)
}
```

## Notes

To conform to `Layout`, like when need conditional layout with `AnyLayout`, use `ZStackLayout`.
