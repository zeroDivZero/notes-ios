# THREAD SANITIZER (TSan)

LLVM-based tool for Swift and C languages to detect data races at runtime. Data races occur when multiple threads access same mem without synchronization and at least one access is write. Data races are dangerous because they can cause programs to behave unpredictably, or even result in mem corruption.

Also detects other threading bugs, including uninitialized mutexes and thread leaks.

**Important:** Supported only for 64-bit macOS, iOS, and tvOS simulators (not watchOS). Cannot be used on device.

## How It Works

Records info about each mem access, and checks if that access participates in race. All mem accesses in code is transformed by compiler:

```c
// pseudocode
// Before
*address = ...;  // or: ... = *address;
// After
RecordAndCheckWrite(address);
*address = ...;  // or: ... = *address;
```

Each thread stores own timestamp and timestamps for other threads to establish points of synchronization. Timestamps are incremented each time mem accessed. By checking for consistency of mem access across threads, data races can be detected independent of actual timing of access. Therefore, TSan can detect races even if not manifested during particular run.

## Performance Impact

Can result in CPU slowdown of 2-20⨉, and mem usage increase of 5-10⨉. Improve mem utilization and CPU overhead by compiling at `-O1` optimization level.
