## 1.1.0 (2026-04-13)

### 🚀 Features

- Metro bundler watch mode is now automatically disabled when running in a CI environment. ([#73](https://github.com/callstackincubator/react-native-harness/pull/73))
- Startup crash detection now monitors apps during launch and reports crashes before the first test even begins, with detailed diagnostics for both iOS and Android. On iOS, Harness prefers Apple diagnostic crash reports (including simulator `.ips` reports under DiagnosticReports) and device-side diagnostics from `devicectl` where available. Crash report selection on iOS simulators uses a more reliable algorithm that tolerates timing variations. ([#71](https://github.com/callstackincubator/react-native-harness/pull/71))
- Replaces the split Android/iOS/Web actions with a single composite action at the repository root (`callstackincubator/react-native-harness`). The action selects setup from your `rn-harness.config.mjs` runner, restores and saves `.harness/metro-cache` automatically, supports optional `preRunHook` and `afterRunHook` scripts, uploads crash artifacts from `.harness/crash-reports/`, and exposes Android AVD snapshot caching via `cacheAvd`. Older per-platform action entrypoints are deprecated in favor of the unified workflow. ([](https://github.com/callstackincubator/react-native-harness/commit/))
- Introduces a first-class plugin system: define hooks with `definePlugin()` from `@react-native-harness/plugins` and register them under `plugins` in `rn-harness.config.mjs`. Plugins can observe Harness, Metro, run, app, suite, and test lifecycle events for logging, artifacts, or custom automation. ([](https://github.com/callstackincubator/react-native-harness/commit/))

### 🩹 Fixes

- Metro cache is now stored under `.harness/metro-cache` in the project root. Set `unstable__enableMetroCache: true` in your config to use it; Harness will log when reusing the cache between runs. In CI, you can cache `.harness/metro-cache` to speed up Metro bundling. ([#74](https://github.com/callstackincubator/react-native-harness/pull/74))
- Harness now restores app startup stall recovery for RN-ready launches, including restart-between-files. Apps are retried when startup stalls without a crash, while confirmed native crashes still fail immediately with crash diagnostics. ([#78](https://github.com/callstackincubator/react-native-harness/pull/78))
- Harness now falls back to the next available Metro port when the configured port is already in use, which lets multiple Harness runs start at the same time without colliding on Metro. When this happens, Harness keeps the selected port consistent for the whole run and prints a message showing which port it ended up using. ([#96](https://github.com/callstackincubator/react-native-harness/pull/96))
- Mobile runners now fully disable native crash monitoring when `detectNativeCrashes` is set to `false`, including iOS simulators and Android emulators and physical devices. This keeps crash-monitor setup aligned with the runtime setting while preserving the existing default behavior of enabling native crash detection when the option is omitted. ([#94](https://github.com/callstackincubator/react-native-harness/pull/94))
- Physical iOS app launches now pass Harness launch arguments to `xcrun devicectl` without breaking JSON output collection. This prevents app launch arguments from being misinterpreted as `devicectl` flags and keeps device launches working when custom arguments are provided. ([#93](https://github.com/callstackincubator/react-native-harness/pull/93))
- Harness now queues concurrent runs before starting Metro when they target the same locked resource, such as the same simulator, device, or browser. Queueing is keyed by the platform resource lock rather than the configured Metro port, so runs using different ports still wait if they target the same resource. ([#91](https://github.com/callstackincubator/react-native-harness/pull/91))
- Improves Expo app startup and compatibility: Metro resolves package-style entry points before Harness rewrites, recognizes Expo’s virtual Metro entry during readiness checks, and aligns runtime bridge initialization with Expo’s Metro runtime and the React Compiler. ([](https://github.com/callstackincubator/react-native-harness/commit/))
- Adds `metroPort` to Harness config and `--metroPort` on the CLI so you can steer Metro and the in-process bridge together. The legacy `webSocketPort` option is ignored; bridge traffic uses the Metro port. When a run ends, Harness clears Android debug HTTP host and iOS simulator JS location overrides so the next normal dev-client or Metro launch is not left pointing at Harness. Includes a URL polyfill path used by the WebSocket bridge where the host runtime does not provide `URL` globally. ([](https://github.com/callstackincubator/react-native-harness/commit/))
- Refreshes the in-app Harness runner screen visuals and builds the test overlay against React Native 0.85+ APIs so the runtime UI stays compatible with current React Native releases. ([](https://github.com/callstackincubator/react-native-harness/commit/))
- Installs Android SDK and emulator-related tooling only when an Android flow actually needs it, so Apple-only or web-only workflows avoid unnecessary Android package setup. ([](https://github.com/callstackincubator/react-native-harness/commit/))
- Refreshes shared target resource locks atomically when renewing heartbeats, improving reliability when multiple Harness processes queue on the same simulator, device, or browser configuration. ([](https://github.com/callstackincubator/react-native-harness/commit/))

### ❤️ Thank You

- Hanno J. Gödecke
- Szymon Chmal @V3RON

# 1.0.0 (2026-03-11)

### 🩹 Fixes

- Add a new host option to rn-harness.config for Metro bind host, replacing HARNESS_METRO_BIND_HOST. ([#70](https://github.com/callstackincubator/react-native-harness/pull/70))
- Rewrites the implementation of the entry point resolver so it no longer mistakenly hijacks relative imports that originate from third-party packages instead of the root directory. ([#68](https://github.com/callstackincubator/react-native-harness/pull/68))

### ❤️ Thank You

- Hanno J. Gödecke
- Szymon Chmal

## 1.0.0-alpha.25 (2026-02-06)

### 🩹 Fixes

- Pre-warm Metro bundles to reduce startup time for tests. This improves responsiveness across the supported platforms and Jest runner. ([](https://github.com/callstackincubator/react-native-harness/commit/))
- Pre-warm Metro bundles to reduce startup time for tests. This improves responsiveness across the supported platforms and Jest runner. ([](https://github.com/callstackincubator/react-native-harness/commit/))
- Pre-warm Metro bundles to reduce startup time for tests. This improves responsiveness across the supported platforms and Jest runner. ([](https://github.com/callstackincubator/react-native-harness/commit/))
- Add support for resolving `tsconfig` path aliases in Metro. This helps apps that rely on TypeScript path mappings bundle correctly. ([](https://github.com/callstackincubator/react-native-harness/commit/))
- Pre-warm Metro bundles to reduce startup time for tests. This improves responsiveness across the supported platforms and Jest runner. ([](https://github.com/callstackincubator/react-native-harness/commit/))
- Pre-warm Metro bundles to reduce startup time for tests. This improves responsiveness across the supported platforms and Jest runner. ([](https://github.com/callstackincubator/react-native-harness/commit/))
- Pre-warm Metro bundles to reduce startup time for tests. This improves responsiveness across the supported platforms and Jest runner. ([](https://github.com/callstackincubator/react-native-harness/commit/))
- Pre-warm Metro bundles to reduce startup time for tests. This improves responsiveness across the supported platforms and Jest runner. ([](https://github.com/callstackincubator/react-native-harness/commit/))
- Support screenshots of elements larger than the viewport by capturing the full bounds of the element. ([](https://github.com/callstackincubator/react-native-harness/commit/))
- Pre-warm Metro bundles to reduce startup time for tests. This improves responsiveness across the supported platforms and Jest runner. ([](https://github.com/callstackincubator/react-native-harness/commit/))
- Support screenshots of elements larger than the viewport by capturing the full bounds of the element. ([](https://github.com/callstackincubator/react-native-harness/commit/))

## 1.0.0-alpha.24 (2026-01-26)

### 🩹 Fixes

- Enables collection of coverage data in monorepository scenarios through the new coverageRoot configuration option. ([#59](https://github.com/callstackincubator/react-native-harness/pull/59))
- Added support for web platform with all functionalities supported by the native equivalents, including UI testing capabilities. ([#62](https://github.com/callstackincubator/react-native-harness/pull/62))
- Added `forwardClientLogs` option to forward React Native logs to terminal during tests ([#63](https://github.com/callstackincubator/react-native-harness/pull/63))
- Add interactive Harness init wizard to guide users through setup and config. ([#60](https://github.com/callstackincubator/react-native-harness/pull/60))

### ❤️ Thank You

- Miklós Fazekas @mfazekas
- Sylvain Abadie
- Szymon Chmal @V3RON

## 1.0.0-alpha.23 (2026-01-19)

### 🩹 Fixes

- There was a change made by mistake to the package.json of the runtime package, resulting in broken release. This is now reverted back to normal. ([8b73b17](https://github.com/callstackincubator/react-native-harness/commit/8b73b17))

### ❤️ Thank You

- Szymon Chmal @V3RON

## 1.0.0-alpha.22 (2026-01-19)

### 🩹 Fixes

- Introduces UI testing capabilities with a new `@react-native-harness/ui` package that provides screen queries, user event simulation (press, type), and visual regression testing through `toMatchImageSnapshot`. This enables comprehensive component and integration testing with real device interactions, similar to React Testing Library but running on actual iOS and Android devices. ([#35](https://github.com/callstackincubator/react-native-harness/pull/35))

### ❤️ Thank You

- Szymon Chmal @V3RON

## 1.0.0-alpha.21 (2026-01-15)

### 🩹 Fixes

- Adds Object.hasOwn polyfill to the runtime package for JSC (JavaScriptCore) compatibility. ([#53](https://github.com/callstackincubator/react-native-harness/pull/53))
- Add automatic app restart functionality when apps fail to report ready within the configured timeout period, improving test reliability by recovering from startup failures. ([#55](https://github.com/callstackincubator/react-native-harness/pull/55))
- Added native crash detection during test execution that automatically detects when the app crashes, skips the current test file, and continues with the next test file after restarting the app. ([#56](https://github.com/callstackincubator/react-native-harness/pull/56))
- Bundling errors are now displayed in the CLI output, providing immediate feedback when build issues occur. ([#57](https://github.com/callstackincubator/react-native-harness/pull/57))

### ❤️ Thank You

- bheemreddy-samsara @bheemreddy-samsara
- manud99 @manud99
- Szymon Chmal @V3RON

## 1.0.0-alpha.20 (2026-01-07)

### 🩹 Fixes

- Added `webSocketPort` option to `rn-harness.config` (default 3001). This allows configuring the Bridge Server port, enabling usage of custom ports without rebuilding the application. ([#44](https://github.com/callstackincubator/react-native-harness/pull/44))
- The module mocking system has been rewritten to improve compatibility with different versions of React Native. Instead of fully overwriting Metro's module system, the new implementation surgically redirects responsibility for imports to Harness, allowing for better integration with various React Native versions while maintaining the same mocking capabilities. The module mocking API has been slightly modified as part of this rewrite. ([#49](https://github.com/callstackincubator/react-native-harness/pull/49))
- Fixed inconsistent Android device manufacturer and model matching. Some devices reported manufacturer and model information in non-lowercased form, which could cause device identification issues. Device information is now normalized to lowercase for consistent matching. ([#45](https://github.com/callstackincubator/react-native-harness/pull/45))
- Updated `chai` and `@vitest/expect` dependencies to resolve test crashes caused by Hermes not understanding bigint literals. ([#37](https://github.com/callstackincubator/react-native-harness/pull/37))
- Fixed HMR (Hot Module Replacement) initialization race condition by adding retry logic with delays when disabling HMR, ensuring Harness waits for HMR to be ready before proceeding. ([#38](https://github.com/callstackincubator/react-native-harness/pull/38))

### ❤️ Thank You

- bheemreddy-samsara @bheemreddy-samsara
- manud99 @manud99
- Szymon Chmal @V3RON

## 1.0.0-alpha.19 (2025-12-21)

### 🩹 Fixes

- ## Features ([](https://github.com/callstackincubator/react-native-harness/commit/))

  - Add support for expo-dev-client
    Enables development with Expo's development client for enhanced debugging capabilities
  - Guard against augmenting the Metro config twice
    Prevents duplicate Metro configuration modifications that could cause issues
  - Run Metro internally
    Integrates Metro bundler execution within the harness for better control

  ## Fixes

  - Add missing use-sync-external-store dependency
    Fixes runtime errors by including required React hook dependency

  ## Chores

  - Reduce install size
    Optimizes package dependencies to decrease installation footprint
  - Add GitHub Actions for Harness
    Sets up automated CI/CD workflows for the project

## [1.0.0-alpha.18] (2025-11-03)

### Features

- **Metro Caching** ([#23](https://github.com/callstackincubator/react-native-harness/pull/23)): Added support for Metro's transformation cache, helping in cases when Metro struggles with re-transforming the same files over and over.

- **Improved Timeout Handling** ([#24](https://github.com/callstackincubator/react-native-harness/pull/24)): Enhanced timeout handling to propagate timeouts not only to the initial bootstrapping process but also to all commands sent to the device.

- **Platform Architecture Refactor** ([#22](https://github.com/callstackincubator/react-native-harness/pull/22)): Introduced a major refactor of the Harness architecture, splitting the CLI package into several smaller packages. This makes it possible to create custom platform packages without modifying existing ones. The Metro integration has also been revamped to be more reliable in CI environments.

### Documentation

- **GitHub Actions Workflow Update** ([#25](https://github.com/callstackincubator/react-native-harness/pull/25)): Updated the example GitHub Actions workflow for iOS by adding a step to install Watchman, which dramatically speeds up the file-crawling process and makes Harness run much faster.

## [1.0.0-alpha.17] (2025-10-22)

### Features

- **Metro Regression Workaround** ([#21](https://github.com/callstackincubator/react-native-harness/pull/21)): Changed the way config is augmented to return an async function, working around a regression in Metro.

- **Migration Prompts** ([#19](https://github.com/callstackincubator/react-native-harness/pull/19)): Added migration guide to help users transition from the old CLI to the new Jest-based workflow. Users with unsupported configuration properties will be prompted to migrate.

### Bug Fixes

- **Bundle URL Fix** ([#20](https://github.com/callstackincubator/react-native-harness/pull/20)): Fixed incorrect URL with double slashes used during test bundling, which was causing failures due to changed behavior in React Native or Metro.

## [1.0.0-alpha.16] (2025-10-22)

### Features

- **Split Setup and Setup After Env** ([#18](https://github.com/callstackincubator/react-native-harness/pull/18)): Split setup files into separate setup and setup after environment phases for better control over test initialization.

- **UI Components Support** ([#17](https://github.com/callstackincubator/react-native-harness/pull/17)): Added basic support for testing UI components in React Native Harness, enabling component-level testing capabilities.

- **Jest Wrapper CLI** ([#16](https://github.com/callstackincubator/react-native-harness/pull/16)): Replaced custom CLI implementation with a Jest wrapper, providing better integration with the Jest ecosystem and improved compatibility.

- **Jest Preset Re-export** ([#15](https://github.com/callstackincubator/react-native-harness/pull/15)): Re-exported Jest preset from the main package for easier configuration and setup.

- **Watch Mode Performance** ([#14](https://github.com/callstackincubator/react-native-harness/pull/14)): Significantly improved watch mode speed, making the development experience faster and more responsive.

- **Code Frame Error Display** ([#13](https://github.com/callstackincubator/react-native-harness/pull/13)): Enhanced error reporting in Jest with code frames, making it easier to identify and fix issues by showing the exact location of errors in context.

- **Jest Globals Detection** ([#12](https://github.com/callstackincubator/react-native-harness/pull/12)): Added validation to throw errors when Jest globals are used, ensuring proper test isolation and preventing common testing pitfalls.

- **Coverage Support** ([#10](https://github.com/callstackincubator/react-native-harness/pull/10)): Implemented code coverage reporting capabilities.

- **Reset Environment Config** ([#11](https://github.com/callstackincubator/react-native-harness/pull/11)): Added `resetEnvironmentBetweenTestFiles` configuration property for better test isolation control.

- **Auto-apply Babel Plugins** ([#9](https://github.com/callstackincubator/react-native-harness/pull/9)): Babel plugins are now automatically applied, reducing manual configuration requirements.

- **Auto-inject Harness** ([#8](https://github.com/callstackincubator/react-native-harness/pull/8)): Harness is now automatically injected into the test environment, simplifying setup process.

- **Setup Files Support** ([#6](https://github.com/callstackincubator/react-native-harness/pull/6)): Added support for Jest setup files, allowing for better test environment configuration.

- **Harness-based Jest Runner** ([#4](https://github.com/callstackincubator/react-native-harness/pull/4)): Implemented a custom Jest runner built on the Harness architecture.
