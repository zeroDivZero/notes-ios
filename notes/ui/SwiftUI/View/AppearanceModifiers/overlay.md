# `overlay()`

Layers specified views in front of this view. To place one or more views in front of another view.

```swift
Image("my_image")
    .clipShape(Circle())
    .overlay {
        Circle().stroke(.white, lineWidth: 4)
    }
```
