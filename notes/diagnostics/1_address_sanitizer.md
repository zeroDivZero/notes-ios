# ADDRESS SANITIZER (ASan)

LLVM-based tool for Swift and C languages that finds mem corruptions and other errors at runtime.

Mem issues are frequently cause of security vulnerabilities. Strongly encouraged to incorporate ASan as part of QA process.

## How It Works

ASan replaces `malloc` and `free` functions with custom implementations that allow regions surrounding requested mem checked for invalid access.

When `malloc` is called, it allocates requested amount of memory and marks surrounding regions as off-limits. When `free` is called, it marks region as off-limits and adds it to quarantine queue, which delays when that mem can be reused by `malloc`. All mem accesses in code are transformed by compiler:

```c
// pseudocode
// Before
*address = ...;  // or: ... = *address;
// After
if (IsMarkedAsOffLimits(address)) {
  ReportError(address);
}
*address = ...;  // or: ... = *address;
```

When code is run with ASan enabled, any access to off-limits mem region results in error.

## Performance Impact

Typically results in CPU slowdown of 2-5⨉, and mem usage increase of 2-3⨉. Can improve mem utilization by compiling at `-O1` optimization level.

For most cases, overhead should be acceptable for daily development — in fact, may not notice slowdown.

## Limitations

Can only detect mem errors during execution. Comprehensive unit tests still required.

Cannot detect leaks, access to uninitialized mem, or integer overflow. Can use ASan in addition to TSan, UBSan, and Instruments to find additional issues.
