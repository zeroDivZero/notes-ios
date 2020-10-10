# `MetricKit`

Framework to aggregate and analyze per-device reports on exception and crash diagnostics of on-device app, and on power and performance metrics.

Does not return data to Mac apps built with **Catalyst**.

## Setup

Need always-in-memory object, like `AppDelegate`, to receive events. Register to `MXMetricManager` and conform to `MXMetricManagerSubscriber`.

```swift
func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplication.LaunchOptionsKey: Any]?) -> Bool {
    MXMetricManager.shared.add(self)
    return true
}

extension AppDelegate: MXMetricManagerSubscriber {
    func didReceive(_ payloads: [MXMetricPayload]) {
        // handle metric payloads
    }

    func didReceive(_ payloads: [MXDiagnosticPayload]) {
        // handle diagnostic payloads
    }
}
```

Each `didReceive(_:)` is called at most once a day.

## Handle Payloads

`MXMetricPayload` (and similarly `MXDiagnosticPayload`) encapsulates daily metrics report. Contains properties that encapsulate more specfic metrics, like `MXMemoryMetric` and `MXAppResponsivenessMetric`. Each `MXMetricPayload` may not have all properties set, need to iterate full array to get all metrics.

All metric classes have base class `MXMetric` (and similarly `MXDiagnostic`), which has `jsonRepresentation()` to easily pass metric as JSON.

Xcode can simulate metrics. Does not work on simulator, need physical device:

**Debug > Simulate MetricKit Payloads**

## Logging

To log specific section manually without relying on automated reporting:

```swift
let filterLog = MXMetricManager.makeLogHandle(category: "Picture Filter")

func applyFilter(named name: String) {
    mxSignpost(.begin, log: filterLog, name: "\(name) filter")
    // long-running operation
    // ...
    // end the data collection; can be inside completion handler
    mxSignpost(.end, log: filterLog, name: "\(name) filter")
}
```

## `MXDiagnostic`

Base class for reports on hangs, crashes, disk writes, and CPU exceptions. Derived class `MXCrashDiagnostic` even provides unsymbolicated stacktrace in `MXCallStackTree`.
