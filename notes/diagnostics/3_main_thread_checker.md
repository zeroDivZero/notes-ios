# MAIN THREAD CHECKER

Standalone tool for Swift and C languages that detects invalid usage of AppKit, UIKit, and other APIs on background thread.

## How It Works

At app launch, Main Thread Checker dynamically replaces implementations of methods that should only be called on main thread with versions that prepend the check. Methods known to be safe for use on background threads are excluded from this check.

**Note:** Unlike other code diagnostic tools, Main Thread Checker doesn't require recompilation, and can be used with existing binaries. Can run it on macOS app without Xcode debugger, such as on CI system, by injecting dynamic library file located at `/Applications/Xcode.app/Contents/Developer/usr/lib/libMainThreadChecker.dylib`.

## Performance Impact

Minimal, with 1–2% CPU overhead and additional process launch time of <0.1 sec. Automatically enabled when running app with Xcode debugger.
