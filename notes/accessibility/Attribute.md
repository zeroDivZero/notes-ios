# ACCESSIBILITY ATTRIBUTE

Core to supporting a11y. Supplies VoiceOver with info about element. An a11y attribute has 5 properties:

1. **Label**: Text identifying element. E.g., "back button", "recipe image".
2. **Traits**: Describe element's state, behavior, or usage. E.g., button trait "is selected".
3. **Hint**: Describes action an element completes. E.g., "displays recipe detail".
4. **Frame**: Frame of element within screen, as `CGRect`. VoiceOver speaks content of `CGRect`.
5. **Value**: Value of element. E.g., with progress bar or slider, current value could be "5 out of 100".

Most UIKit components have preset attributes; supply details to improve UX. Need to supply most attributes for custom control.

## Implementation

In Storyboard, can see some a11y attribute properties in identity inspector of element. Can also be set in code.

```swift
imageView.isAccessibilityElement = true
imageView.accessibilityLabel = "Creamy cupcake with chocolate frosting and sprinkles on top."
imageView.accessibilityTraits = .image

label.accessibilityLabel = "Difficulty Level"
label.accessibilityValue = "\(value)"

// to support Dynamic Text
label.font = .preferredFont(forTextStyle: .body)
label.adjustsFontForContentSizeCategory = true  // not really needed if font is preferredFont
```

**In general, aim to explain meaning of state of control, rather than how it looks.**
