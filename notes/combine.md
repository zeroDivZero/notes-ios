# COMBINE

Framework implementing functional reactive programming (FRP) paradigm. Heavily used by SwiftUI.

## FRP

Data flows from one place to other automatically through subscriptions.

Particularly useful when data changes over time.

E.g., use FRP to push value of slider to stream, or use publisher to send value to subscribers, which could be label showing slider value, or something else.

In addition to driving UI updates, also useful in asynchronous programming. E.g., when making network request, get result back eventually. Instead of executing completion closure, request method would return publisher, which publishes result when request done. If result needs to be transformed, or need to chain with another request, easier to read code than nested tree of completion closures.

## Publisher and Subscriber

Publisher object sends values to subscribers over time. Could be single, multiple, or no values. Can only emit single completion or error event. Publisher flow commonly represented by _marble diagram_:

![publisher flow marble diagram](../../assets/combine_publisher.png)
