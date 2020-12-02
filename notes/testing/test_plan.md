# TEST PLAN

Xcode feature. Way to run test set with particular config. JSON file with `.xctestplan` extension, added to project and referenced from scheme. 3 main elements:

1. **Test targets:** One or more test targets (unit or UI). For each target, select tests (not always all) plan will run and if tests can run in parallel.

2. **Shared settings:** Set of default options, can be overridden by specific config. Settings typically found in scheme editor: launch args, l10n settings, screenshot settings, execution order (alphabetic or random), runtime sanitizers, thread checker, and malloc guards.

3. **Configs:** One or more configs to override shared settings. Test plan runs selected tests multiple times, once per config.

## Convert Scheme to Use Test Plan

If creating new test plan (blank or from scheme), recommended first to create folder (**New Group** in proj nav) to hold test plans. Following step adds test plan ref to proj root automatically, regardless of test plan file location; easier to move if folder already created.

Once: From scheme editor, select **Test** and click **Convert to use Test Plans**. Or **Product** > **Scheme** > **Convert Scheme to use Test Plans**. Then create test plan blank or from scheme, or choose existing.

When done, check scheme **Test** again and should see it using test plan.

## Create New Test Plan from Scratch

**Product** > **Test Plan** > **New Test Plan**. Use scheme editor to add new plan to scheme.

## Configure Test Plans

Use scheme editor to add/remove test plans and set default (run tests with **cmd+U**).

Click on each plan to see **Tests** and **Configurations** tabs.

### Tests

Add/remove test targets, tests, and change options (such as running tests in parallel).

### Confiugrations

Change **Shared Settings** (args, l10n, code coverage, sanitization, mem management, etc.). Add/remove configs (renamable) to change shared settings. Tests will be run for each config.

If test target not added to plan cannot run tests manually in source code editor. Can add target but disable tests.

## Run Tests

If test plan has 1+ configs and running tests manually, can option-click test to choose single config.

## Command Line

List all test plans in scheme:

```bash
xcodebuild -scheme ToDo -showTestPlans
Test plans associated with the scheme "ToDo":
        UnitTests
        FullTests
        PerfTests
```

To run default test plan on iPhone 8 (iOS 13.4.1) simulator:

```bash
xcodebuild test -scheme ToDo -destination 'platform=iOS Simulator,OS=13.4.1,name=iPhone 8'
```

To run different test plan:

```bash
xcodebuild test -scheme ToDo -destination 'platform=iOS Simulator,OS=13.3,name=iPhone 8' -testPlan PerfTests
```

## Benefits

* **Run tests with different sanitizers/diagnostics:** Can't test with both address and thread sanitizers enabled simultaneously. With test plan, can create 2 configs, one with address sanitizer enabled and another with thread sanitizer. Running test plan then runs tests twice, once for each config. Can easily add another config to run with malloc diagnostics.

* **Test multiple localizations:** Create config for each supported language. Set app language and region as part of config. Good way to generate screenshots for localizers.

* **Run selected tests with specific config:** E.g., perf tests usually should not run in parallel.

* **Different test scopes:** Can run default quick test set with 1 config and **cmd-U**. Then full set of unit, UI, and perf tests running against several configs.

Each scheme can have 1+ test plans; easier to manage than schemes.
