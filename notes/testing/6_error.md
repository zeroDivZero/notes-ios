# ERROR

When testing throwing function, should test both success path and error path. 3 ways: catch error, assert on throw, and test itself throws.

## Catch Error

```swift
func testPlayingBioBlitzThrows() {
    let game = Game(name: "BioBlitz")

    do {
        try game.play()
        XCTFail("BioBlitz has not been purchased.")
    } catch GameError.notPurchased {
        // success
    } catch {
        XCTFail("Did not throw GameError.notPurchased.")
    }
}
```

`game.play()` is expected to throw, so if it doesn't, or if it throws wrong error, `XCTfail()` fails test.

## Assert on Throw

**XCTest** provides `XCTAssertThrowsError()` and `XCTAssertNoThrow()` to check if expression throws.

```swift
func testPlayingBlastazapThrows() {
    let game = Game(name: "Blastazap")
    XCTAssertThrowsError(try game.play()) { error in
        XCTAssertEqual(error as? GameError, GameError.notInstalled)
    }
}
```

Add trailing closure to handle error.

```swift
func testPlayingExplodingMonkeysDoesntThrow() {
    let game = Game(name: "Exploding Monkeys")
    XCTAssertNoThrow(try game.play())
}
```

## Throwing Test

Test that throws is considered failure.

```swift
func testCrashyPlaneDoesntThrow() throws {
    let game = Game(name: "CrashyPlane")
    try game.play()
}
```

If test throws, output not useful unless error conforms to `LocalizedError` and `errorDescription` is provided. Simple common implementation:

```swift
extension LocalizedError {
    var errorDescription: String? { "\(self)" }
}
```
