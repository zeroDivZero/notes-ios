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
