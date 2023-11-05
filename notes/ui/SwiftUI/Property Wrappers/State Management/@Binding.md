# `@Binding`

Creates 2-way connection between property that stores data, and view that displays and changes data. Connects property to source of truth stored elsewhere, instead of storing data directly.

## Example

Button toggling play/pause creates binding to parent view property:

```swift
struct PlayButton: View {
    @Binding var isPlaying: Bool

    var body: some View {
        Button(isPlaying ? "Pause" : "Play") {
            isPlaying.toggle()
        }
    }
}

struct PlayerView: View {
    var title: String
    @State private var isPlaying = false

    var body: some View {
        VStack {
            Text(title)
                .foregroundStyle(isPlaying ? .primary : .secondary)
            PlayButton(isPlaying: $isPlaying) // pass binding
        }
    }
}
```

## `@Bindable`

To create binding to property of type that conforms to `Observable`, use `Bindable` property wrapper.
