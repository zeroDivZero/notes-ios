# `UICollectionView.CellRegistration`

```swift
struct CellRegistration<Cell, Item> where Cell: UICollectionViewCell
```

For registering specific type of cells and configuring each one.

```swift
// declaration
private var myCellRegistration: UICollectionView.CellRegistration<MyCell, MyCellModel>!

// somewhere when configuring collection view
myCellRegistration = UICollectionView.CellRegistration { cell, indexPath, model in
  cell.configure(model)
}

// data source returning cell
dataSource = UICollectionViewDiffableDataSource<Section, Int>(collectionView: collectionView) {
    (collectionView: UICollectionView, indexPath: IndexPath, itemIdentifier: Int) -> UICollectionViewCell? in
    collectionView.dequeueConfiguredReusableCell(
      using: cellRegistration,
      for: indexPath,
      item: itemIdentifier)
```

`cell`, `model` strongly typed, no need to cast. Decouples data source (which now only knows registration) and exact cell type.
