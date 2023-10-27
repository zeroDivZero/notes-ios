# `Group`

Collects multiple instances of content type — like views, scenes, or commands — into single unit.

```swift
@frozen struct Group<Content>
```

Groups views without affecting layout. Easy way to apply same modifier to all members at once (but not to group itself):

```swift
Group {
    Text("SwiftUI")
    Text("Combine")
    Text("Swift System")
}
.font(.headline)
```

View group created with view builder. Can use group's initializer to produce different kinds of views from conditional:

```swift
Group {
    if isLoggedIn {
        WelcomeView()
    } else {
        LoginView()
    }
}
.navigationBarTitle("Start")
```

Group of views itself is view. Can compose group within other view builders, including nesting within other groups. Allows adding large numbers of views to different view builder containers:

```swift
var body: some View {
    VStack {
        Group {
            Text("1")
            Text("2")
            Text("3")
            Text("4")
        }
        Text("5")
    }
}
```

Can initialize groups with other types such as `Scene` and `ToolbarContent`.
