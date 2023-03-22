# VIEW ORGANIZATION

If high-level view, like `body`, starts getting long, create new member views to keep it short.

```swift
var body: some View {
    HStack {
        remove
        Spacer()
        add
    }
    .padding(.horizontal)
}

var remove: some View {
    Button(action: {
        count -= 1
    }) {
        VStack {
            Text("Remove")
            Text("Item")
        }
    }
}

var add: some View {
    Button(action: {
        count += 1
    }) {
        VStack {
            Text("Add")
            Text("Item")
        }
    }
}
```
