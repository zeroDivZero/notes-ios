# `UICollectionViewCompositionalLayout`

```swift
class UICollectionViewCompositionalLayout: UICollectionViewLayout
```

Layout designed to be composable, flexible, and fast. Composed of `NSCollectionLayoutSection`s (distinct visual groupings). Each section is composed of `NSCollectionLayoutGroup`s of `NSCollectionLayoutItem`s. Group can lay out its items as horizontal row, vertical column, or custom arrangement.

![compositional layout](../../../../assets/compositional_layout.png)

```swift
func createBasicListLayout() -> UICollectionViewLayout {
    let itemSize = NSCollectionLayoutSize(
        widthDimension: .fractionalWidth(1.0),
        heightDimension: .fractionalHeight(1.0))
    let item = NSCollectionLayoutItem(layoutSize: itemSize)

    let groupSize = NSCollectionLayoutSize(
        widthDimension: .fractionalWidth(1.0),
        heightDimension: .absolute(44))
    let group = NSCollectionLayoutGroup.horizontal(
        layoutSize: groupSize,
        subitems: [item])

    let section = NSCollectionLayoutSection(group: group)

    let layout = UICollectionViewCompositionalLayout(section: section)
    return layout
}
```
