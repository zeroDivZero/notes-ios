# MVVM

**Model-View-ViewModel**. Design pattern SwiftUI adopts to separate UI from model.

**Model** is data and logic of app. Can be structs, database (SQL), ML model and code, etc. **View** (UI) is visual presentation of model, is stateless, and allows user to interact with model.

## Connecting Model and UI

3 options:

1. [`@State`](../Property%20Wrappers/State%20Management/@State.md) or `@StateObject` in `View`. Minimal separation.
2. Model only accessible via gatekeeper entity **View Model**. Full separation.
3. View Model exists, but Model can be directly accessed. Partial separation.

Choice depends on Model complexity. Typically option 2 (particularly if Model is SQL, don't want queries directly in View). Allows app to grow and stay maintainable.

Extremely simple Model (no logic) can opt for option 1. Something in-between can use option 3 (tweak on MVVM).

## Update Flow

User interaction sends intent to View Model, which translates to commands to update Model. When Model changes (either by View Model or other signal), SwiftUI automatically updates UI:

![MVVM Model to UI](/assets/swiftui-mvvm.png)
