# `clipShape()`

Sets clipping shape for this view.

## Params

### `shape`

Clipping shape (protocol `Shape`) to use. Fills view's frame while maintaining aspect ratio.

### `style`

Fill style (struct `FillStyle`) to use when rasterizing shape.

## Return Value

View that clips this view using specified shape and rasterization.

## Discussion

Preserves parts of view covered by shape while eliminating other parts. Clipping shape itself not visible.

```swift
// clip image to a circle
Image("my_impage")
    .clipShape(Circle())
```
