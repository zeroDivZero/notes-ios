# VIEW ORGANIZATION

If high-level view, like `body`, starts getting long, either create custom views, or if subview not complex enough to be own custom view, create member views to keep it short.

```swift
var body: some View {
    HStack {
        CardView() // custom view
        Spacer()
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
