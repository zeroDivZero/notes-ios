# `Spacer`

Flexible space that expands along major axis of its containing stack layout, or on both axes if not contained in stack.

```swift
@frozen struct Spacer
```

Specify optional arg `minLength: CGFloat?` for minimum space, but typically left out to let system decide, responsive to screen size.


## Example

```swift
HStack {
    Image(systemName: "checkmark")
    Spacer()
    Text(name)
}
```
