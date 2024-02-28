# PREVIEW

See preview in dark or light mode.

```swift
struct ContentView_Previews: PreviewProvider {
    static var previews: some View {
        ContentView()
            .preferredColorScheme(.dark)
        ContentView()
            .preferredColorScheme(.light)
    }
}
```

## Named Preview

```swift
#Preview("Blue") {
    MyView(color: .blue)
}

#Preview("Red") {
    MyView(color: .red)
}
```

## Group

```swift
#Preview {
    Group {
        MyView(color: .blue)
        MyView(color: .red)
        MyView(color: .green)
    }
}
```
