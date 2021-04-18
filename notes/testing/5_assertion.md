# ASSERTION

Tests should be sensitive to important things and ignore others. If it's not important, can allow bit of float.

E.g., for user name instead of hardcoded strings like "John Smith", use random string:

```swift
let user = User(name: UUID().uuidString)
```

May uncover hidden assumptions. Similarly for other fields:

```swift
func randomAge() -> Int {
    Int.random(in: 0...120)
}
```

If order of elements in array doesn't matter, don't test it. Use `Set`, or:

```swift
extension Array where Element: Comparable {
    func fuzzyMatches(other: Array) -> Bool {
        sorted() == other.sorted()
    }
}
```

If element only conforms to `Equatable`, need to loop over one array removing all elements of another:

```swift
extension Array where Element: Equatable {
    func fuzzyMatches(other: Array) -> Bool {
        guard self.count == other.count else {
            return false
        }

        var selfCopy = self
        for item in other {
            if let index = selfCopy.firstIndex(of: item) {
                selfCopy.remove(at: index)
            } else {
                return false
            }
        }

        return true
    }
}
```

## Verification Method

If need to write multiple similar tests, each with multiple similar asserts, can write verification method to group asserts for convenience.

```swift
func verifyDivision(_ result: (quotient: Int, remainder: Int),
                    expectedQuotient: Int,
                    expectedRemainder: Int,
                    file: StaticString = #file,
                    line: UInt = #line) {
    XCTAssertEqual(result.quotient, expectedQuotient,
                   file: file, line: line)
    XCTAssertEqual(result.remainder, expectedRemainder,
                   file: file, line: line)
}
```

Pass `file` and `line` so if test fails, failure is shown at `verifyDivision()` callsite and not inside it.
