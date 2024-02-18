# `foregroundStyle()`

Sets text style (such as color) displayed by this view.

## Params

### `style`

Style (Protocol `ShapeStyle`) to use when displaying this text.

## Return Value

`Text` with specified style.

## Discussion

E.g.:

```swift
HStack {
    Text("Red").foregroundStyle(.red)
    Text("Green").foregroundStyle(.green)
    Text("Blue").foregroundStyle(.blue)
}
```
