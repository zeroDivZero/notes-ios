# UNDEFINED BEHAVIOR SANITIZER (UBSan)

LLVM tool for C languages (no Swift) that detects undefined behavior at runtime. Undefined behavior describes result of any operation with unspecified semantics, such as dividing by zero, loading mem from misaligned pointer, or dereferencing null pointer.

## How It Works

Uses Clang to emit checks into code during compilation. Nature of inserted code depends on kind of undefined behavior. E.g., Integer Overflow check adds code around arithmetic operators, including addition, subtraction, multiplication, and division.

```c
// Before
int32_t n = 42;
n += 17;

// After
int32_t n = 42;
if (SignedAdditionWillOverflow(n, 17)) {
    DiagnoseUndefinedBehavior();
}
n += 17;
```

## Performance Impact

Minimal, with average 20% CPU overhead in Debug config.
