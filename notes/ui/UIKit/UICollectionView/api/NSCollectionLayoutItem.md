# `NSCollectionLayoutItem`

```swift
class NSCollectionLayoutItem: NSObject
```

Most basic component of collection view's layout. Responsible for size, space, and rendering of single view on screen. Typically a cell, but can be supplementary view like header, footer, and other decoration.

Specifies size as width and height dimensions. See `NSCollectionLayoutDimension`.

Combine items into groups that determine how those items are arranged in relation to each other. See `NSCollectionLayoutGroup`.

Ex:

```swift
let itemSize = NSCollectionLayoutSize(
    widthDimension: .fractionalWidth(0.6),
    heightDimension: .fractionalHeight(0.4))
let item = NSCollectionLayoutItem(layoutSize: itemSize)
```
