# Section Header

```swift
let headerSize = NSCollectionLayoutSize(widthDimension: .fractionalWidth(1.0), heightDimension: .estimated(44))
let headerElement = NSCollectionLayoutBoundarySupplementaryItem(layoutSize: headerSize, elementKind: "header", alignment: .top)
section.boundarySupplementaryItems = [headerElement]
```

Arg `alignment` (`NSRectAlignment`) determines if it's header, footer, or decorative view. `elementKind` is string identifier.
