# Insets and Spacing

`NSCollectionLayoutSection` can apply `interGroupSpacing` and `contentInsets` to its groups and content respectively.

`NSCollectionLayoutGroup` has `interItemSpacing` of type `NSCollectionLayoutSpacing`. `.fixed(200.0)` means exactly 200 pts in-between items. `.flexible(200.0)` means min of 200 pts.

`NSCollectionLayoutItem` can apply `contentInsets` to its content. And `edgeSpacing` of type `NSCollectionLayoutEdgeSpacing` (which has `leading`, `top`, `trailing`, and `bottom` of type `NSCollectionLayoutSpacing`) to add spacings to edges. Edge spacing is applied before insets.
