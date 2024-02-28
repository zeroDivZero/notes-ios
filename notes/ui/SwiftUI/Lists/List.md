# `List`

Container presenting rows of data in single column, optionally allowing selecting one or more members.

Static content:

```swift
var body: some View {
    List {
        Text("A List Item")
        Text("A Second List Item")
        Text("A Third List Item")
    }
}
```

Dynamic:

```swift
struct Ocean: Identifiable {
    let name: String
    let id = UUID()
}

private var oceans = [
    Ocean(name: "Pacific"),
    Ocean(name: "Atlantic"),
    Ocean(name: "Indian"),
    Ocean(name: "Southern"),
    Ocean(name: "Arctic")
]

var body: some View {
    List(oceans) {
        Text($0.name)
    }
}
```

## ID Keypath

If data not conformed to `Identifiable`, need to specify keypath to ID that uniquely identifies instance.

```swift
List(collection, id: \.id) {
    ListRow(element: $0)
}
```

## Navigation to Detail View

Add navigation by embedding list in `NavigationSplitView` and nesting each row in `NavigationLink` to set up transition to destination view.

```swift
NavigationSplitView {
    List(items) { item in
        NavigationLink {
            ItemDetail(item: item)  // view to navigate to when row selected
        } label: {
            ItemRow(item: item)  // row view
        }
    }
    .navigationTitle("Items")
} detail: {
    Text("Select an Item")  // default view when nothing selected (iPad)
}
```
