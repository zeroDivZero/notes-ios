# `NSCollectionLayoutSize`

```swift
class NSCollectionLayoutSize: NSObject
```

Width and height (pair of `NSCollectionLayoutDimension`s) of item in collection view. Every item has explicit size.

## `NSCollectionLayoutDimension`

```swift
class NSCollectionLayoutDimension: NSObject
```

Can be expressed using *absolute*, *estimated*, or *fractional* value.

### Absolute

44 x 44 point square:

```swift
let absoluteSize = NSCollectionLayoutSize(
    widthDimension: .absolute(44),
    heightDimension: .absolute(44))
```

### Estimated

If content size might change at runtime. System computes actual value later.

```swift
let estimatedSize = NSCollectionLayoutSize(
    widthDimension: .estimated(200),
    heightDimension: .estimated(100))
```

### Fractional

Relative to dimension of item's container. Ex: Following item has width and height both equal to 20% of its container's width, making it square that grows and shrinks as size of its container changes.

```swift
let fractionalSize = NSCollectionLayoutSize(
    widthDimension: .fractionalWidth(0.2),
    heightDimension: .fractionalWidth(0.2))
```
