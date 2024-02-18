# `font()`

Sets default font for text in view.

## Params

### `font`

Font (struct `Font`) to use when displaying this text.

## Return Value

`Text` with specified font.

## Discussion

Can apply font to specific text view or all text views in container.

```swift
VStack {
    Text("Font applied to a text view.")
        .font(.largeTitle)


    VStack {
        Text("These two text views have the same font")
        Text("applied to their parent view.")
    }
    .font(.system(size: 16, weight: .light, design: .default))
}
```
