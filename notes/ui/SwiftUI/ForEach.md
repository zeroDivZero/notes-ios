# `struct ForEach`

Computes views from collection of identified data.

## Declaration

```swift
struct ForEach<Data, ID, Content> where Data : RandomAccessCollection, ID : Hashable
```

## Overview

Use `ForEach` to provide views based on `RandomAccessCollection` of some data type. Either the collection's elements must conform to `Identifiable`, or provide `id` param to `ForEach` initializer.

```swift
HStack {
    let contents = ["👻", "🎃", "🕷️", "😈"]
    ForEach(contents.indices, id: \.self) {
        CardView(content: contents[$0])
    }
}
```
