# [Get your App Performance Score](https://developer.android.com/topic/performance/app-score#static-score)
The App Performance Score provides app developers with static and dynamic assessments. Here we are instructed on values we should be monitoring like app startup time, existensce of baselie profiles

You should:

* Meassure App start up time
* Measure app startup time from a notification
* Measure animation and scroll rendering
* Measure full screen rendering issues,  how long it takes for the screen to be fully rendered and become interactive

Be aware calling `reportFullyDrawn()` by using the `FullyDrawnReporter` or `ReportDrawn()` lets the system know when the app is ready to be interacted with by a user. This enables access to the TTFD metric. This metric can be used for benchmarking and enables improved Startup Profile creation.

# Memory Management 
Android processes share memory. To start a new app process, the system forks the Zygote process then loads and runs the app's code in the new process. This approach allows most of the RAM pages allocated for framework code and resources to be shared across all app processes. There is other ways it shares memory but the point is
that due to the extensive use of shared memory, determining how much memory your app is using requires care, but there are techniques to determine the app's memory
use as described in the [create a heap dump](https://developer.android.com/studio/profile/capture-heap-dump) documentation.

To determine the memory footprint for an application, any of the following metrics may be used:

* Resident Set Size (RSS): The number of shared and non-shared pages used by the app
* Proportional Set Size (PSS): The number of non-shared pages used by the app and an even distribution of the shared pages (for example, if three processes are sharing 3MB, each process gets 1MB in PSS)
* Unique Set Size (USS): The number of non-shared pages used by the app (shared pages are not included)

[Here](https://developer.android.com/topic/performance/memory/guide/concepts#rss-pss-uss) is a visual representation of these distributions.

The heap of a process starts at the required size by the app and then it can grow dinamically but only up to a limit tha the system defines for each app. The exact heap
size limit varies between devices based on how much RAM the device has available overall. If your app has reached the heap capacity and tries to allocate more memory, it 
can receive an `OutOfMemoryError` The logical size of the heap is not the same as the amount of physical memory used by the heap. When inspecting your app's heap, 
Android computes a value called the Proportional Set Size (PSS), which accounts for both dirty and clean pages that are shared with other processes—but only in an amount
that's proportional to how many apps share that RAM. This (PSS) total is what the system considers to be your physical memory footprint. In the previously mentioned 
section, "Create a Heap Dump", you can learn how to read this info. So these pages can be either clean or dirty, clean are pages that are file-backed, means that they 
represent a resource that was loaded from storage and can be reproduce very easily, dirty happens when we change somehting in those files, if we modify a file and it is
not written to storage yet, and there is also anonymous data, the heap our app uses actually ives in anonymous pages, anonymous is everything that is not backed by a a file
in the storage

`getMemoryClass()` method returns an integer indicating the number of megabytes available for your app's heap, you can use this info for example, to determine how much data is safe to keep in a cache. 

Apps in the background can be cached, a cached process that retains resources that it currently does not need affects the system's overall performance. The less memory
your app consumes while in the cache, the better its chances are not to be killed and to be able to quickly resume. 

## Stressful App Test
`stressapptest` is a memory interface test that helps create realistic, high-load situations to test various memory and hardware limitations for your app. With the 
ability to define time and memory limitations, this allows you to write instrumentation to verify real-world encounters of high-memory situations. For example, use the
following set of commands to push the static library in your data file system, make it executable, and run a stress test for 20 seconds of 990 MBs:

```
adb push stressapptest /data/local/tmp/
adb shell chmod 777 /data/local/tmp/stressapptest
adb shell /data/local/tmp/stressapptest -s 20 -M 990
```

`stressapptest` can be used to request memory allocations larger than freely available. This type of request can raise various alerts, which you should be aware of from the development side. 

# [Memory allocation among processes](https://developer.android.com/topic/performance/memory-management)

The Android platform runs on the premise that free memory is wasted memory. It tries to use all of the available memory at all times. For example, the system keeps apps
in memory after they've been closed so the user can quickly switch back to them. For this reason, Android devices often run with very little free memory. Memory 
management is vital to properly allocate memory among important system processes and many user applications.

On Android, storage isn’t used for swap space like it is on other Linux implementations since frequent writing can cause wear on this memory, and shorten the life of the storage medium.

The system can move annnonymous dirty pages and dirty pages to zRAM, dirty pages are pages that contain ram that is a copy of a file which original exists on storage,
the system would not be able to restore these pages so it doesn't delete them when it needs to free memory up and instead it compresses them into the zRAM. It can be
decompressed later, however compressing and decompressing can cause UI janks this whole process is responsibility of the "kernel swap daemon" (kswapd), however when
the system can not free more memory by compressing pages, it then starts killing processes which is responsiblity of "Low-memory killer" (LKM) when this happens the
system uses `onTrimMemory()` to notify an app that memory is running low and that it should reduce its allocations. If this is not sufficient, the kernel starts 
killing processes to free up memory. The systems kills processes based on a score, processes with a high score are killed first. Background apps are first to be killed,
and system processes are last to be killed. Background apps are killed first, then the most recent previous app that was used is killed (you can think of it as the last app to be killed in the background apps list), then the home app, then the services started by apps, Perceptible apps (not foreground apps but are perceptible like 
listening to music), then the Foreground app, then framework services such as telephony and wi=fi, then the system process, then very low level processes used by the 
system like `kswapd`

You should always diagnose heavy memory critical user journeys, these include 

* Loading and manipulating complex media or large bitmaps.
* Hosting WebView instances. See here for how to [manage and diagnose webview memory](https://developer.android.com/develop/ui/views/layout/webapps/manage-webview-memory)

The source code used in this examples and more info can be found in [this AOSP repo](https://android.googlesource.com/platform/development/+/android17-release/guides/memory/)

## Avoid memory churn
Garbage collection events don't affect your app's performance. Numerous garbage collection events ocurring in a short period of time can quickly drain the battery as
well as marginally increase the time to set up frames due to necessary interactions between the garbage collector and app threads. The more time the system spends on
garbage collection, the faster the battery drains.

# [Processes and Threads](https://developer.android.com/guide/components/processes-and-threads)
When an application component starts and the application doesn't have any other components running, the Android system starts a new Linux process for the application 
with a single thread of execution. By default, all components of the same application run in the same process and thread, called the main thread.

If an application component starts and there is already a process for that application, because another component from the application already started, then the 
component starts within that process and uses the same thread of execution. However, you can arrange for different components in your application to run in separate 
processes, and you can create additional threads for any process.

# [Inspect your app's process state and budget](https://developer.android.com/topic/performance/memory/app-memory-budgets#inspect-process-state)
Starting Android 17 apps can declare memory budgets. You can define different budgets for when your app is the inte foreground, perceptible and background. One way to 
inspect your app's active process state and importance during development is by querying Activity Manager using ADB:

```
adb shell dumpsys activity processes <package-name>
```

To inspect your app's current resident memory usage:
```
adb shell dumpsys meminfo -a <package-name>
```

an example for a multiprocess streaming music app using memory budgets is [here](https://developer.android.com/topic/performance/memory/app-memory-budgets#multi-process-budgets).
You Can learn more about the command above [here](https://developer.android.com/topic/performance/memory/guide/tools-overview), in Android 18 this also prints memory limit
set by the system, budget, budget at runtime or the adb.

Use [procstats](https://developer.android.com/topic/performance/memory/guide/tools-overview#procstats). While meminfo provides a snapshot in time, procstats provides historical 
data by periodically sampling the state and memory use of all running applications. This is the primary tool used for long-term memory health monitoring and is what drives the 
memory usage reporting in Android Settings. View stats for the last 3 hours `adb shell dumpsys procstats --hours 3`. This returns us min/avg/max of RSS, PSS and USS at the same
time, if you see max is significantly higher than min, and the average creeps up over time as sample count increases.

# Obtaining heap dumps
## [Using AHAT (Android Heap Analysis Tool)](https://developer.android.com/topic/performance/memory/guide/java-memory#obtain-java-heap-dumps)
To run this command, you must build your app with `<profileable android:shell="true"/>` or `<debuggable>`. As mentioned in this document you can actually create a run config to
run your app with profiling enabled. In java you can use `jcmd` to do GC heap dumps to get hprof files.

```
# 1. Trigger the dump (the command takes a moment to complete):
adb shell am dumpheap -g -b png com.android.memorylab /data/local/tmp/heap.hprof

# 2. Pull the file to your development machine:
adb pull /data/local/tmp/heap.hprof .
```

then launch AHAT

```
ahat heap.hprof

# or run the standalone jar
java -jar ahat.jar heap.hprof

# open the broswer in http://localhost:7100.
```

On the browser you can find your activity, this helps you find GC Roots, the collector treats GC root as always reachable object. The GC root can contain a series of references
to other objects that finally point to a leaked object. **Sample Path from GC Root** option shows the chain of references preventing the object from being garbage collected, and
**Object Size** shows how much memory is being retained by this specific instance. AHAT has a specialized view for identifying leaked Activities, which are one of the most common 
and impactful memory leaks in Android.

### [Diffing Heap Dumps](https://developer.android.com/topic/performance/memory/guide/java-memory#diffing-heap-dumps)
Taking a "clean" dump as a baseline and comparing it against a dump captured after you have performed some actions is a great way to find leaks and AHAT makes it easy for us.
```
java -jar out/host/linux-x86/framework/ahat.jar leaked.hprof --baseline base.hprof
```

### Examples
A GC root is not always directly holding the leaked object, the GC only traces roots for these types:
* Static fields of loaded classes
* Local variables and parameters on the stack of a live thread
* Live threads themselves
* JNI global references from native code
* Objects used as monitors (synchronized) and a few JVM-internal ones

Everything else is an ordinary heap object. Let's see what this means with two examples:

```
class MyActivity: Actiivity() {
   static LeakClass anInstance;

  void onCreate() {
    if (anInstance == null) {
       anInstance = new LeachClass(this.context);
    }
  }
}
```

In here the only reason this is a leak is because `anInstance` is a stattic field, if it wasn't then it would survive config changes and therefore no leak would exist. But since
it is a static field it will outlive an activity's lifecycle and since it is a static field it is also the GC root and the path to the GC root looks like:

```
MyActivity.class  (static field anInstance)   ← GC root
  → LeakClass
    → context
      → MyActivity #1 (destroyed on rotation)  ← leaked
        → Window, DecorView, the whole view tree, resources...
```

But if we pass the context to a singleton repository provided by the Dagger singleton component, then it looks like this:

```
ActivityThread.sCurrentActivityThread     ← GC root (static field)
  → ActivityThread.mInitialApplication
    → MyApp (your @HiltAndroidApp)
      → ApplicationComponentManager
        → SingletonC (generated Dagger component)
          → DoubleCheck (the scoped provider caching the instance)
            → Repository
              → context
                → MainActivity (destroyed)   ← leaked
```

Notice the root isn't the repo. `ActivityThread` is a class that manages an app's process, its `main` method is the entry point of android apps, where the main Looper is set up, it creates 
the `ActivityThread` object, stores it in the static field `sCurrentActivityThread`, and then calls `Looper.loop()` forever. That loop is your main thread. That static field of type 
`ActivityThread` holds both the app and activity instance:

```
ActivityThread
 ├─ mInitialApplication → MyApp → Dagger component → Repository → old MainActivity
 └─ mActivities (map of ActivityClientRecord) → current MainActivity
```

When the old activity is destroyed, its record is removed from mActivities. That path is gone. The only remaining path to the old activity is through the application, the singleton component
and the repository, and that’s why it leaks. But as I mentioned a thread stack is also a root so we have at least two routes leading to the same object:
```
static ActivityThread.sCurrentActivityThread ─┐
                                              ├→ ActivityThread object → MyApp → …
main thread stack (ActivityThread.main local) ┘
```

This is becaus The main thread’s stack has the `ActivityThread.main()` frame. That frame’s local variable references the same `ActivityThread` object, and Looper.loop() is still running on top
of it. Depending on the tool and its version you're using you may see either or root in this case, but the solution would be the same, just notice that the class causing the leak is not the 
GC root in this case.

### [Recording allocation stack traces](https://developer.android.com/topic/performance/memory/guide/java-memory#recording-allocation-stack-traces)
**Sample Path from GC Root** tells you why an object is still alive, it doesn't tell you how it was created. Allocation stack traces provide the exact line of code that allocated 
an object. Thew below commands record every allocation's stack trace, this is computationally expensive and consumes significant memory. In a large production app, this can make 
the app nearly unusable.

```
# Increase the allocation tracker's stack depth (requires a process restart)
adb shell setprop dalvik.vm.allocTrackerMaxStack 16

adb shell am force-stop com.android.memorylab
adb shell am start --track-allocation -n com.android.memorylab/.MainActivity
```

After running those commands, you interact with your app, and then take a heap dump. Open the dump in AHAT. Navigate to a large `byte[]` instance. (e.g., inspect `MainActivity` →
`mJavaAllocations` (`ArrayList`) → elementData (`Object[]`) → array element [0]). In the instance view, look at the Allocation Site section. It will show the full stack trace 
leading to `MainActivity.allocateJava`

## [With Perffeto](https://developer.android.com/topic/performance/memory/guide/java-memory#using-perfetto)
Perfetto can also capture Java heap dumps as part of a system-wide trace by enabling the android.java_hprof data source in your Perfetto config. This is useful for correlating 
heap state with other system events. Unlike standard .hprof files, Perfetto's Java heap dumps only capture the object reference graph, not the actual data contents of fields and
only perfetto can read them

# [App Code Is Memory](https://developer.android.com/topic/performance/memory/guide/app-code#why-matters)
Your app instructions load from an `.apk` file, this means that code is file-backed. When you write code in Java and Kotlin, that code is actually turned into assembler instructions.
Assembler instructions depend on the architecture of the CPU, the most common architecture in mobile phones is `ARM64 ISA` which is a RISC (Reduce Instruction Set Computer). Each
instruction in this architecture takes 4 Bytes of storage, when it is loaded into RAM the same ammount of bytes are copied into RAM. For example iterating on a list with an Iterator
rather than a simple for loop can be more expensive because of Iterator's method calls and its alloaction itself. You can measure code impact using `meminfo` and `showmap`

# [Keep background work alive with a lean process](https://developer.android.com/topic/performance/memory/guide/process-splitting)
Many apps perform legitimate work when their UI is no longer visible, such as downloading large asset packs, synchronizing local databases, streaming audio, recording exercise 
workouts, or maintaining a connected-device session. When this background work runs inside the same OS process as your foreground UI and graphics engine, the entire process stays
at an elevated importance level together with all of the memory that the UI allocated. This means that if the app is running a lightweight service and while the app is in the background
this could block the system from reclaiming memory that the UI was using. In order to fix this you just run the service in a different process, just add the propery `android:process=":bg"`
in its manifest declaration. I think this applies to the firebase messaging service, I have to test to make sure it is ok to initialize it in a different process but in theory that
actually is the most responsible resource use.

# [Inspecting Performance](https://developer.android.com/topic/performance/inspecting-overview)
Perfromant apps consume resources efficiently, RAM(no leaks, no churns therefore no highly frequent or long GCs), baterry friendly, is CPU optimized, efficient storage footprint, 
has immediate response, starts fast, UI is smooth and fluent, low network usage. You most likely want to or may actually need to inspect your app's performance of one or more of the 
following events:

* App startup
* Slow rendering (jank)
* Screen transitions and navigation events
* Long running work
* Operations in the background, such as I/O and networking

There are three ways of inspecting what is happening so you can see if it aligns with your expectations, passive, manual and automated. 

## Passive
Is when you find slow rendering by interacting with your app directly, or when you find info using Logcat.

You can search for skipped frames in Logcat using `package:mine tag: Choreographer`, this is complex because devices can render at different rates, for example, 90 frames per 
second. If a frame last more than 700 milliseconds is considered a frozen frame and you can search them with `package:mine tag: OpenGLRenderer` they will say "Davey!", after 
5 seconds delay you get a ANR. You can spot slow app startups searching for `tag: ActivityTaskManager Displayed` this is the time-to-initial-display (TTID) which is the time 
it took to draw the first frame when an activity is opened, if you use the Activity's method `reportFullyDrawn()` which would represent the time-to-fully-drawn (TTFD), this 
uses the `FullyDrawnReporter` under the hood, you can see it with `tag: Fully drawn`.

**DON'T USE AN EMULATOR TO MEASSURE PERFORMANCE**, **DEBUGABLE CAN BE USED WHEN YOU NEED HEAP DUMPS**. When doing system traces or profiling CPU performance, and taking call
stack samples and recording continous call stack sessions you will always want a `profileable` build, these builds are based on top of release builds, since you are measuring
CPU performance you almost always want these builds to be optimized and most of the times obfuscated also, but sometimes when doing method traces/profiles you need to disable
obfuscation temporarily. For cpu performance debugging and measurement you NEED a physical device. Debugging memory on the other hand needs debug builds (not release, 
nor profileable).

## Manual inspection
Perfetto is the best tool to inspect performance on devices Android 9 and higher. check the [Quickstart: Record traces on Android](https://perfetto.dev/docs/getting-started/system-tracing) 
guide. Also watch the the in-depth series on [performance debbugging](https://www.youtube.com/playlist?list=PLWz5rJ2EKKc-xjSI-rWn9SViXivBhQUnp). We will also talk more about 
manual inspecction when we talk about types of traces, like system traces, stack traces, etc.

## Automated
### Macrobenchmark
Be aware that a debuggable app is effectively profileable, if we add the profileable property to the manifest in android it really only takes effect in a non-debuggable build 
type, like release, and when used in a release build it allows the app to be profileable without being debuggable. Profileable apps introduce a small overhead compared to 
debuggable apps, the former allows us to trace cpu usage, and we can see dropped frames, what a thread is doing, power consumption, etc. When debugging performance you usually 
will start doing system traces, traces require profileable builds, but debuggable apps are useful to further troubleshoot performance issues, it enables more useful debugging 
capabilities, however it only comes at a performance cost, performance debuging with debugable builds is actually a heavy resouce consuming activity. Performance meassuring, 
which is what macrobenchmark is for, needs profileable builds and its overhead is small. Both, When you are measuring performance (Macrobenchmark) and when you're debugging 
performance (traces like system trace or method trace only, not sampling like heap dumps) you need an environment similar or identical to what the user sees (release builds), 
measuring performance of unoptimized code doesn't makes much sense, tracing unoptimized code can be misleading, these two activities should be done in physical devices, not 
emulators, because emulators run on top of your computers hardware which is not a real world scenario. So to set up a real world environment you need to run performance 
measurment and system tracings in a release build, but not any release build, it has to be profileable because this enables profilers to attach to your app without the overhead 
of debuging hooks. Your release builds should have optimized, obfuscated and shrunk code, and profileable builds will have these configurations as well. However there are times 
when obfuscated code won't let you debug performance issues such as when doing method traces, this is because you basically can't read it. But in other traces it doesn't make a 
difference. So using obfuscated code in traces is optional, it seems like trace points are not subject to this issue so if you can debug performance just using trace points on 
obfuscated code then you're fine. If you can not debug performance with obfuscated code, then you can disable it by adding the following proguard rule: `-dontobfuscate`. Again, 
obfuscated code seems to not have a negative impact on system traces, as opposed in method traces where you most likely can't use obfuscated code. You can run Macrobenchmark 
with obfuscated code, however if the meassure results are not what you expected then which suggest some perfomance regressions, then you may like to have MB take a method tracing 
(yes, macrobenchmark can take method tracing but it won't replace system tracing, it seems like MB relies on system tracing to do its job, so you can't replace the default system 
traces with method traces, but you can have both). If the code is obfuscated you will not be able to read those method traces. So it is optional to have obfuscated code, but since 
you really don't get any performance benefit form it you may just disable it by default in build used for system tracing and measure performance, the code is still optimized and 
shrunk though. For baseline profiles you have to disable obfuscation, don't worry about this, after you get the profile you just actually do the release build with those files and 
everything will end up being obfuscated. In perfetto traces the issue is the same when you just want to trace the system obfuscation is fine, but when tracing methods and debbuging
memory usage then you must likely don't want obfuscated code. To sum up, builds used in performance tracing and measurement should be optimized, shrunk, profileable, but not 
obfuscated. Builds used in sampling like heap dumps and stack traces should be debuggable.

Use Macrobenchmark to prevent problems before they hit production. In [this video(6:30)](https://youtu.be/-Mgy_nTMCtc?si=UMeificD5sQaXcml) we are told that in order to configure 
Macrobenchmark tests, we need to add a build type, in the video android studio adds it automatically to the app module gradle file but this seems to either have changed over time 
and also there is other ways to configure them correcly (Using run configurations), in newer versions of the "Now in android" app it seems like it is not even set manually, meaning 
a build type is added automatically and they only add it to the `app` and `benchmark` module, in the video the app module set `debuggable = false` and in the `benchmark` module 
this flag is true, so that I need to clarify. They show how to set up my macrobenchmark. They show we can use startup modes, `COLD` useful for app start up, it helps you understand 
it better. `WARM` or `HOT` are used when you don't require cold starts such as caching mechanisms or user flows that won't need to start cold, in the test call `pressHome()` to 
reset the state of the device your benchmarks on, `startActivityAndWait()` which starts default activity and until first frame is drawn, these two function calls are enough to 
measure TTID, Macrobenchmark will stop by default after TTID. For a TTFD you'd need to wait for a specific UI state like having a text on screen and you do that with `UIAutomator` 
(`device` object). Benchmarks should run on a physical device. The results are created in `outputs/connected_android_test_additional_output/benchmark/connected/SOME_CODE`, you can 
find them as a json format also so you can parse them and plot them as part of your CI pipeline. Macrobenchmark results include system traces. 

## [Profile types and when each is helpful](https://developer.android.com/topic/performance/tracing/profile-types-overview)
Tracing and profiling are two different techniques used in performance analysis. 

Tracing involves collecting highly detailed data about the execution of a system. Traces contain enough detail to fully reconstruct the timeline of events, so if you look at the right
info in a trace you can fix a bug without reproducing it. It is impractical to read traces directly so you use a combination of trace analysis libraries and trace viewers, the libraries
provide a way to define trace events programmatically and viewers lets you see those events on a timeline. So tracing is some sort of performance analysis logging but it reflects it in
a structured way so you can see the timeline. In production what you need is **"field metrics"** we will talk more about it, this way you avoid the overhead of collecting traces in 
production but you're still able to spot performance issues which you can then trace in a lab environment. 

Profiling involves sampling some usage of a resource by a program. A single continuous session of recording is known as a profile. Each sample collects the function callstack, The most 
common types of profiling are memory profiling and CPU profiling. It seems the line between system trace and sampling is really thin, you could even use it interchangeably because
a continuous session profile can be seen as a System trace, maybe I'm wrong but as os right now it seems my conclusion is correct. However the difference might rely in that a sample
is perceived to collect a more detailed call stack, this call stack can be referred as stack trace and it is said that collecting this info consumes more resources, btw in theory
these only work with debuggable builds. Samples take time to collect so you can't use timing information from profiles (in android studio these are known as 
"Stack sampling profiles"/"call stack samples") to understand if something is taking too long, instead this is what system traces are for. Because work in Android can be distributed
across threads and processes, i.e, you could be doing a binder transaction on main thread so the work will be done in another thread or process. If the work is being done on another
thread during the period of time we want to debug, and you take a stack sample of the main thread you may end up with a stack that implicates the wrong thing, which is something you
can see with a trace, you can see how different pieces of work connects with each other; therefore, you usually want to take a trace and then a stack sample/profile. BTW A SLEEPING 
THREAD MEANS THAT IT IS BLOCKED AND THIS IS USUALLY BECAUSE IT IS DOING IO OR NETWORK CALLS OR IT COULD BE BEING BLOCKED ON PURPPOSE. In AS the stack samples functionality uses
[simpleperf](https://android.googlesource.com/platform/system/extras/+/master/simpleperf/doc/README.md) under the hood to take the stack sample profiles. It shows you Java method
calls as well as native functions and syscalls. There is another option previously called "Trace Java Methods" for stack method sampling profiles which seems to have changed its name
to "Find CPU Hotspots (Java/Kotiln method recording)" which will instrument and trace every method you enter and exit which tends to have way too much overhead to be reasonable.

So in the end all below are profiles, yes even system traces, but each has different characteristics. System traces don't consume as much resources as Stack sampling profiles. Traces
can be seen as the logging of performance debuging, AS profilers seem to be a little more detailed on CPU info while RAM usage is not too detail and it has a lot more info as already
mentioned, and profiles is just a very detail sample of cpu or RAM usage, in CPU you see method calls and in RAM you see memory allocations. Traces can not feasibly capture execution
of extreme high frequency events e.g. every function call. Profiling on the other hand can record extreme high frequency events like function calls and significantly cut down how much
info they store by taking samples. Profiles that collect every function call output GB of data everysecond so it they are impractical for anything beyond investigating small snippets
of code. Traces show you resource usage but doesn't tell why it happened nor what code is beign executed during that time.

If a method is called 50 times method profiles will just show you an statistical amount of how much time did the app spend executing those calls to the same method through a period 
of time while the trace will actually tell you "this fucntion was called 50 times and is slow because a method it calls inside it is slow"

* System trace: They provide a bird eye view of CPU usage, you can see system how your app interacts with the system/hardware, it is timing information so you can see the info
  through time, like how long did a frame take. Almost every video I have seen about performance debugging says this is the first step when debugging performance because it helps
  you understand more or less where **where** is the reason for a drop frame, how many drop frames there where. For example I intentionally blocked the main thread for 2S, it just
  shows a frame took 2S, it shows some long lines in the main thread, I can click the dropped frame and look into it, there is some long lines only in the main thread, it doesn't
  say anything about why, it only shows that the choreographer is a long line, it could be doing some work, I can't tell from just that, I know I blocked the thread. But when I
  click the droped frame it shows some statistics, it shows the existing threads states during the frame existence period, in the main thread I can see it has a 2.05 seconds sleep
  and the time it was in the running state was just 26ms, I can see that the expected duration was 16.67 so it would have been a dropped frame anyways, but I'm using an emulator
  and by looking at the lines it seems like it is something about the rendering pipeline and not my code. the first call is `Choreographer.doFrame`, then that calls, `animation`,
  next to animation I have `traversal` but this is called after the thread is not blocked anymore, below that line I have a line with calls to `Recomposer.recompose` right next
  to it aligning with the `taversal` portion on top I have `meassure` and `draw-VRI` then below it I have `Compose.recompose`, this level has also some other calls next to it
  the first call next (it doesn't matter what it is right now) is actually a block of calls, it is so small that I can see much about it and the smallest size I can trace dobe
  shows some info but I'm not going to look into it because there are quite a few of them but that set of tasks end aligns with the `meassure` call I mentioned previously, below this
  line I can see some binder activity happening. What I can tell from this info, I already know I'm blocking the thread but suppose I didn't know, when , his block of task I mentioned
  starts this represents the sleep time end, this meand the thread is not sleeping anymore at this point and from there until the frame ends there is also some running state, some
  small sleeping in `traversal`, you can put your pointer on top of these portions and it will tell you the time they spent running and idle. What you need to understand here is that
  this do show us some kind of LIFO stack, being the `choreographer.doFrame` the first call, which calls `animation` which calls, `recomposer.recompooe`, which calls
  `Compose.recomposoe`, but this one is the one that experiments the 2s sleep, and therefore also all of the previous callers are also delayed, when that ends it just do its work,
  when its work is done `Recomposer.recompose` returns, then `animation` returns and this line continues its works which is `traverslar` and the same cycle repeats, `traversal` calls
  `meassure` which calls `onMeassure` and so on until everything starts returning to `traversal`, when `travesal` returns then `doFrame` returns, when `doFrame` returns we have a
  frame draw on screen. You can also see that before a frame is visible on screen a call to `DrawFrames` in the render thread has to completed. I was able to see how work
  in the main thread relates to work in render thread. So as you can see it gives us an idea, for example if you see recomposition taking too long then you can go look into anything
  that is recomposing but this time using other traces types. This traces can contain system and user-defined events, these are triggered through function calls. There is two types of
  event, Trace slices, they represent the time between different points in your code, you add them with `Trace.beginSection` and `Trace.endSection` or `trace("secionName") {}`. Trace
  counters, numeric values that represent metrics, for example heap size. They can be added with `Trace.setCounter`. Trace points are used to try to narrow down root causes of
  performance issues, however instead of using those you can actually take some stack samples / stack traces using "stack sample profiles". A good example of how traces helps you,
  since you can see relationships between different pieces of work being done you can visually see that every frame that needs to update what the users sees on screen delegates drawing
  to the render thread, this means you can see that when render thread returns from the `drawFrames` request on the first frame (for example) only then the frame is considered done
  which means the user now sees your UI. System tracing can be more of a performance measure tool but also a performance measure debugging tool.
 
  System traces also contain metrics which can be created from PerfettoSQL queries and can be used to perform analysis or compare traces. System traces work great for finding
  latency issues caused by delays, waits, or scheduling problems, so you can diagnose latency problems. It can help you spot duplicated computations. Finding lock contentions
  are possible because you can see what a thread is doing.

  You can learn how to read this profiles in AS [here](https://developer.android.com/studio/profile)

  In Android you have different ways to capture system profiles as shown [here](https://developer.android.com/topic/performance/tracing), you can use the AS CPU an memory profiler,
  Perfetto command-line tool (Android 10 and higher) you open this traces in Perfetto UI. Compared to AS system trace which focus on your app only, perfetto allows you to see all
  processes in the devices. System tracing utility (system traces on device). In Android 10 (API level 29) or higher, the on-device trace files are saved in Perfetto format, while
  earlier versions of android save them in Systrace format. The last option is Systrace command-line tool which is a legacy platform-provided command-line tool. I inlcude a sectino
  just for [perfetto](#perfetto) below. If you're not using the AS profilers you need to manage all configurations yourself so make sure to use a profileable build that is based on
  release, and enable or disable optimization and ofusctation as needed, all other options other the AS profilers won't show you a warning if you try to take a system trace of a
  debuggable build for example.

  You can define trace points to see app's code execution time directly in a system trace as explained [here](https://developer.android.com/topic/performance/tracing/custom-events).

  You can add in-process trace events, it is useful for debugging coroutines as shown [here](https://developer.android.com/topic/performance/tracing/in-process-tracing). This library
  seems to be a replacement to `androidx.tracing` library because this library performance is not that good, every single trace section can add 1,220ns in a Pixel 6A while this new
  API adds less overhead and executes faster, and it can't add additional app context, its labels can only be 147 charcters, and is Android only. While this other option supports KMP,
  has no label length limit, It seems like when you start it it creates a separate process, you can see it being used in a KMP/CMP desktop app [here](https://youtu.be/BhUf_Sv_Bv0?si=tmdAaHUMJcOh6uVW)
  to track recompositions

  If you ever need to find out what objects are taking too much time to be created or needs too many resources when it is creating and therefore creating is slow you can debug knowing
  that dependencies are injected in order, knowing this you can add dummy dependencies in between these objects, the dummy dependencies will do nothing more than adding tracing points

* Stack Sample Profiles: They record samples of code execution and saves call stack information at a set rate. In android studio that feature has changed name over time,
  I think it was previously called method tracing, but now is called "Find CPU Hotspots (Callstack Sample) or Method Sampling". There is another stack method sample profile
  option in AS, it was previously called "Trace Java Methods" which seems to have changed its name to "Find CPU Hotspots (Java/Kotiln method recording)" which will instrument
  and trace every method you enter and exit, which tends to have way too much overhead to be reasonable, that said, the former could miss recording work that happens in between
  samples because sampling is done at a set rate while the latter is a continuous session sample. These recording gives you information in terms of methods that where called.
  check [this video](https://youtu.be/21lY_MMiD2g?si=kYo_kzbJTRuFVjJp) to learn more about method stack profiles. Click specific threads to see a thread call stack in isolation
  . In the flame charts, Orange color functions represent android platform code while light yellow are functions in our app and dark yellow is java functions. You don't necessarily
  need an physical device because they don't give you timming info but you rather get statistics, however a phyisical device is always bettter, always use a physical when meassuring
  performance with Macrobenchmark and debugging performance with system traces. For method sampling either at a set rate or as a continuous session it seems that you can use either
  or build type, however know that unoptimized code and not obfuscated code can help you debug through the stack with your function names, for example, continuing with the
  system trace I made previously, I created a function called `myFun` which is called right before I call my first composable in my actiivty, this fucntion blocks the main thread
  for 2 seconds `Thread.Sleep(2000)`. If I run using a debug build I will see the function name however something else happens under the hood also, I have this code in my app
  `(context.applicationInfo.flags and ApplicationInfo.FLAG_DEBUGGABLE) != 0` this verifies if the manifest of the installed app is debuggable, when I install the app in a debug
  build it returns true, but if I start the app using the profiler even though it was installed as a debug build the code checking for debug builds now returns false but my code
  is still unoptimized and not obfuscated but now it seems to be not really debuggable and if I close and open the app the flag stil returns false now, so it modifies the installed
  app, so it looks like I get some build where minify is disable, no shrinking nor no obfuscation, but is really not debugable any more, if you try to attach the debugger it won't
  work. So when the profiler sees you use a debug build and start the profiler it just turns off shrinking and obfuscation, which is something you can do manually with the
  `-dontoptimize` and `-dontobfuscate` proguard rules in a release build. In conclusion always use a release build and if you want to debug with more detail add the "dont obfuscate"
  and "dont optimize" proguard rules, if you only do "not obfuscate" it could still be optimized so some functions could be inlined and won't exists in the stack, and if you only do
  "don't optimize" then you will see obfuscated names. Take this into account when taking traces manually with `adb` tools, always use a release build for system traces, and
  cpu call stack samples, however memory sampling and traces can only be done with true debug builds. You can collect call stacks programmatically so you can remove noise
  from your samples, btw those samples are stored on device so you need `adb` to pull them up to your computer (see the tips section). With these profiles you can spot code with a
  lot of CPU activity, so it helps you understand how your **code** behaves, note the keyword here is the code. Sampling profiles gives you statistical information, it is an
  agregatted of all samples

  To understand more how flame charts are generated look [here](https://developer.android.com/studio/profile/inspect-traces#flame_chart) but basically calls to the same function
  that have the same set of parents are agregated if another call to the same function is done with a different parent chain then they are displayed separately.

  Usually you want to collapse frames from the Java virtual machine (for example `android::AndroidRuntime::start` and `art::{...}`), and the system kernel (for example
  `[kernel.kallsyms]+{offset}`). Usually this corresponds to collapsing frames related to `[kernel.kallsyms]`, `/apex/`, and `/system/*`.

  In AS profiler you have "Callstack Sample" for method profiling with samples, and ["Java/Kotlin Method recording"](https://developer.android.com/studio/profile/record-java-kotlin-methods)
  which are really resource heavy because it records method calls with timing info, so they are some special kind of profile because they also seem to have some tracing characteristics

  Callstack samples is more of a debugging tool for performance not to measure performance.

* Heap Dumps: they're a snapshot of your app's Java heap memory. They help you understand memory usage, this means you can spot object using a lot of memory which you can then
optimize. This info can help you spot memory leaks, duplicated objects and bad memory usage patterns in general. They do require a debug build. See [this](https://developer.android.com/studio/profile/capture-heap-dump)
documentation to learn how to read them. in heap dumps you can spot small memory leaks easier if the dump is taken after a long session, it seems those object go to the top,
most likely because the they survive collections happening in the young gneration and therefore promoted to the  old Generation. Objects that survive enough collection cycles in
the young generation are promoted to the old generation

* Heap Profiles: They take samples when memory is allocated. They can help you spot memory churns, by reducing memory churns you can reduce garbage collection and reduce power
consumption and even janks (slow rendering) since heavy garbage collections can affect main thread. You can spot memory leaks using these profiles. It seems like in AS these
are recorded using [Track memory consumption (Java/Kotlin allocations)](https://developer.android.com/studio/profile/record-java-kotlin-allocations)

## Perfetto
There is perefetto command line tool and perfetto UI. The command line tool (part of android SDK) lets you collect performance information from Android devices via the Android 
Debug Bridge (ADB). Invoke the `perfetto` tool using the `adb shell perfetto ...` command, more info [here](https://developer.android.com/tools/perfetto). However instead of
using the command line to record traces you can also do that directly from Perfetto UI or from a device as previously mentioned. It is also said that perfetto traces are more
lightweight than using AS profilers.

Perfetto command line traces needs a config file which uses textproto format. You can use this base configuration provided in [here](https://perfetto.dev/docs/getting-started/system-tracing) 
by the perfetto team `curl -O https://raw.githubusercontent.com/google/perfetto/main/tools/record_android_trace`,  that website is also a guide on how to get started, this will 
download a file with no extension, it is a script. Then run the command below

```
# See python3 record_android_trace --help for more details.
python3 record_android_trace \
   -o trace_file.perfetto-trace
   # This option configure the trace to run for 10s.
   -t 10s \
   # This option configures the main buffer size to be 32MB.
   -b 32mb \
   # This option enables atrace annotations from all apps on the system.
   -a '*' \
   # These options specify some of the most important instrumentation on the
   # device: CPU scheduling/frequency to know what is running on the CPUs and
   # the importance the system placed on that work and atrace annotations to
   # have context on what was happening inside userspace processes (platform
   # and app).
   sched freq view ss input

# Other example I found in a yt video https://youtu.be/phhLFicMacY
phyton3 ./record_android_trace -o starup-trace.perfetto-trace sched freq idle am wm gfx view binder_driver hal dalvik camera input res memory
```

but I ended up with the command below, this one gives me the "Expected Timeline" and "Actual Timeline". BTW, the first command I showed didn't give the frame time info,
with the second command I did get it but it seems like it is adding info I don't need for start time system trace. It seems like some frame info also lives in the `surfaceFlinger`
process which in the first command I didn't get, but dropped frames are only shown in my app process. The given script uses the perfetto comand line tool but it offers very
helpful functionality at development time, it automatically check the connected device to get info like API level, it also offers backwards compatibility in devices with 
Android 10 and lower. it saves the traces in the correct directory in the device, it can stop the trace automatically if you set a time duration, and it launches pefetto UI
automatically which means it pulls the trace file automatically for you. You can configure it further either with a config file or you can pass sort options (only when not 
using `-c/--config`, short options of "Atrace" events are: sched, gfx (frame timing info), am, wm (see --list). Short options of "Ftrace" events are: sched/sched_switch, kmem/kmem (see --list-ftrace),
to see those options run `python3 ./record_android_trace --list`

```
python3 ./record_android_trace -o starup-trace.perfetto-trace -a '*' sched freq idle am wm gfx view binder_driver dalvik input res
```

Perfetto command line tool is useful for creating scripts. The short options I was talking about are sources, they are declared in the configuration file and define what info
we want to collect in a trace. In Perfetto all tracing data sources are idle by default and record data only when instructed to do so. Some data sources are:

* ftrace: for information from the kernel
* atrace: for user-space annotation in services and apps
* heapprofd: for native memory usage information of services and apps

The configurations options are really large as you can see [here](https://perfetto.dev/docs/reference/trace-config-proto). Some useful is the ring buffer, you define the size of the
trace and when it is full it stops.

Reading these traces can be hard if you don't know how the system should behave and also there is a lot of documentation. Some interesting data is "Android App Startup Breakdown" and
look for "Optimization Status", it can show if you're start up time is being JIT compiled or not, if it is JITting too much your start time migh be slow. "HeapTaksDaemon" is the GC
if, it is too bussy collecting garbage your app created, it will drain battery faster. You can also look out for a thread's "running" state which means that the thread is ready but
is waiting for the CPU scheduler to schedule work on that thread, and it could be because the thread has low priority. You can also create a custom track, first select the duration of
time, then go to the "slices" option in the bottom panel, there is an arrow when you hover a line, click it, and now you have an option on the top right corner of the bottom pannel
that says "add debug track"/"show dedug track", create your track there. [Here](https://perfetto.dev/docs/getting-started/cpu-profiling) is how you can do method sampling and from 
there you can see flame graphs. WorkManager owns its own thread and you can see enque work in that thread. The actual timeline shows if a frame was missed or rendered on time or 
after it was expected, red color means a frame took longer than expected (jank), light green means the frame had enough time to be produced but they were produced too late, dark green
means it was rendered on time and without delays.

If you want to know the app start up look for the "Android App Startups" track/slice/bar metric. Beware that it represents the time to initial display, even if you're using 
`reportFullyDrawn()`. To identify the time to full display, search for `reportFullyDrawn()` in the Perfetto search box.

To find the main thread, find the row with your app's package name and expand it. The two rows with the same name as the package (usually the first two rows in the section) represent 
the main thread. Of the two main thread rows, the first represents CPU state and the second row represents tracepoints.

Now check the time spent in OpenDexFilesFromOat*; in the trace, it happens at the same time as the bindApplication slice. This slice represents the time taken to read the DEX files of 
the application. To reduce the time spent in the OpenDexFilesFromOat* state, use R8 minification to reduce the amount of code that needs to be converted to DEX files. Make sure that the 
app doesn't make unnecessary binder transactions during startup, since they increase the risk of CPU contention. If you have to make binder transactions, make sure they don't take longer 
than your device's Vsync refresh rate. If you have to make binder transactions, make sure they don't take longer than your device's Vsync refresh rate. The CPU profiler in Android 
Studio can show you your app's activity with respect to the device's Vsync rate.

To know how a binder transaction is being prioritized, click the binder transaction slice of interest. go to the **Current Selectio**n panel and click** binder reply** under the 
Following threads section. The **Thread** field also tells you the thread that the binder reply occurs on if you want to navigate there manually. To see how the system server is 
handling this binder transaction you will have to look in the CPUs. Find the system processes that handle the binder reply by finding the slices that include the binder reply 
thread name, for example "Binder:687_11 [2542]". Click the relevant system processes to get more information about the binder transaction. Take a look at this system server 
associated with the binder transaction of interest. **End State** says **Runnable (Preempted)**, which means that the process is getting delayed because the CPU is doing something 
else. To find out why, expand the **Ftrace Events** track. In the **Ftrace Events** tab that becomes available, scroll through and look for events related to the binder thread of 
interest **"Binder:687_11 [2542]"**

Learn from [this](https://developer.android.com/topic/performance/appstartup/case-study-gmail-wear) start up performance debuging example.

https://perfetto.dev/docs/analysis/trace-processor
https://perfetto.dev/docs/tracing-101
https://perfetto.dev/docs/getting-started/system-tracing
https://perfetto.dev/docs/analysis/stdlib-docs
https://perfetto.dev/docs/getting-started/android-trace-analysis

## [Tracing in Compose](https://developer.android.com/develop/ui/compose/tooling/tracing)
By default, system traces do not include individual composable functions because system tracing only tracks areas specifically marked for tracing, these traces are great for seeing
how long particular sections of your code are taking to run and at a low overhead cost. However, composable function calls are available in method traces as method traces tracks
every function call in my app but doing this affects the performance of your app. Composition tracing shows composable functions inside system traces, they gives you the low 
intrusiveness from system tracing, with method tracing levels of detail in composition.

Just add this artifact, if you use the compose bom just add `implementation("androidx.compose.runtime:runtime-tracing")`. With this dependency, when you take a system trace that 
includes recomposition, you can see the composable functions automatically. Double-clicking on a composable in the chart takes you to its source code. There is an APK size increase 
for Compose apps coming from tracing strings embedded in the APK by the Compose compiler but they can be removed in your production build by adding the following Proguard rule:

```
-assumenosideeffects public class androidx.compose.runtime.ComposerKt {
   boolean isTraceInProgress();
   void traceEventStart(int,int,int,java.lang.String);
   void traceEventStart(int,java.lang.String);
   void traceEventEnd();
}
```

Note that keeping the functions in, while incurring some APK size cost, ensures that the APK being profiled is the same one that the app users run.

It is possible to capture a composition trace from terminal. To do so, you have to perform the steps that Android Studio normally does for you automatically. First, add the 
additional dependencies to your app.

```
implementation("androidx.tracing:tracing-perfetto:1.0.0")
implementation("androidx.tracing:tracing-perfetto-binary:1.0.0")
```

Don't ship these libs with your production app as it has a large effect on your app size. Start a trace with perfetto with the below configuration. The important part is 
`track_event` data source

```
buffers: {
    size_kb: 63488
    fill_policy: RING_BUFFER
}
buffers: {
    size_kb: 2048
    fill_policy: RING_BUFFER
}
data_sources: {
    config {
        name: "track_event"
    }
}
duration_ms: 10000
flush_period_ms: 30000
incremental_state_config {
    clear_period_ms: 5000
}
```

Launch the app and enable tracing with this command

```
# set app package variable, e.g. com.google.samples.apps.nowinandroid.debug
# can be found through `adb shell ps -ef` or `adb shell cmd package list packages`
package=<your app process>

# issue a broadcast to enable tracing
adb shell am broadcast \
-a androidx.tracing.perfetto.action.ENABLE_TRACING \
$package/androidx.tracing.perfetto.TracingReceiver
```

You can also enable compose tracing in Macrobenchmark test, just add the same last two artifacts I mentioned and add this `androidx.benchmark.fullTracing.enable=true`
instrumentation argument. You can see [here](https://developer.android.com/topic/performance/benchmarking/macrobenchmark-instrumentation-args#fulltracing) to see how
you can add this argument through Gradle, or through the run configuration, or from the command line with the task `./gradlew :benchmark:connectedAndroidTes` or even
if you're running it in a CI pipeline

You can also add a recomposition trace which which adds the composable functions from composition tracing, and also records state reads and writes that cause composable 
functions to recompose to the trace. This helps you find which state change triggered a recomposition. Recording both in a single pass have a high pergormance overhead 
so use them for debugging, not for measuring performance. Just copy the [record_recomposition_trace.py](https://github.com/android/performance-samples/tree/main/RecompositionTracing)
and execute this command `./record_recomposition_trace.py -p <your app package>`

If you need information of the layout or drawing you can add a `trace` block, in the layout phase you can do it like this, just add the layout modifier to any composable
that you want to track the layout phase for like in the below code. The below code will tell you how long it took to measure all children of the composable you add it to.
If you want to knwo how long it took to place the children you can also wrap that call.

```
Modifier.layout { measurable, constraints ->
	trace("MyComposable:measure") {
		val placeable = measurable.measure(constraitns)
		layout(placeable.width, placeable.height) {
			placeable.place(IntOffset.Zero)
		}
	}
}
```

https://developer.android.com/develop/ui/compose/tooling/tracing
https://developer.android.com/develop/ui/compose/performance

## Profiling Methods
As we already know, we can do manual profiling with method tracing using profilers, and is also posible to record system traces directly on a physical device, those are manual 
aproaches to recording profiles. Automated and instrumented ways of recording profiles is using Macrobenchmark (system traces) and starting method tracing with 
`Debug.startMethodTracing`, we can enhance those by adding trace points also. But sometimes there is difficult to debug errors in production, and we have different options for
this, like `Crashalitycs`, which can gives us a system trace (it seems like it uses `ApplicationExitInfo ` under the hood, you also have `ApplicationStartInfo`), it can also
provide us a heap dump (it uses `ProfilingManager ` under the hood). But we have `ProfilingManager` to collect profiles in production, it helps us debug rare issues in 
production, it helps us collect data from many users to analyze it. Compared to manual profile collection, profiles collected with this manager offer more timing control
because they can be based on events or just on demand at specific points, you can use them locally as well as to collect in the field profiles, so they are more scalable,
however less customization. They are very useful because you can collect a profile even if you're not able to reproduce a bug locally, you can find and fix performnce
issue using data collected in the field. Data from other apps is removed because by redacting the profiles before returning the information so they protect user's privacy,
therefoe, they are less complete than manual locally collected profiles.

## Improve Performance
* Stay off the main thread, you can guarantee using strict mode
  ```
  if (debug) {
  	StrictMode.setThreadPolicy(
  		StrictMode.ThreadPolicy.Builder()
  			.detectAll()
  			.penaltyLog()
  			.build() 
  	)
  }
  ```
* Since system can kill the app in low end devices, always use creation extras in VM, use `SavedStateHandle`, in activities and fragments use `savedInstanceState` in the
  `onSaveInstanceState` and `onCreate` methods. In compose use `rememberSaveable` or `rememberSerializable`.

* Avoid wake locks, there is partial and full wake locks, the former only avoid the CPU from sleeping and the former also avoids the from UI sleeping, when devices sleep they
  enter in a low-power state which makes sures that the CPU is not doing too much work, in android Doze is a power saving mode state when the cpu is sleeping/idle. Wakelocks
  provide a gate for other processes to continue consuming CPU also so it ends up cause battery drain. There are two ways to acquire a wake lock, manually by using
  `PowerManager` (often used with a foreground service). Avoid manual `WakeLock` management; the other way of acquiring a wake lock is indirectly/automatically by using APIs
  such as `WorkManager` for background tasks to keep the CPU running while the device screen is off, if not used correctly `WorkManager` can tirgger the excessive partial wakelocks
  metric in android vitals. In [this video](https://youtu.be/xMylnxek5a4?si=pahT767ogy7_0Oc3)(27:27) we are told that google play considers partial wake locks excesive when all of
  the wake locks accumulated while running in the background run for three or more hours in a 24-hour period for more than 5% of total app sessions. There are valid reasons to
  acquire a wake lock such as, to complete a user-initiated action such as downloading a large file. Previously you would use background services to schedule a periodic sync in
  the background to download fresh conent for offline viewing but now you should use APIs like `JobScheduler` or event better `WorkManager` (they acquire wake locks on your behalf).
  For playing audio in the background you don't need a manual wake lock because the system automatically acquires a wake lock (these wake locks are currently excempt from the
  excesive wake lock calculation in app vitals). For communicating with an external device via Bluetooth you may need manual wake locks if you need communication while the screen
  is off but you can also try using `WorkManager`. For tracking location APIs you don't need manual wakelocks as when location events are received in `LocationManager` a brief wake
  lock is held to alert the device. Check [oficial documentation](https://developer.android.com/develop/background-work/background-tasks/awake/wakelock) for more. To debug wake locks
  you need a debuggable instance of the app, go to android studio "VIew > Tool Windows > App inspection" and click on "Background Task Inspecto" tab, here you can also inspect database
  and newtork. If you have multiple APIs acquiring wake locks and you excesive usage is reported in vital then use perfetto to debug issues, you can collect system traces manually
  over a long period of time, you would be interested in looking for the "Device State" section, in that section look for "Top App", "Long Wakelocks", "Foreground Apps" and "Jobs,
  and pin them, you will be able to see the number of long wakelocks that occurred, if you're expecting to see some wakelocks like location wakelocks but you're not seeing it in the
  tracks I just mentioned it is probably because those are short, they can be quite often but they are not long, so you can search in perfetto top search input with something like
  this "\*location\*" (include the stars) and they probably will be in the "Wakelock" track

* Get off the main thread asap, you might want to have a thread that is created with high priority that runs in parallel to the main thread and you can use that custom thread to run
  high priority/important tasks, you wouldn't want to run high priority tasks on a low priority background thread because you could have a situation where you priority inversion, where
  the main thread is waiting on a low priority thread so that is why you would want this parallel high priority thread

In order to understand the impact of performance changes/improvements you can do local tracing (inspact), bencharking (after doing changed meassure improvements), and 
take in field metrics (monitoring) so we can know when we need to improve.

## [Performance Monitoring](https://youtu.be/GiBu21pP9I0?si=L4A9BnFe_O5DMcMa)
For performance monitoring in the field you can use "Android Vitals" available in the play console. Use Firebase Performance Monitoring, it can collect performance
info about specific fucntions with the annoation `@AddTrace(name, enable)`, usingn its gradle plugin you can get network request durations report in firebase console. 
even crashlytics can help debug OOM errors. Use the "JankStats" library `androidx.metrics:metrics-performance`

You can use Firebase Test Lab in your CI pipeline to run benchmark tests, they have a scripting interface you can use to run bencharmks on every build. On every commit 
that lands to your release branch or before it is merged onto the main branch your CI pipeline can run your benchmark suite, this way you can compare between releases 
and catch performance regressions if metrics rise above a well defined threshold before they land to production. To automate reporting you need to set thresholds for 
every important metric to you and then compare it to a previous benchmark. Google recommends to not compare a build against another build, instead take a group of builds 
before the changes land and then compare to another group of builds taken after the changes have been landed to the codebase. So the steps would be

* Write Macrobenchmarks
* Run on physical devices
* Collect Metrics
* Store benchmark results for processing
* Run step fitting algorithm in CI to detect regressions

When Creating the pipeline that cna do the step fitting alogrithm look [this article](https://medium.com/androiddevelopers/fighting-regressions-with-benchmarks-in-ci-6ea9a14b5c71)

You can also collect data in the field with `ProfilingManager`, `ApplicationStartInfo`, and `ApplicationExitInfo`. `ApplicationStartInfo` can show you the reason why an app started.
`ApplicationExitInfo` can give info about crashes and ANRs. You can see a demo of how to use `ApplicationExitInfo` in [this video](https://youtu.be/xMylnxek5a4?si=vJvtOO7z2O9vFOvx)(40:00).

```
class AppExitLogger(private val context: Context) {
	@RequiresApi(Build.VERSION_CODES.R)
	fun logAppExitInfo() {
		val activityManager = context.getSystemService(Context.ACTIVITY_SERVICE) as ActivityManager
		val exitReasons = activityManager.getHistoricalProcessExitReasons(null, 0, 0)

		if (exitReasons.isNotEmpty()) {
			val logEntries = mutableLIstOF<String>()
			val dateFormatter = SimpleDateFormat("yyy-MM-dd HH:mm:ss.SSS", Locale.US)

			for (reason in exitReasons) {
				val timestamp = dateFormatter.format(Date(reason.timestamp))
				val description = reaons.description ?: "No Description"

				val logEntry = """
					Timestamp: $timestamp
					Reason Code: ${getReasonCodeStr(reason.reason)}
					Description: $description
					Importance: ${getProcessImportanceStr(reason.importance) /* consider checking if importance is CHADED state */ }
					Process State Summary: ${reason.processStateSummary}
					Tombstone stream: ${reason.traceInputStream?.converToString() /* usually collected for ARN */ }
					""".trimIndent()

				// Filter reaons to only include ANR
				if (reason.reason == ApplicationExitInfo.REASON_ANR) {
					logEntried.add(logEntry)
				}
			}
		}
	}
}
```

`reason.traceInputStream` will gives us a trace of every single thread at the time of exit, so it is helpful in ARNs. App vitals also gives you some info about ARNs but without
the level of detail you can get by using the exit info but is a good place to start

### [Profiling Manager](https://developer.android.com/topic/performance/tracing/profiling-manager/overview)
`ProfilingManager`, introduced in Android 15, is an API that lets you collect real user Perfetto profiles (system traces and heap dumps) programmatically, it gives you 
two types of profile collection `App-driven` and `Event-driven`, in the former you define the start and the end of the collection process and the latter are automatically collected by the system. As
of 11/3/27 the events it tracks automatically are ANRs, APP_FULLY_DRAWN, KILL_TASK_MANAGER, KILL_RECENTS, KILL_FORCE_STOP, COLD_START, KILL_EXCESIVE_CPU_USAGE, ANOMALY,
OOM (out of memory), with the android 17 restriction on memory usage the ANOMALY trigger is really useful because it identifies performance anomalies detected by the
system, it supports memory and binary spam, if a memory usage exceeds a threshold it creates a heapdump which allows you to use this trigger to examin resouce
allocations and the app state to identify the root cause. If the app is terminated due to violating the android 17 memory usage limit it will provide a heap dump. With
the OOM this manager monitors for out of memory errors, when this occurs a heap dump is created also, so this is more powerful than just a stack trace in crahsaliytics.
This manager lets you register a result listener which will only provide you with the information on the next app start up, and from that listener you send the report
to your servers, then you can use perfetto to inspect the heap dump as shown in [this video](https://youtu.be/fOXJR5qLq54?si=nZ7ufFkzV3UgiXXq). Check perfetto heap profiles

## Benchmark
[This](https://github.com/android/performance-samples) repo contains the samples using the `JankStats` library, Macrobenchmark, Microbrenchmark, and recompositino tracing.
[Compose Hero Benchmarks](https://cs.android.com/androidx/platform/frameworks/support/+/androidx-main:compose/integration-tests/hero/README.md) example, [performance-samples](https://github.com/android/performance-samples) 
contains macrobenchmarks, microbenchmarks, JankStats samples, it also has information on how on how to set up a benchmarks in CI in 
"performance-samples/MacrobenchmarkSample/ftl/README.md"

Both Macro and Micro benchmarks are instrumented JUnit tests however macro usually interacts with the UI using UI Automator or some other library, its most commonly used 
to test UI performance but it can track anything, object allocation time, in theory anything at any scale. Microbenchmakrs where existed first and they where known as just
benchmarks you can still use them, as it name implies you usually use them smaller pieces of code, for example to test how long it takes for a repository to execute a 
function, in theory you could also test a function in your viewmodel, serialization times and similart tasks. Microbenchmarks returns us the following info on the console 
Execution Time in nano seconds of the code being measured, Allocation Counts: Shows the number of object allocations or garbage collection hits if tracking memory allocations 
is enabled and it also generates some JSON files useful for automated CI/CD pipelines for detecting regressions, those files gives you Per-Run Timings which is a detail by 
run and not aggreated as in the console, detailed Metrics which Includes CPU time, real (wall-clock) time, and allocation metrics, and Device Metadata to help contextualize 
the results

### [Macrobenchmark[(https://developer.android.com/topic/performance/benchmarking/benchmarking-overview)
The Macrobenchmark library measures larger end-user interactions, such as startup, interacting with the UI, and animations, it injects events and monitors results externally 
from a test app that is built with your tests. Therefore, when writing the benchmarks, you don't call your app code directly and instead navigate within your app as a user. 
Macrobenchmark and UI automator is the recommended tool for testing UIs created with Jetpack Compose. Jetpack Benchmarks are standard JUnit instrumentation tests that run on 
an Android device, Cold start is `Application.create`, warm start is `Activity.create` like when you open an app after the activity was destroyed but the proces still running 
also config changes, hot start is  `Activity.onStarrt` happens when app is briefly in the background and is moved to the foreground again. Always run these tests in a physical 
device or using "Firebase Test Lab"

These test allows you to meassure startup timming, frame timming, CPU, memory usage, power (they record system traces automatically which you can use to track regressions), and
you can add custom metrics. Since Macrobenchmark can install your app with baseiline profiles you can test using the most similar performance to what your users will see. Unlike 
most Android UI tests, Macrobenchmark tests run in a separate process from the app itself. This is necessary to enable things like stopping the app process and compiling from DEX 
bytecode to machine code.

```
// cusotm metrics shown in https://youtu.be/xMylnxek5a4?si=lpjxJCcreBMvbL6Z 12:50
// https://youtu.be/Z96wfbID_Yc?si=V0zWWy3ytIPNZt9k 20:50
// used to measure how much code is running in interpreted mode, it measures all JITting that occurred during benchmark
// With no baseline profile you will see a larger number, with baseline profile you should see a shorter duration
val jitCompilationMetric = TraceSectionMetric(sectionName = "JIT Compiling %", label = "JIT compilation", Mode.SUM) 

// tracks time spent in class initialization. It should go down when a baseline profile is applied
val classInitMetric = TraceSectionMetric(sectionName = "L%/%;", label = "ClassInit")
```

By tracking JIT you can see how effecting a baseline profile is because baseline profiles remove the need of JIT compilation. High percentages of JIT compilation can cause 
slow rendering and slower startup time.

| | | | | | | | | |
| - | - | - | - | - | - | - | - | - |
| ClassInitCount | min | 7,111 | median | 7114 | max | 7120 | | |
| ClassInitSumMs | min | 94.1 | median | 100.6 | max | 110.7 | | |
| JIT compilationCount | min | 171.0 | median | 255.5 | max | 298.0 | | |
| JIT compilationSumMs | min | 376.6 | median | 490.7 | max | 567.2 | | |
| frameCount | min | 231.0 | median | 291.5 | max | 329.0 | | |
| timeToInitialDisplayMs | min | 359.7 | median | 368.1 | max | 394.2 | | |
| frameDurationCpuMs | P50 | 3.8 | P90 | 6.8 | P95 | 13.1 | P99 | 64.4 |
| frameOverrunMs | P50 | -9.7 | P90 | -4.3 | P95 | 7.4 | P99 | 141.0 |

The results are delivered as a statistical distribution. An interesting part of this benchmark is the inflection point in P90 to P95 in "frameOverrunMs" because it shows 
good numbers replaced by bad numbers, in this metrics a negative number means we are rendering frames earlier than its deadline and a positive number means you missed the 
frame's deadline so they are janky frames. BTW reddit start up time using R8 and profile guided optimizations is 881ms. You can read the "P"s values like for example the 
"P90" means 90% render faster than "this" and the rest (10%) render slower. "frameDurationCpuMs" is the amount of time the frame spent actively being produced on the CPU 
across both the main application UI thread and the Compose RenderThread. When optimizing Jetpack Compose layout hierarchies, look at your worst-performing frames and If 
"frameOverrunMs" spikes into positive integers at the high percentiles, it indicates that recompositions are stalling the main thread during heavy scroll 
animations. Always focus on median values, since they provide the best estimate of typical user startup times.

It is important that you call `reportFullyDrawn()` or `ReportDrawn()`, or even newer versions like `ReportDrawnWhen` (don't worry if it is called multiple times, android 
handles it for you so you can add it as a call in any composable's body). There is a suspending function called `ReportDrawnAfter` where you can call a suspeding function 
from. Reporting this to the system Allows Benchmarks to meassure TTFD. And optimzie Baseline Profiles, you can call it as many times as needed in case you have asynchronous 
parts of your home screen that load separately, you can even wait for content to be loaded from the network

You need to choose the `startupMode` parameter, you can choose between `StartupMode.COLD` for start up benchmarks, this will kill the app's process between the 
`setupBlock()` and `meassureBlock` and the app restarts in each iteration of the test. `StartupMode.WARN` useful for frame timming benchmarks or cached startup benchmarks, 
in here the process is created before the test runs and is not killed between iterations, it also clears the activities before iteration, is like running the `onStart` 
method in an activity, in these tests you usually want to run some operations before the benchmark test starts and the app is not killed between the setup and the test. 
`StartupMode.HOT` could be useful for some per-activity caching mechanisms, the app's process and the previously-running activity won't be restarted so is like running the 
`onResume` method of an activity. You can also pass `null` and handle the process lifecycle yourself. There is also an optional `compilationMode` parameter, you can choose 
between: `Partial` (`CompilationMode.DEFAULT`), is the default value, is used for understanding initial performance, it uses information from Baseline Profile or 
warmupIterations to pre-compile your app, meaning that if a baseline profile exists it will precompile the classes and methods listed in the profile so it is useful when
you want to know the performance improvements delivered by the base line profile which means this is similar to a regular app installation, so you should compare it against 
a `none` compilation mode. `Full`, useful when you're in the middle of finding and improving performance and you want to compare runtime improvements, it 
removes the number of factors contributing to performance variance (JIT) so you can focus on the improvements delivered by changes you have made, but the startup might be 
slower than partial due to bigger OAT file, remember that loading the whole pre-compiled app from disk might take longer. `None` used for comparing Baseline Profiles, it 
doesn't use any baseline profiles even the ones coming from libraries, it basically disables all precompilation and therefore any existing baseline profile is disabled 
also, this is the only way to compare base line profiles in a benchmark. In Android versions 5 and 6 apps used to be fully compiled which can cause slow start ups because
compiled code has a bigger footprint on storage and therefore reading all that code from disk needed a lot of I/O

In frame metric benchmarks always set the margin with similar code to below
```
val feed = device.findObject(By.res("feed"))
feed.setGestrueMargin(device.displayWidth/3)
feed.fling(Direction.DOWN) // this doesn't scroll the same distance everytime
feed.drag(Point(feed.visibleCenterX, 0)) // use this to get consistent scrolling
```

Traces from the benchmark are store at the following URI: "$Project/benchmark/build/outputs/connected_android_test+additional_output/build_variant_name/connected/$Device/$TestName.trace", 
if you want to keep the results, make sure to copy them if you need to use then for later.

You can measure any custom trace section, for example I mentioned how to add a custom trace section in [compose](#tracing-in-compose), using `TraceSectionMetric()`, it 
measures a section by using its name. It has two modes, `Mode.First` for measuring the first occurence only and `Mode.Sum` for combining timing information of section with 
the same name together. You can use wildcards in the section name. 

```
PowerMetric(PowerMetric.Type.Power(
	mapOf(
		PowerCategory.CPU to PowerCategoryDisplayLevel.TOTAL,
		PowerCategory.DISPLAY to PowerCategoryDisplayLevel.TOTAL,
		PowerCategory.GPU to PowerCategoryDisplayLevel.TOTAL,
		PowerCategory.NETWORK to PowerCategoryDisplayLevel.TOTAL,
	)
))

TraceSectionMetric("MyComposable", Mode.sum) 
TraceSectionMetric("MyComposable:measure", Mode.Sum)
TraceSectionMetric("%jetsnack.HighlightedSnackItem%") TraceSectionMetric("%myPackage.MyComposable%") // finds all section names produces by composition tracing

// This trace section takes into account the SQL wildcard character %,
// which can find trace sections without the full name.
// This way, you can measure composables produced by the composition tracing
// and measure how long they took and how many times they recomposed.
// WARNING: This metric only shows results when running with composition tracing, otherwise it won't be visible in the outputs.
TraceSectionMetric("%EntryRow%", TraceSectionMetric.Mode.Sum)
``` 

See [this video](https://youtu.be/Z96wfbID_Yc?si=siHG_R-8tBl0Fg8C)(17:48) to see how to read the results

#### Writting a Benchmark
1. You almost always would like to use the android studio option to create a benchmark module, this add a dedicated Gradle module just for benchmarking, this module
   measures the app built by an app module, the built app is also referred as the "target of the macrobenchmark"

3. The target app module needs to add the `ProfileInstaller` library which Macrobenchmark needs to enable profile capture and other things like restarting the app, etc.

4. The benchmarked version of the app has to be as close as possible to the release version(no debuggable and optimized with R8), you can copy relase version
   configurations like this

   ```
   create("benchmark") {
        initWith(getByName("release"))
        signingConfig = signingConfigs.getByName("debug")
    }
   ```
   
6. If you have a multimodular app set the build variant you want to compile by declaring it in the `benchmark` build type configurations of the `:app` and
   `:macrobenchmark` modules with this line ` matchingFallbacks += listOf("release")` this means that when you run the benchmark you need to select the `benchmark`
   build type in the `:app` and `:macrobenchmark` modules and the `release` build type in all other modules

8. If you have multiple build flavors then add the same flavors in your `:macrobenchmark` module so you can build and benchmark different flavors. 

9. To make sure that the benchmark, both, builds and tests the correct variant of your app make sure you select the benchmark variant of both the app and the
   Macrobenchmark module in the Build Variants panel and the proper variant in other modules which you declared using `matchingFallbacks`,
   [This](https://github.com/android/performance-samples/tree/main/MacrobenchmarkSample/macrobenchmark) is a sample of a Macrobenchmark module.

11. For running the benchmarks use Android 14 (API level 34) or later to persist state when benchmarking. The Macrobenchmark library fully resets the compilation state
    for each compile, which on Android versions earlier than 14 requires reinstalling the APK. As a workaround, control app compilation separately and skip compilation
    using CompilationMode.Ignore.

13. To run all benchmarks from command line  use `./gradlew :macrobenchmark:connectedCheck` or a single test use `./gradlew :macrobenchmark:connectedCheck -P android.testInstrumentationRunnerArguments.class=com.example.macrobenchmark.startup.SampleStartupBenchmark#startup`

14. If you want to use the resutls after a successful benchmark run for your CI pipeline, metrics are displayed directly in Android Studio and are output for CI usage in
    a JSON file. JSON reports and any profiling traces are automatically copied from the device to the host. These are written on the host machine in the following
    location: `project_root/module/build/outputs/connected_android_test_additional_output/debugAndroidTest/connected/device_id/`

16. Macrobenchmarks can specify a `CompilationMode`, which defines how much of the app must be pre-compiled. The defualt mode is `CompilationMode.DEFAULT`, which installs
    a Baseline Profile—if you already generated and copied it—on Android 7 (API level 24) and later. The Baseline Profile will be installed only if the target app contains
    both a Baseline Profile and the `ProfileInstaller` library. If you want to control the compilation yourself you need to pass `CompilationMode.Ignore` and control the
    JIT manually using the command shown [here](https://source.android.com/docs/core/runtime/jit-compiler#turn-on-jit-logging) using `adb`

18. Your benchmark doesn't have to define UI interctions using UI Automator. Instead, it can run an animation, for example. It also doesn't need to use UI Automator
    specifically. It collects performance metrics as long as frames are being produced. The benchmark can us something different to UI Automator but UI Automator may
    be preffered.

Configure the behavior of the library with the following instrumentation arguments. You can either add these to your Gradle configuration or apply them directly when 
running instrumentation from the command line. To set these arguments for all Android Studio and command line test runs, add them to testInstrumentationRunnerArguments:

```
android {
    defaultConfig {
        // ...
        testInstrumentationRunnerArguments["androidx.benchmark.dryRunMode.enable"] = "true"
    }
}
```

If you're running the macrobenchmark from the command line, use `-P android.testInstrumentationRunnerArguments.[name of the argument]`: `adb shell am instrument -e androidx.benchmark.enabledRules BaselineProfile -w com.example.macrobenchmark/androidx.test.runner.AndroidJUnitRunner`

If you're invoking the am instrument command directly (which may be the case in CI testing environments), pass the argument to am instrument with `-e`:
`adb shell am instrument -e androidx.benchmark.enabledRules BaselineProfile -w com.example.macrobenchmark/androidx.test.runner.AndroidJUnitRunner`

For all the arguments available see [here](https://developer.android.com/topic/performance/benchmarking/macrobenchmark-instrumentation-args)

##### [Metrics](https://developer.android.com/topic/performance/benchmarking/macrobenchmark-metrics)
`PowerMetric` is a little different that the other metrics, it captures the change in power or energy over the duration of your Macrobenchmark run. Each 
selected category is broken down into its measurable hardware components, while unselected categories are grouped into an "unselected" bucket. It requires 
some spceidif hardware, these metrics measure system-wide consumption rather than per-app calculations. Consequently, data collection is limited to physical 
Google Pixel 6, Pixel 6 Pro, and newer physical devices.


#### App Startup Insights
They enhance benchmark results by providing you with detail info on issues that occurred while benchmarking. These insights can alert you if there is issues 
with blocking operations, lock conentions, installation time, DEX processing, application binding, JIT compilation, resource loading, high number of broadcasts. 
Add it to your project with `androidx.benchmark:benchmark-traceprocessor` and add it to a test benchmark like this

```
benchmarRule.measureRepeated(experimentConfig = ExperimentalConfig(StartupInsightsConfig(true))) { // your benchmark }
```

### [Microbenchmark](https://developer.android.com/topic/performance/benchmarking/microbenchmark-overview)
These are great for everything that is CPU-bound or processing a lot of data, so you can meassure the CPU of the code you execute. It can also show why the operations 
are slow by showing what is happening while they run, such as running on a low-priority thread, sleeping due to disk access, or unexpectedly calling into an expensive 
function, like bitmap decoding.

Microbenchmarks are most useful for CPU work that is run many times in your app, also known as hot code paths. Good examples are RecyclerView scrolling with one item 
shown at a time, data conversions or processing, and other pieces of code that get used repeatedly.

Because benchmarks run in a loop, any code that isn't run frequently or performs differently when called multiple times might not be a good fit for benchmarking.

### UI Automator
It is used in benchmark to define and perform interactions with your app. Previously you had to explictly wait if a screen is loading but now it waits 10S 
automatically

```
// start app
startApp()

// Click a button
onElement { textAsString() == "Search" }.click()

// scoll elelment
onElement { isScrollable }.fling(Direction.DOWN)

onElement { isEditable && contentDescription == "Prompt" }.text = "some text"

onElement { id == "Parent" }.
	onElement { id == "Child" }.
	onElement { id == "Grandchild" }
	.click()

// 3. Wait until the target screen settles and is fully rendered
waitForStableInActiveWindow()
```

You can enable `testTagAsResourceId` to interact with Compose modifiers. To allow UI Automator to find your Compose elements, enable `testTagAsResourceId = true` on 
the semantics modifier of your top-level Compose element. Find the Composable using its `testTag` mapped as a `viewIdResourceName` like this `onElement { viewIdResourceName == "my_lazy_column" }`

### Benchmarks in CI
[Here](https://developer.android.com/topic/performance/benchmarking/benchmarking-in-ci) is more info of how to set this. The idea when I implement this is to do it using a 
step fitting algorithm, as described in [this video](https://youtu.be/ynBPcFs6OOk), the resources I can use for this is [this](https://medium.com/androiddevelopers/fighting-regressions-with-benchmarks-in-ci-6ea9a14b5c71) 
article which also points to the actual set fitting algorithm google uses written in go. Also use [this](https://github.com/android/performance-samples/tree/main/MacrobenchmarkSample/ftl) 
document that describes how to set up benchmarks using github actions and firebase test lab

## Measure Performance
Usually you wouldn't want users to report performance issues, so here is a list of things you can look out for make sure the user experience is not affected by performance
issues

* App startup: Basically the main thread is doing some IO to read your application from storage and load it to ram, so starting an app is quite expenive. Try to make cold
  starts take 500ms or less. Aim to keep warm starts under 200ms and hot starts under 150ms. P95 and P99 latencies very close to the median latency. Try to avoid Interprocess
  communications (IPCs, Tip: You can use `am trace-ipc start` to get more information about these calls. Disable it before resuming benchmarking, because it has significant
  overhead and otherwise persists until device restart.) and unnecessary I/O during during startup as it can introduce lock contention problems (when different threads, processes
  or db queries try to access the same resources at same time)
* Avoid visual Janks, specially common in lazy list or complex screens. Spot them using a physical device using **Developer Options > Show refresh rate **in the **Debugging**
  section.
* Animations, navigating screens, transitions that are not running smoothly.
* Performance in long running tasks and important and high traffic flows.
* 

## Baseline Profiles
A baseline profile is just a list of classes and methods with annotations that are ahead-or-time compiled by the system at installation time. When generating a Baseli Profile 
the app should not be obfuscated because we need the actual namess (do this using proguard `-dontobfuscate`, you should create a `benchmark` build type in the app module
as indicated in the [benchmark](#benchmark) section in this document and create a proguard file only for the mentioned rule and add it to that build type only), the benchmark
build type in the app module should can be declared as in the below code.

```
val macrobenchmark by creating {
	initWith(release)
	signingConfig = signingConfig.getByName("debug)
	matchingFallbacks += listOf("release")
	isDebuggable = false
	proguardFiles("baseline-profiles-rules.pro")
}
```

When you write the benchmark that defines the baseline profile you have to define the interactions you are interested in, the interactions defined in the test body will be ran
several times, the info of classes and methods than run while the benchmark is in progress will be collected. Since baseline profiles do not measure performance they can run
on an emulators. The device you use for running your profiles needs to have root access because the profile is saved in a system folder that is not accessible for the app you
need to run these tests in a rooted device or just an emulator (an emulator without play services can be considered an effectively rooted device) because we are not meassuring
performance, instead we are just indexing classes and method calls, therefore it is ok to use an emulator. You can switch an emulator to root access with the command `adb root`
and run the test manually, however you could use "Grade Managed Devices", this is a AGP feature which lets you configure an emulator in your build script. Gradle enables you to
run instrumentation tests without the need to manually handle the emulator they run on, making builds more reproducible, AGP will automatically download the emulator image
if needed, start emulator up, run the tests you specify, copy the resutls to the host machine, tear down the emulator which clears the device state for next use. To declare a
managed device add the following configurations to the `android` block in your benchmark module build script

```
testOptions {
	managedDevices {
		create(name = "pixel2Api31", ManagedVirtualDevice::class) {
			device = "Pixel 2"
			apiLevel = 31
			systemImageSource = "AOSP" // AOSP images has root access but doesn't come with Google Play, You can get an image that comes with google play but it won't have root access
		}
	}
}
```

You run the tests using the following command `./gradlew :benchmark:pixel2Api31NameOfBuildVariantAndroidTest`, for example `./gradlew :benchmark:pixel2Api31BenchmarkAndroidTest`,
this will run all test in the benchmark module, if you only want to run the test that generates the baseline profile do 
`./gradlew :benchmark:pixel2Api31NameOfBuildVariantAndroidTest -P android.testInstrumentationArguments.androidx.benchmark.enableRules=BaselineProfile`. Once the test runs the profile
is create in the benchmark module in the URI `build/outputs/managed_device_android_test_additional_output/pixel2Api31` you need to copy the profile into you app module in the
`src/main` folder right next to the `AndroidManifest` and rename it to `baseline-prof.txt `, now you need to add the profile installer dependency to your app module 
`"androidx.profileinstaller:profileinstaller "`, this library allows benchmarks to pick up the compiled baseline profile locally for benchmarking but it also enables the benefits
of baseline profiles on older android platform versions and even on devices where google play services are not available.

If you want to measure performance improvements delivered by installing a baseline profile in the app you can use Macrobenchmarks, in the compilation mode use `CompilationMode.DEFAULT1`
which is `Partial` compilation, this mode will try to apply an existing baseline profile if it exists which means the classes and methods defined in the profile will be pre-compiled
when running the test. Compare `Partial` compilation mode against `None` because it runs the test without pre-compiling any code, meaning the baseline profiles are not applied, 
this way you are comparing a situation where you have base line profiles against a build where base line profiles are not applied so you can know what performance improvements you're
getting from baseline profiles, but remember to run benchmarks on a physical device.

You can measure Macrobenchmark Baseline Profiles improvements in your app using Macrobenchmark since you can start your app in the test using different compilation modes, so you
can see what is the start up time with no compilation and compare it to the start up time using pre compilation, and you can even compare again full AOT compilation which should
be even slower because that fully precompile code means your app needs to read more code from storage making the startup time slower. With no precompile code the JIT threadpool 
in a systrace will be doing more work than with precompile code and for partial precompile you'll see some work there.

To get a baseline profile for app start up that is behind a login wall you have at least two options, you can either use the `UIAutomator` to navigate through your app by actually 
typing login info of a test account or an even more advance way to do this is to have a different variant of the app that has an additional broadcast receiver which will receive
information from the benchmark with a username and password or to initialize with a data file.

You can generate baseline profiles from a CI pipeline, first write the tests that generate baseline profiles, then on the CI pipeline you can use "Gradle Managed Devices" to run
the tests on an emulator, then the pipeline needs to copy the generated profile into `source/main` folder and then build the app with the profile, this means that you first need
to build the benchmark variant that generates the profile but then you build the release version and optionally you can copy the profile as a commit to your version control so
you can use it to build the next release if its needed

Meassuring performance improvements delivered by  baseline profiles in production can be done with the tools I mentioned, Android vitals, Firebase performance monitor. and for
start up profiles you can query start up time using `ApplicationStartInfo`. You can also measure baseline profiles improvements in the field using profile verifiers to confirm 
profile compilation has succeeded. You can also roll out two different APKs in the playstore but is a little difficult to do so.

As explained before, what you get by creating baseline profiles is some text files that can be easily read, these are a list of classes and methods that profile recorded, you then 
include this list when building the release bundle, when app is installed in user's device the OS uses that list of classes and methods to compile them. You can also get a nice
insight of what classes the app uses at startup or at whatever time the benchmark runs, you could use this info to do some kind of debugging or improvements by identifying code
that shouldn't run or can run latter.

These performance enhancements directly result in improved business metrics such as user retention, transactions, and ratings.

When capturing a Baseline Profile with a test, your app must not be obfuscated. If you aren't using the Baseline Profile Gradle plugin, you should also make sure that `-dontobfuscate` 
and `-dontoptimize` are applied. The Baseline Profile Gradle Plugin automatically handles this configuration for you. In your release builds R8 automatically rewrites the rules from 
your unobfuscated profile files to match the obfuscated and optimized code in your release APK. The build takes advantage of the unobfuscated text file by transforming the rules 
correctly. If you use an advanced, non-Gradle workflow such as custom CI automation pipelines to generate your profiles, you must still follow the same principles. However, when you 
build your release app, you must obfuscate it. R8 processes the unobfuscated text rules file and correctly transforms the rules to apply to the obfuscated release app.

These dependencies and their minimum version are required at different times and work together as a toolchain to enable an optimal Baseline Profile.
* Android Gradle plugin: `com.android.tools.build:8.0.0`
* Macrobenchmark library: `androidx.benchmark:benchmark-macro-junit4:1.5.0`
* Profile Installer: `androidx.profileinstaller:profileinstaller:1.4.1`

Functinallities and capabilities when gnerating a baseline profile with the aid ofAGP have changed over time. It seems like the baseline profile Gradle plugin was added on AGP version
8.0, it seems like the baseline profiles plugin automated the capability of creating/using multiple Baseline Profile source files and created them in variant-aware directories such as
`src/free/generated/baselineProfiles/baseline-prof1.txt`, I'm still not sure if they mean I can include more than one baseline profile text file or if they mean that the capability of
creating multiple Baseline Profiles like one in one variant and another one in another variant and if I create one in a variant source set what happens to profile file created in the
main one. In AGP version 8.2 D8 and R8 can transform the human-readable Baseline and Startup Profile rules to fully capture all the rules you need to optimize app performance. 
So from here we were now able** generate profiles from an unminified build and apply them to a minified release build**. Increases Baseline Profile coverage of methods by ~30% and 
increases app performance by ~15%. In AGP 8.3 we where now able to declare variant-aware Baseline Profile files in library modules also, previously this was only posible in the app
module only. In AGP 8.4 **Local app installations of non-debuggable builds using the Gradle wrapper command line tool or Android Studio install Baseline Profiles**, so the performance of 
your local release build more closely matches production. This update doesn't affect production performance of Baseline Profiles. In AGP 9.1 In addition to variant-aware directories, 
you can declare multiple Baseline Profile source files with an arbitrary name, such as `src/free/generated/baselineProfiles/baseline-prof1.txt`, for library modules as well as app modules.

In my setup with the latests verstions as of 11/19/26 I can place Baseline Profile rules in a dedicated source set directory and enabling multiple files. I'm not constrained to a single,
fixed path profile. This means I can define distinct Baseline Profiles tailored to specific build flavors and types (for example, using directories like `src/variant/baselineProfiles/`),
which makes sure performance optimization rules are precisely applied for each unique application or library binary. 

As mentioned before, you should use the Baseline Profile Gradle Plugin to define and produce profile files. This plugin hooks into the build process, and AGP compiles these 
human-readable profile rules into a binary format that you can find the packaged in an APK or AAB in `assets/dexopt/baseline.prof`, ART then uses the profile in the binary format to do
on-device compilation provided that the profile is smaller than 1.5 MB.

Play Store "internal app sharing" doesn't support Baseline Profiles; however, the "internal testing track" does.

## Startup Profiles
Is another form of profile guided optimization which takes the most important code for users interaction and allows the system to precompile it at installation time, it is loaded
separately from the other app's code making startup time even faster. Start up profiles guide R8 to be able to perform optimization through R8. For example, R8 could inline code	
that actually only runs after start up into the start up path but when R8 has start up profiles it can avoid this "optimizations" that actually could regress start up time because 
if R8 moves more code into start up path then more code needs to be loaded at start up. These profiles trade application size for application performance

They remove the need for JIT compile the code at start up (baseline profiles also do this but this is more focused on start up as described above) and makes it faster because
a lot of JIT can cause slow rendering and startup performance.

It is important that you call `reportFullyDrawn()` or `ReportDrawn()`, or even newer versions like `ReportDrawnWhen` (don't worry if it is called multiple times, android handles it 
for you so you can add it as a call in any composable's body). There is a suspending function called `ReportDrawnAfter` where you can call a suspeding function from. Rerporting this 
to the system Allows Benchmarks to create a more precise baseline profile

Beware that starting `WorkManager` is resource heavy, so starting it during startup might not be the best for performance, the solution to this is adding a proxy in front of 
`workManager` so it doesn't get executed during startup, it could be implemented by creating your own API, also direct calls to `WorkManager` should be forbiden and instead you 
should call your own API exclusively. After all startup is done your API should start `WorkManager` automatically. You could get some ideas from [this article](https://medium.com/@ahmed.ally2/customizing-workmanager-fundamentals-ba81fe430ec8)

Startup profiles are similar to Baseline Profiles, but they are used at compile time to optimize DEX layout for faster startup times, rather than for on-device optimization.

## [Start Profiles vs Baseline Profiles](https://developer.android.com/topic/performance/baselineprofiles/overview#compare-baseline-startup)
The human readable version of the former is usually named `startup-prof.txt` and the latter `baseline-prof.txt`. While their contents might sometimes appear similar, especially 
if you're primarily focused on startup, they serve distinct purposes and influence performance at different stages.

Baseline profiles are used at installation time by the ART to precompile the methods and classes declared in the profile, the profile can include rules required for app startup 
optimization, along with additional profiles for other critical user journeys.

Startup Profiles contains rules specifically optimized for your app's startup path and it is used during compilation and not during installation, after D8 converts your source
code to DEX files, then R8 uses the startup profiles to influence the layout of your DEX files, R8 makes sure that startup code is placed in the primary DEX file for faster 
execution.

You should generally set `includeInStartupProfile` to `true` only for test scenarios essential to the app's initial display.

# [Micro Optimizations](https://www.youtube.com/watch?v=Z9-Z16glXRU)
Set initial size values in you collections, it avoids copying and resizing the collections every time they add a value. Use inline value classes this means add the annotation 
`@JvmInline` to you value classes, if you're only wrapping a value for type safety and readability then use value classes instead of data classes, if you do so you get the 
benefit of type safety of classes(data classes to), without the overhead of actually allocating a class at runtime, instead the compiler copies the value assigned to the value 
class in the code which delivers raw performance however they can have initializers, methods, properties and computed properties, those methods are converted to static methods
that take your parameter at runtime, compose uses value classes for size and offset, what they do is wrap a long in a value class and use 32bits for x and 32bits for y. Bitmaps
are stored row by row so it is more performant to read them by road instead of column since accessing column first will waste cached values. To debug in C and C++ you use `-g`
flag, and to optimize code you use different flags like `-02` which converts divisions and multiplications to bitwise operations, there is other flags you could try `-04`, java
compiler on the other hand doesn't do much optimizations initially when transforming source code into bytecode, however optimizations are deliver later, they are performed when 
the code executes with a combination of JIT and AOT code generated by the compiler for the jvm, kotlinc does a little more optimizations but nothing significant, however in 
Android the optimization is a very tailored process and is not directly performed on source code, instead, first it is compiled to bytecode by the javac or kotlinc, then they 
are translated into .dex(dalvik executables) by D8 and R8, D8 is used for debugging builds and, R8 is for release builds and can perform different optimizations, it will shrink 
and optimize delivering optimized .dex files, then the ART(similar to a JVM) executes the DEX bytecode and transform it to native instructions and its compiler uses both JIT and 
AOT, and you would think the final step is running those native instructions(assembly, i.e. ARM64) but truth is not the final step, modern cpus actually execute microcode, so 
almost all, if not all assembly instructions are turned into microcode. Using `by lazy` might not be a good choice performance wise. When you want to debug for performance 
usually you will use Android Studio's Kotlin decompiler, and people usually turns that bytecode into java to read it a little more easily but this is not a good approach because 
you're again hiding the information you wanted to look for. You can use [kotlin explorer](https://github.com/romainguy/kotlin-explorer) tool to find the DEX instructions and also 
aarch64 instructions your bytecode generates, read a little about it [here](https://www.romainguy.dev/posts/2024/micro-optimizations-in-kotlin-1/), to see assembly code you would 
need to plugin a phone or emulator, you can also enable R8, you can use AI to describe/explain assembly code, you can tell it to explain code line by line. Try to avoid companion 
objects in Kotlin because it adds a static class that which has to be initialized whenever the enclosing class is used the static class and its static fields are initialized and 
the bad thing is that wherever you call the enclosing class kotlinc creates code on every class call to make sure the companion object is initialized, if all you're putting in the 
companion object is private and internal constants then you should use top-level constants and use the right name space since that would be the only problem, naming them so they 
can explain their location, and you might prefer top-level functions as well.

Data locality is the practice of positioning computation as close to the physical data storage as possible. By moving processing code to the data rather than streaming massive 
datasets over a network, systems reduce latency, minimize network congestion, and vastly improve processing speeds. At the micro-level, data locality refers to how data is 
structured in system memory to maximize CPU cache performance. Because retrieving data from RAM takes far longer than fetching it from L1/L2 caches, software engineers write code 
that favors sequential memory access (e.g., arrays over linked lists). This exploits cache line architecture, allowing adjacent data to be loaded into the CPU instantly.

Be aware that if you're running benchmarks then you're not running the whole app and therefore you won't see GC runs, when you allocate your objects they will be close to each 
other in memory so it's not what's going to happen in real life and that is why you actually need both micro-benchmark and macrho-benchmarks

BTW most android devices are ARM64 now a days and ARM64 and aarch64 are virtually the same instruction set

Better eviction strategy for LRU caches

## Key Differences Between JVM and Android Runtimes

**File Architecture**: The JVM reads individual .class files (or packages of them inside .jar archives). Android uses .dex files, which merge all application classes into a single 
compressed file to deduplicate data and save memory.

**Virtual Machine Style**: The JVM is a stack-based virtual machine, meaning it uses an internal operand stack to evaluate expressions and execute operations. Android runtimes—such 
as the legacy Dalvik Virtual Machine or the modern Android Runtime (ART)—are register-based, meaning they use virtual registers to store data.

**Bytecode Set**: Because of the structural differences listed above, the instruction set (bytecode) inside a .class file is fundamentally unreadable to a runtime expecting .dex 
instructions, and vice versa.

Also introduce benchmarks in you CI to monitor for regressions. Whenever you want to optimize you app, fist read the code, then profile your app, then question yourself and investigate, 
most of the times the issue is not what you think it is, almost always is something else, the profiler you almost always want to use is the memory profiler and start tracking down 
memory allocations that you think should not exists, so read the code as you profile the app and track down memory allocations, always question yourself and investigate the code you're 
looking at, after you write the optimization, always write a benchmark, is very common to don't get the results that you're expecting, it can vary, sometimes is slower, or faster, include
benchmarks in your CI so you can track performance across time because is easy to introduce regressions, whenever you commit code you could get alerts, it could be good to get alerts even 
if the performance got better so you can investigate why and understand better.

# [Optimizing Kotlin Code in Practice](https://youtu.be/wLvGCnNLs7c?si=F9FXgYZdftGB0rWK)

To do profiling and optimization better you need hardware and software, try to choose the slowest device that can target your app, if it runs decently in that device it will run much better 
in other devices, usually benchmarking makes your device temperature hot, so you should use any method to cool it down. Use macro and micro benchmark libraries these libraries do several 
"optimizations" like disabling animations, lock the clocks of the device to avoid different frequencies of the CPU while benchmark is running to minimize interference with the benchmark. Use 
the Kotlin explorer to see what your code compiles to understand your code a little better, also you might like to use compiler explorer website, then to understand the compiled to(assembler 
instructions) you might like to have AI explain you what the code is doing line by line. Try to benchmark the following code which has performance issues, and is reading the pixels of bitmap 
being read vertically, meaning info is firstly read by columns in order to find the greatest red value 

```
val pixels = IntArray(1920 * 1080)
// get pixels of bitmap

var maxRed = 0
benchmarkRule.measureRepeated {
    for (x in 0 until 1920) {
	for (y in 0 until 1080) {
	    val index = y * 1920 + x
	    maxRed = maxOf(maxRed, pixels[index].red)
	}
    }
}
```

You fix it by switching the for loops parenthesis content, you need to iterate over rows instead of columns because this leverages the locality of the caches, this happens because of the cache 
line, whenever you go to read a value it will retrieve the next values in the line, this implies you should know the cache line size so you can iterate more efficiently, this is just an example, 
most codebase would need to do such optimization, it is also great to compare `number.sign` without R8 and with R8, usually R8 optimizations are very good, in this specific case the kotlinc 
compiler uses turns this into a bytecode which has more instructions which results in more assembler instructions, but after using R8 we can see the bytecode changed from using the pure Kotlin 
approach to instead using the same as if we have used Java from the start which would be the intrinsic function `Math.sigNum(int)` which because is intrinsic it is very optimized, actually there 
is very often times when the compiler relies on java functions to optimize kotlin generated bytecode.

Another function that generates a lot of, most of the times, unnecessary code is kotlin's `check` and `require`, they use contracts under the hood, but the reason it generates a more code than it 
may need is due to the need of throwing an exception, so to solve this you could implement your own function, the solution would be to throw the exception from other function

```
inline fun checkPrecondition(value: Boolean, lazyMessage: () -> String): Unit {
    contract {
        returns() implies value
    }
    if (!value) {
        throwIllegalStateException(lazyMessage())
    }
}

internal fun throwIllegalStateException(message: String) {
    throw throwIllegalStateException(message)
}
```

As mentioned before, prefer using top level functions with good naming instead of companion object inside util or helper classes, as when you create companion objects it creates a static class and 
when you create a static class and call it the semantics of Java and Kotlin is makes code to make sure the static class has been initialized, so everywhere you call that class the compiler has to 
add code to make sure the static object has been initialized, this is in the case your helpers companion object includes methods only, meaning you're not actually initializing anything. and if this 
code runs inside a loop then you're paying an extra heavy computation cost.

SIMD, MMX, AVX, Neon, are special instruction sets that let a cpu operate on multiple pieces of data, you can also do some SIMD with a single register and that is called SWAR(stands for SIMD within 
A Register), this is done in different places in compose, for example two places are, first when calculating the offset and pass it to a negative value, since the offset is wrapped ina Long(64-bits) 
but the x and y coordinate are only integers(32 bits) so we can just check turn the bit that determines the number sign and flip it in parallel this means the instructions is executed in parallel, 
in a single cpu cycle, so it is faster than if we would have unpacked the x, unpack the y, flip the each unpacked value individually and then pack it in another object also, instead here in a single 
cpu cycle we get to change the bit, even though we still need to repack it as value classes are immutable, the other place this is done is in svg paths, usually coordinates then to have very exact 
number(lots of decimals), but they are passed as strings, so what happens under the hood is that when the compiler groups characters in groups of four, remember each character in Java and Kotlin is 
16 bits, so they are packed in a long, so we end up with 64 bits, so now we can perform 4 operations at a time to figure out if that group represents a number and do those calculations in parallel, 
the process is, first since they are encoded strings, using the proper encoding format, we subtract the representation of 0(you can think of it in HEX, binary, or even decimal by the value a character 
in the encoding format represents ASCII or Unicode in this case you don't care too much what would be the Unicode bits format such as UTF-8, UTF-16, etc), if the value is lower negative, then it can't 
be a number, but if the value is positive, it could be a number, that is your first operation ran in parallel with SWAR, then we add to each character a "magic" number which is represented by the 
encoding value of letter F, this is done because if you add the greatest value of number characters(which is 9) to the value of letter F you will not get any value greater than 127(decimal, but you can 
make the conversion to binary or HEX), so values that are not numbers will be greater than 127, so the second parallel operation is add letter F encoding value, then you run two more checks in parallel, 
which is two masking operations, so you run an `or` on the results of the two operations, which returns 1 if any of the bits of the two values is 1, remember 1 represents true and 0 represents false 
just what an `or` would normally do, and then an `and` to a mask that sets the top bits which would be the value of -128, and if the result is all zeros then you know it is all digits. Most of the times 
fewer instructions mean optimized code.

In Kotlin `mutableMapOf()` returns a `LinkedHashMap()`, this could be bad for jetbrains because they now can never change the implementation since people might be relying in the ordered elements that 
a linked has, this map is expensive because it generates a lot of objects to keep the insertion order, also iterating over the map is really expensive and it misses cache a lot this is because the 
objects in the map could have been allocated in anywhere in RAM(as opposed to values in an array where data locality can be leveraged), instead in android collections package there is a scattered 
map(`mutableScatterMapOf<T, T>`), the API is similar to a hashmap, it has three arrays, an array of keys, an array of values, and array of metadata(one byte per entry), when you want to read a value 
from the map, you read one byte from the metadata, the it read value and key arrays, and since they are using arrays under the hood, your reads could benefit from the cache, this map insert and does 
a `foreach` faster than `LinkedHashMap` but it removes a little slower, even when it is slower removing you still have a memory efficient data structure because it doesn't allocate any objects on your 
behalf, only when it needs to grow or shrink, it can look up 8 positions in the metadata to find the value you want.

In Kotlin when we do `String.toFloat()` it parses the float and if not a float numeric string, then it return null, however that is a very expensive computation because is made with regular expressions, 
which are expensive on their own, it allocates 930 objects whenever you call that

Check the app performance score in the android documentation, always keep compose updated to its latest version, use R8 to shrink and optimize the app, use baseline profiles and startup profiles, start 
up profiles tells the ART what pieces of code the apps needs to start and that info is used to reorganize the DEX files in the APK to put the start up code together and close to each other so that memory 
and disk cache can benefit from it.

Another thing I learnt from [this video](https://youtu.be/M6extgmQQNw?si=vyU6_-LvJo451WUd) explaining how system services work, I learnt that the whenever we request for a service the system returns us a 
manager, that manager doesn't directly has the code that process our requests, we will talk more about that in a second and also about some performance implications underneath, first we need to know that 
these services are accessed through the context, the context is an object that allows us to access system functionality, it lets us interact with the underlying OS through a layer called "Application 
Framework" which are all the APIs that communicate with underlying components of the OS architecture, services are part of that layer(i.e. Location service) and pretty much all the classes we use to develop 
our apps also, we can access to it from practically anywhere in the presentation layer, the 4 main components of Android apps all extend the `ContextWrapper` class, this class at the same time extend the 
`Context` class, the context class defines the methods we can operate over an instance of what is called `ContextImpl` which is the object that actually has all the actual code that executes whenever we need 
to communicate with the system to get different resources, the wrapper contains it and delegates all the logic to it, that object has a reference to something that seem like a collection called 
`SystemServiceRegistry`, that registry is a set of callback(provider) you execute whenever you reach for a system service, the first time you call for a service the callback is executed and creates an 
instance of a manager, all subsequent call to that service return the same manager object, there is only one instance of each service in the system however ther can be many more instances of a manager, if 
the app has two activities and each request the same service then you'd have created two manager instances that rely on the same service but are two different instances, however a manager lives in your 
application process while most services live in a process called "System Server", so in order for them to communicate you need to do some IPC, so they rely on an API called "Android Interface Definition 
Language"(AIDL) which you use to define two other interfaces on the manager side that is known as "Proxy" and the name of the proxy implementation usually doesn't even include that word, on the system 
process side which is running the service(it could be other process other than the `SystemServer`) the created interface is known as "Stub", this is done because the IPC communication is done using `Binder` 
and the reason it uses AIDL is because it simplifies and seems to standardizes how IPC is done using `Binder`, so when you interact with your manager it interacts with an object that could be refer to as 
"Proxy" which can communicate with the process running the service through and interface that is referred to as "Stub" using "Binder" under the hood, however this is where we can optimize our code because 
when you send an object from one process to the other using `Binder` this creates a copy of the object in the other process making the original object in the origin process not eligible to be garbage 
collected on the origin process side, not until the reference to the copy object in the destination process has been destroyed which according to what is said in the video doesn't happen as fast/often as 
you'd like which could cause memory leaks, for example if you implement a listener in your activity and pass that listener to an service if the activity is destroyed the activity resources are not released 
immediately, leaking resources no matter what you do, so what you want to do is not pass resource consuming objects like an activity, instead it could be an anonymous object or just an object implementing 
some callback class. There is a component in between the two processes, the app process and the process running the service(i.e. System Server), called `ServiceManager`, services are registered here using 
unique name, for example the `SystemServer` process starts when the device starts, it creates instances of some services the system needs, each service generates a **Stub** that we mentioned previously, 
these **stubs** are passed to the `ServiceManager` by each service and they are converted into something called `IBinder`, this binder is some sort of handle to the service, according to the video the 
`ServiceManager` also has a record of registered services by name, which previously it was said that services where registered by name in the `ContextImpl` registry, when the app request a service this 
request is handled by the `ServiceManager`, when a manager(i.e. LocationManager) is created the first time it asks the `ServiceManager` for the IBinder that matches the name of the requested service, the 
returned object can be used to generate a **Proxy** which is the component that the origin process uses to communicate via `Binder`, for example, an alarm manager proxy is called `iAlamrManager`. Check 
services running on a device with adb command `adb shell service list`

[Inside the Renderer](https://www.youtube.com/watch?v=lkpV7EzayfU)

ART reorders field properties(instance properties) of a class based on their type and their name, so depending how you access them and how you name them then you will be affected by cache misses or not, 
it changes cache 

When you use JNI they library you're using is loaded and automatically you have the APIs that can talk to that library, obviously you're very limited in what you can do and also the library must expose APIs 
that are very C like, the most performant way to use the JNI in Android is to only make JNI calls that would pass down from java primitive types from, all the calling java methods extracting data should be 
done on the Java side and the native function that you call should just take all those primitives(that includes arrays), this make the JNI code a lot easier because you don't have that dance of looking up 
the java function from the C++ side, calling back the VM making sure you're doing it the right way which is usually the part that is "painful", this way your JNI becomes a really thin glued interface, it is 
very easy to make mistakes, specially when you manipulate arrays because if you're not careful you're going to copy the entire array which is expensive.

In Android you can think of the rendering pipeline end-to-end as three major components, the UI toolkit(all widgets) which sits on top of the canvas and when the window is doing its rendering the buffer that 
the window rendered is handed over to the window compositor, which is called **surface flinger**, this flinger will take all the windows that are visible on screen and composite them together there is 
different ways to do that. Canvas was backed by Skia, Chrome uses Skia also, Skia was a CPU base rendered(software rendered), and the window compositor itself was always using either OpenGL or something the 
Android team called "hardware composer" which is basically an abstraction for OEMs, this tells the phone manufacturers "hey here are all the windows, tell us if you can render them yourself using som secret 
sauce you have in your hardware, if you can't just give them back and we will use the CPU"(it changed to GPU later), but after new devices starting appearing, you had more inches and pixels per inch, the cpu 
was not going to be able to do all the computations when there is more pixels on the screen, so the UI pipline/UI toolkit had to move to do rendering computations using the GPU and that was done by rewritting 
some functions of the Canvas API, without changing the API itself, to make it use the GPU instead, GPU is commonly use by video game apps, video playback, media apps, that happened in Android 3, so the GPU 
render was not using SKIA anymore, it was still using it for a few things specific to the Android UI toolkit, and all the way to Android P(around 2017) Android backed to SKIA again, because SKIA had been 
working all that time in their own GPU renderer and it had reach the point where it made sense to stop Android investing in their own renderer and go back to it instead. The way a GPU renders is a little 
different nowadays and this is more clear with computer shaders, but effectively have to send the GPU triangles that you can texture, so you have the concept of shaders which is a program that runs on every 
pixel(per pixel) where you can compute the color of such pixel using mathematical operations, for example the modern way to render text is as vectors and that data is in the font files, in the old days they 
where rendered by the CPU so the computation power wasn't available and therefore what it did is, it drawn each glyph(glifo, jeroglifico) into a texture and then for each character you want on screen it 
generated two triangles and then make it point to that texture, this was called an atlas, but it was a very complex system, in the early stages of the GPU if you wanted to optimize its computations you had 
to avoid changing state, the state to draw text is different to draw images, and so on, so what was happening at that point is that the commands where grouped by state to avoid changing state too much. In 
Android you can do 3D graphics using three options, Android has a built in 3D graphics API for "simple" use cases, for more complex uses cases you have to either use a game engine, however they are kind of 
heavy and they tend to take full screen, the third option is to write OpenGL or Vulkan code which is kind of complicated, btw Android uses all three grpahics engines, Skia, OpenGL, Vulkan, Skia on new chipsets 
since 2024 could be using Vulkan under the hood, it seems also that OpenGl is not under development any more and Android requires Vulkan is required from Android 15(2024), also an OpenGL impelementation seems 
to be working Vulkan under the hood. Android XR should be using the built it 3D rendered. In graphics AI and ML is doing work that is not LLM, like using micro neural networks being used as a form of data 
compression to replace textures of materials, we are talking about really tiny networks that you know fit in a few lines of code in the shader, this is a specific problem being solved instead of having a big 
model that you throw anything at

# TIps

* For bitmaps that are used like thumbnails or just don't need transparency set the Bitmap config to use RGB565 instead the default ARGB4X since the default uses
  twice as much as the suggested one. In Coil, you can use the `bitmapConfig` property to configure it.
  
* Glide and Coil helps you downscale and use a bitmap pool for more performant memory usage
  
* You can find duplicated bitmap usage using the AS profiler with a "Analyze Memory Usage" profile, this gives you a Heap dump, duplicated bitmaps are highlighted
  automatically
  
* Use the APK analyzer tool to ensure that you aren't packaging larger than required image files. Reduce the sizes or consider placing the images on a server and only
  downloading them when required.
  
* The profiler in android studio has a "Find memory leaks with LeakCanary" option which will help you find memory leaks
  
* `ProfilingManager`, introduced in Android 15, is an API that lets you collect real user Perfetto profiles prgramatically, it gives you two types of profile collection
  `App-driven` and `Event-driven`, in the former you define the start and the end of the collection process and the latter are automatically collected by the system. As
  of 11/3/27 the events it tracks automatically are ANRs, APP_FULLY_DRAWN, KILL_TASK_MANAGER, KILL_RECENTS, KILL_FORCE_STOP, COLD_START, KILL_EXCESIVE_CPU_USAGE, ANOMALY,
  OOM (out of memory), with the android 17 restriction on memory usage the ANOMALY trigger is really useful because it identifies performance anomalies detected by the
  system, it supports memory and binary spam, if a memory usage exceeds a threshold it creates a heapdump which allows you to use this trigger to examin resouce
  allocations and the app state to identify the root cause. If the app is terminated due to violating the android 17 memory usage limit it will provide a heap dump. With
  the OOM this manager monitors for out of memory errors, when this occurs a heap dump is created also, so this is more powerful than just a stack trace in crahsaliytics.
  This manager lets you register a result listener which will only provide you with the information on the next app start up, and from that listener you send the report
  to your servers, then you can use perfetto to inspect the heap dump as shown in [this video](https://youtu.be/fOXJR5qLq54?si=nZ7ufFkzV3UgiXXq). Check perfetto heap profiles
  
* [This Document](https://android-developers.googleblog.com/2026/06/prioritizing-memory-efficiency-steps-for-android-17.html#Trim): Shows us how to register a callback
  so our app can free memory more effectively to avoid the OS killing our app and or slow user experiences due to page swapping, register in `Activity`, `Fragment`,
  `Service`, or even your custom `Application` class (Using it in the Application class is highly effective for global cache management) for the `onTrimMemory()`
  callback. This is useful due to the RAM behavior explained [here](https://android-developers.googleblog.com/2026/08/app-broader-memory-limits.html), where you can
  see compressing and decompressing pages can prevent immediate eviction but adds CPU overhead, which can result in noticeable UI jank and experience slowdowns. And
  look [here](https://developer.android.com/topic/performance/memory/manage-app-memory#release) for the official documenation
  
* Crashlytics version 20.1.0 introduces additional debug data to help you catch, prioritize, and fix Out-Of-Memory exceptions and memory limiter kills.
  
* Add LeakCanary library to your app to receive Logcats when a possible memory leak happens when activities, fragments, viewmodels, services are destroyed
  
* Use `SparseArray`, `SparseBooleanArray`, and `LongSparseArray` instead of `Hashmap`
  
* Use lite protobufs instead of regular ones as regular ones generates more code

* System traces tells us everything that is happening in the device, this information helps us understand when and what our application is doing, for example it can show
  us how long our app took to start,  when a thread is doing blocking I/O, it allows you to identify slow operations and understand how different threads work together.
  Once we have identify places where things are not working as expected we have to understand why, so we do Stack sampling, Stack sampling also shows us whats happening
  but it helps us understand what code is executing, but collecting those traces have a performance impact, so you can't rely solely on them to understand how the apps is actually doing.
  You can take stack samples using the sampling profiler, beware that if you collect stack samples without a systrace first you may be inspecting the wrong information
  for example you could be sampling the wrong thread, not the thread which is actually doing the work you're concerned about. Stack samples shows proportions not timing
  info. Perfetto offers us the advantage of helping you understand system behavior and inner process communication, while AS profiler focuses on the app exclusively.
  You'll trace using Perfetto to identify places where app is spending too much time, and then go deeper with stack samples
  
* You can start a method tracing programatically with `Debug.startMethodTracing("my_app_trace")` and `Debug.stopMethodTracing()`. The system saves the resulting .trace
  file in a package-specific directory on external storage, get the file with `adb pull /sdcard/Android/data/com.your.package/files/my_app_trace.trace` and drag and drop
  it in AS profiler. An interesting code is `Coreographer.getInstance().postFrameCallback { handler.postAtFronOfQueue { Debug.stopMethodTracing() } }`, this will let you
  collect more specific call stacks. However with this approach you're doing a continuous tracing which is consumes more resources and can make your app run really slow,
  so to profile methods with lees overhead take samples ` startMethodTracingSampling()` and stop it the same way, This info is found [here](https://developer.android.com/studio/profile/generate-trace-logs)

* Emulator vs Physical Device: For performance tracing use a physical device, the more constrained the phone is the better so you can feel first-hand the parts of the
  app that can drop frames and cause UI janks, an emulator is not the best for performance tracing because they have the computer's hardware available which is not
  realistic, phone's are generally not as powerful as desktops and laptops but also the performance might depend on what you're running on your machine, so deffinitely
  use a physical device. For memory profiling (sampling) preffer a physical device but an emulator should be enough.

* For CPU profiling/tracing you're app should be marked as profileable, this configuration is similar to a release build, we can't use a debuggagle build because it is
  not optimized because this is the only way for you to be able to step into the execution to debug your app at runtime, it comes at a performance cost but the benefits
  to developing your app are greater. Profileable builds will not have allocation tracking available, they don't have access to the same level of debug hooks as debuggable
  builds. So you may have different build types, debugging performance you can use a run configuration or just android studio profilers as they will configure the installed
  APK as necessary but for benchmarking with Macrobenchmark for performance measuring you do need different build types and you can see how to configure that in the
  Macrobenchmark documentation. Instead of BuildTypes you can do different run configs, this is noted in the tools.md file. Macrobenchmark can make sure the app is as closed
  to a release build as possible, it can make sure the test run just as if the code was already precompiled either by AOT or JIT (JIT turn in AOT later). Collecting garbage
  is not expensive under responislb euse of memory but if you're producing a lot of garbage it can trigger GC collections too oftes which can drain battery more quickly, so
  avoid allocating too many objects in places like the innermost part of a for loop and it could even cause some UI janks

* Android live allocation tracking using the memory profiler. It introduces performance overhead but can help identify memory leaks, just be aware that the GC behavior is
  unpredictable and therefore this is a complicated task. The memory profiler allows you to see the allocations happening throught the app, you can see how and what is
  being allocated and some details about what the objects are, you can also track them through time (visually) and see them being deallocated (collected). Using that
  information you can approach memory leak hunting with a repeatable task, for example, navigating to a screen, trace it, then go return to previous scene and then forward
  again to the same scene a few times, you can record these profile sessions and if an object(s) is not being GC then you should be able to start noticing, macrobenchmark
  can automate cpu usage profiling but can also collect memory traces, so you could have a test that does the navigation and then collect a memory trace so you can then
  take a look. You can track native allocations using perfetto (metadata and more). You could also override the `onTrimMemory()` callback at component or app level and
  request user permission to capture a Heap Dump at runtime, because it is a resource consuming task it is a good idea to ask the user to authorize you to do the dump
  which you can forward to your server, you collect it programmatically with `Debug.dumpHprofData(filePath)`. You can also get a heap dump programatically whe an OOM
  occurs using the the `ProfilingManager` and registering for a result callback that returns the heap dump when the app is started again. Since the OOM memory or onTrim
  callback be caused due to a memory leak it is a good starting point to troubleshoot potential leaks.

* Avoid manual `WakeLock` management; use `WorkManager` for background tasks to keep the CPU running while the device screen is off


Heap Dump Vs Allocation Tracking, Sampling vs Instrumenting
  

# Testing
https://developer.android.com/develop/ui/compose/testing/interoperability
https://developer.android.com/training/testing/ui-tests

# Continuous Integration
https://developer.android.com/training/testing/continuous-integration
https://developer.android.com/studio/projects/continuous-integration
