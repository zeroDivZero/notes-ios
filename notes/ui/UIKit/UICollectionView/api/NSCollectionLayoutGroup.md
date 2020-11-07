# `NSCollectionLayoutGroup`

```swift
class NSCollectionLayoutGroup: NSCollectionLayoutItem
```

Container of set of items. Determines how items are laid out relative to each other: horizontal row, vertical column, or custom arrangement. Itself does not render any content.

Specifies own size as width and height dimensions, similar to item.

Subclass of `NSCollectionLayoutItem`, so can be nested.

![compositional layout](../../../../assets/nested_groups.png)

Ex:

```swift
let groupSize = NSCollectionLayoutSize(
    widthDimension: .fractionalWidth(1.0),
    heightDimension: .absolute(44))
let group = NSCollectionLayoutGroup.horizontal(
    layoutSize: groupSize,
    subitems: [item])
```

After configuring group, must initialize `NSCollectionLayoutSection` with that group.
