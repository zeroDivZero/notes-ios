# ACCESSIBILITY ATTRIBUTE

Core to supporting accessibility. Supplies VoiceOver with info about element. An accessibility attribute has 5 properties:

1. **Label**: Concise text identifying control or view. E.g., "back button", "recipe image".
2. **Traits**: Describe element's state, behavior, or usage. E.g., button trait "is selected".
3. **Hint**: Describes action an element completes. E.g., "displays recipe detail".
4. **Frame**: Frame of element within screen, as `CGRect`. VoiceOver speaks content of `CGRect`.
5. **Value**: Value of element. E.g., with progress bar or slider, current value could be "5 out of 100".

Most UIKit components have preset attributes; supply details to improve UX. Need to supply most attributes for custom control.
