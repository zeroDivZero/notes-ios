# `ignoresSafeArea(_:edges:)`

Expands view out of safe area.

```swift
func ignoresSafeArea(
    _ regions: SafeAreaRegions = .all,
    edges: Edge.Set = .all
) -> some View
```

## Parameters

### `regions`

Kinds of rectangles removed from safe area that should be ignored (i.e. added back to safe area of new child view).

### `edges`

Edges of view that may be outset. Any edge not in this set will be unchanged, even if that edge is abutting safe area listed in `regions`.

## Return Value

New view with safe area expanded.

## Example

```swift
ZStack { ... }.ignoresSafeArea()
```
