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

#### Types of Charts
Before talk about charts and sections in the Analysis pane we will talk about its sections and charts.

* **Top down and bottom up charts**: 
* ****
* ****
* ****
* ****

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



