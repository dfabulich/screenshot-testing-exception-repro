This repository reproduces a bug in [Compose Preview Screenshot Testing](https://developer.android.com/studio/preview/compose-screenshot-testing).

To repro:

1. On the `main` branch, we have a normal screenshot test. Run `./gradlew --rerun-tasks updateDebugScreenshotTest` to generate (regenerate) its screenshot.
2. Switch to the `exception-bug` branch, where [the test has been updated to throw an exception](https://github.com/dfabulich/screenshot-testing-exception-repro/commit/b75a5607a27e77cfa46014e9209ae5d4f3b1df23). Run `./gradlew --rerun-tasks validateDebugScreenshotTest` again.

* Expected: The build should fail.
* Actual: gradle logs the exception, but then declares "BUILD SUCCESSFUL".

The only way to get the build to fail is to delete the stale generated screenshot in `app/build/outputs/screenshotTest-results/preview/debug/rendered/com/example/kotlinreflectrepro/GreetingScreenshotTestKt/GreetingPreview_748aa731_0.png`.
