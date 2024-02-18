# `frame()`

Positions view within invisible frame of fixed size.

```swift
func frame(
    width: CGFloat? = nil,
    height: CGFloat? = nil,
    alignment: Alignment = .center
) -> some View
```

If only specified one dimension, resulting view assumes this view's sizing behavior in other dimension.
