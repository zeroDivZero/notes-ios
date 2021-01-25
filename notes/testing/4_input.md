# INPUT

Test should, when given specific input, always expect same specific output, regardless of app state or order of tests. **I** and **R** in **FIRST** - isolated and repeatable.

Code under test must rely solely on provided input - via initializer or properties (dependency injection). If it accesses something not provided by test, such as via singleton, it's harder to test.

Avoid side effects, use immutable data and not functions to change mutable variables, and reduce app state.

Highly testable code makes writing unit tests trivial.

Can use debugger to step through test, but if need to do it constantly, may be smell that test isn't simple enough.
