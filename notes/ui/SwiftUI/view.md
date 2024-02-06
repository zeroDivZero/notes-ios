# VIEW

By default, SwiftUI view file declares structure and preview. Structure conforms to `View` protocol and describes view's content and layout. Preview declaration creates preview for that view.

Auto-generated code in `ContentView.swift`:

```swift
import SwiftUI

struct ContentView: View {
    var body: some View {
        VStack {
            Image(systemName: "globe")
                .imageScale(.large)
                .foregroundStyle(.tint)
            Text("Hello, world!")
        }
        .padding()
    }
}

#Preview {
    ContentView()
}
```
