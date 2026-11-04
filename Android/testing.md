# libs
```
org.hamcrest:hamcrest-library:1.3
org.mockito:mockito-core:2.13.0
junit:junit:4.13
org.robolectric:robolectric:3.0
androidx.test.espresso:espresso-core:3.1.0
androidx.test.ext:junit:1.1.1
androidx.test:rules:1.1.1
androidx.test:runner:1.1.1
```


* [Change the Test Build Type](https://developer.android.com/build/gradle-tips#change-the-test-build-type): By default, all tests run against the debug build type. You can change
this to another build type by using the testBuildType property in your module-level build.gradle file.

* You can learn how to change some of the instrumentation test configurations [here](https://developer.android.com/build/gradle-tips#configure-instrumentation-manifest-settings)


https://developer.android.com/studio/test

* Espresso vs UIAutomator: Android engineering teams combine both frameworks in the same test suite. For example, you can use Espresso to navigate through your app's internal
  screens rapidly, and then invoke UI Automator the moment a system permission dialog or system notification appears.

  | ---------------- | -------------- |
  | Feature	Espresso | 	UI Automator |
  | Scope	Single app (in-app UI) |	Cross-app and system-level UI |
  | Execution Process	Runs in-process alongside the app |	Runs out-of-process via the accessibility layer |
  | Speed	Fast (direct view hierarchy access)	| Slower (inter-process communication overhead) |
  | System/OS Access	Cannot touch system UI, permissions, or other apps | Can interact with notification shade, permissions, and settings |
  | Synchronization	Automatic (via IdlingResource) |	Manual/explicit waiting often required 

