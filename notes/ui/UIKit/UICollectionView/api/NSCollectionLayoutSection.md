# `NSCollectionLayoutSection`

```swift
class NSCollectionLayoutSection: NSObject
```

Container of set of `NSCollectionLayoutGroup`s. Collection view layout has one or more sections.

Can have its own background, header, and footer.

Ex:

```swift
let section = NSCollectionLayoutSection(group: group)
```

## Scrolling

Property `orthogonalScrollingBehavior` determines section's scrolling behavior relative to main layout axis. Default is same direction. Set it to `.continuous`, for example, to allow scrolling orthogonally to layout.
