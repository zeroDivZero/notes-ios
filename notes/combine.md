# COMBINE

Framework implementing functional reactive programming (FRP) paradigm. Heavily used by SwiftUI.

## FRP

Data flows from one place to other automatically through subscriptions.

Particularly useful when data changes over time.

E.g., use FRP to push value of slider to stream, or use publisher to send value to subscribers, which could be label showing slider value, or something else.

In addition to driving UI updates, also useful in asynchronous programming. E.g., when making network request, get result back eventually. Instead of executing completion closure, request method would return publisher, which publishes result when request done. If result needs to be transformed, or need to chain with another request, easier to read code than nested tree of completion closures.

## Publisher and Subscriber

Publisher object sends values to subscribers over time. Could be single, multiple, or no values. Can only emit single completion or error event. Publisher flow commonly represented by _marble diagram_:

![publisher flow marble diagram](../assets/combine_publisher.png)

Each arrow is publisher. Marble is value emitted. Top arrow has line at end representing completion event. Bottom arrow has cross representing error event. After either event, no more value.

### Code Example

Can model value stream with array.

```swift
[1, 2, 3]
  .publisher
  .sink(receiveCompletion: { completion in
    switch completion {
    case .failure(let error):
      print("Something went wrong: \(error)")
    case .finished:
      print("Received Completion")
    }
  }, receiveValue: { value in
    print("Received value \(value)")
  })
```

Combine adds `publisher` property to `Array`. Turns array of values into publisher to publish values to subscribers.

Created publisher type is `Publishers.Sequence<[Int], Never>`. `Publishers` is enum used as namespace for all publishers. Each publisher conforms to `Publisher`.

subscribe to a publisher using the sink(receiveCompletion:receiveValue:) method. 

