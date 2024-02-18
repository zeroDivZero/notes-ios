# `padding()`

Adds equal padding to specific edges.

```swift
func padding(
    _ edges: Edge.Set = .all,
    _ length: CGFloat? = nil
) -> some View
```

* `edges`: Set of edges to pad. Default `.all`.
* `length`: Points to pad on specified edges. `nil` (default) for platform-specific default value.

There exist variants to pad each edge independently or only specify amount for all edges.
