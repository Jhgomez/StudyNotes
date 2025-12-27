# [Get your App Performance Score](https://developer.android.com/topic/performance/app-score#static-score)
The App Performance Score provides app developers with static and dynamic assessments. Here we are instructed on values we should be monitoring like app startup time, existensce of baselie profiles

# Inspecting Performance
You most likely want to or may actually need to inspect your app's performance of one or more of the following events:

* App startup
* Slow rendering (jank)
* Screen transitions and navigation events
* Long running work
* Operations in the background, such as I/O and networking

There are two main approaches when inspecting performance, manual and automated. It's likely that you start with manual debugging when inspecting a new area.

## Manual inspection
Perfetto is the best tool to inspect performance on devices Android 9 and higher. check the [Quickstart: Record traces on Android](https://perfetto.dev/docs/getting-started/system-tracing) guide. Also watch the
the in-depth series on [performance debbugging](https://www.youtube.com/playlist?list=PLWz5rJ2EKKc-xjSI-rWn9SViXivBhQUnp). We will also talk more about manual inspecction when we talk about types of traces, like 
system traces, stack traces, etc.

You can check more about perfetto later but in this section we will talk about Android Studio Profilers

### [Android Studio Profilers/Profile your app performance](https://developer.android.com/studio/profile)
Be aware in Windows and Linux only you can run the standalone profiler without having to run android studio by going to folder "studio-installation-folder/bin" and executing "profiler"

In order to [profile your app](https://developer.android.com/studio/profile), you will be required to have the following

* An app with a release build variant that has the profileable manifest configuration enabled, also known as a profileable app. By default, apps have this configuration set to true. It is defined inside the
  application tag `<profileable android:shell="true" />`. Or Use a debuggable app instead of a profileable app if you need to record Java/Kotlin allocations, capture a heap dump, or see the Interaction
  timeline in task views that provide it.
* A virtual or physical test device that runs API level 29 or higher and has Google Play.
* Android Gradle Plugin 7.3 or higher.

#### Profileable v. debuggable apps
A debuggable app is based on the debug build variant of your app and lets you use development tools such as the debugger; however, it comes with some performance costs. A profileable app is based on 
the release build variant of your app and enables a subset of common profiling tasks without the performance overhead of the debug build.

#### Build and run a profileable or debuggable app
To build and run a profileable app in Android Studio, follow these steps:

1. Create a run/debug configuration if you don't already have one. Basically this is done automatically by Android studio whenever you run a test, or just run the app, or run an app with the debbuger, you can
   in the tools.md file the setion "Create and edit run/debug configurations".
2. Select your release build variant (Build > Select Build Variant).
3. Click "More actions(is three dots icon to the right of the play icon to run an app)  > Profile '<NameOfRunConfig>' with low overhead(small guage icon)  or Profile 'app' with complete data(a bigger gauge icon)".
   Again, for full profile make it debbugable if not just make it profileable and use the low overhead option, a profileable app lets you do most common profiling tasks.

If for any reason instrcutions above fail, you can build and run a profileable app manually

#### Start profiling/Record A System Trace
1. Select a process from the list in the Home tab within the Profiler pane. In most cases, you'll want to select the top process that represents your app.
2. Select a profiling task from the Tasks section. If you don't know where to start, get an overall view of performance activity by inspecting your app live.
3. Use the Start profiler task from drop-down to select whether to start the profiler task from startup or attach to the process as it's running.
4. Click Start profiler task. The task starts in its own tab.
5. Interact with your app so activities are triggered.
6. Stop the recording (if applicable), wait for it to parse, and see the results.

The recordings are saved for the duration of the current Android Studio session; if you want to keep them for longer, export them by clicking Export recording . Not all trace types can be exported.

To edit your profiler task recording configuration, click "profiler settings" icon. There are two main settings you can toggle:

* For tasks that involve sampling, the Sample interval represents the time between each sample. The shorter the interval you specify, the faster you reach the file size limit for the recorded data.
* The File size limit represents the amount of data that can be written to the connected device. When you stop recording, Android Studio parses this data and displays it in the profiler window. If
  file is too large AS might have problems parsing it. if you're recording either a trace with a short sampling interval or an instrumented trace while your app calls many methods in a short time,
  you'll generate large trace files quickly. If you use a connected device running Android 8.0 (API level 26) or higher, there isn't a limit on the file size of the trace data, and the File size
  limit value is ignored. 

#### Reading Sytem Trace(With AS profilers)
After you record a trace, for example, if you notice a spike in the modem power rail, you should go to the threads section and see what thread activity could be causing the spike at the time.

Some metrics you can read with it are:
* **CPU Usage**: Shows CPU usage of your app as a percentage of total available CPU capacity by time.
* **Interactions**: Shows user interaction and app lifecycle events along a timeline (requires a debuggable app process and a device running API level 26 or higher).
* **Display**: Shows info related to how smooth your app UI renders. Select Lifecycle to inspect how long it takes your app to render each frame on the main thread and RenderThread.
  This info is helpful for investigating bottlenecks that cause UI jank and low framerates.
* **Threads**: Shows the threads that your app and various system processes run on. To learn about how to use system traces to investigate and help reduce UI jank, see Detect UI jank.
* **CPU cores**:  Shows the activity on each core in your device. Hold the pointer over a thread activity to see which thread this core is running on at that particular time.
* **Process Memory (RSS)**: Shows the amount of physical memory currently in use by the app.
* **Power Rails**: Appears when you profile on a physical device.
* **Battery**: Shows your app's battery usage.
