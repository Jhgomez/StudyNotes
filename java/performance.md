# Context
In my computer "JAVA_HOME` is set to "openjdk-21.0.2" and `java -version` prints bellow message
```
openjdk version "21.0.2" 2024-01-16
OpenJDK Runtime Environment (build 21.0.2+13-58)
OpenJDK 64-Bit Server VM (build 21.0.2+13-58, mixed mode, sharing)
```

# JDK Performance Monitoring Utilities
The bin folder contains the following programs that can be used for profiling and monitoring:

* Java ViusalVM: It used to be part of the Oracle and Open JDK distributions in the past but that changed after JDK 9 since it is no longer included and has to be downloaded separately
* JConsole
* Java Mission Control
* Diagnostic Command TOol

## Java Flight Recorder
This is just another monitoring program but I will focus on it because I want to use it to monitor my apps. This isn't a standalone program. Its usage is closely related to two tools, "Java Mission Control" and "Diagnostig Command Tool"

JFR collects information about the events in a Java Virtual Machine (JVM) during the execution of a Java application. JFR is part of the JDK distribution, and it’s integrated into the JVM. JFR is designed to affect the performance of a running application as little as possible.

We can start/create a JFR recording :

1. when starting a Java application, from the command line. In my case I will use Gradle to pass this arguments to the JVM/JDK
2. passing diagnostic commands of the jcmd tool when a Java application is already running
3. Using the JMC interface(you have to download JMC first)

JFR doesn’t have a standalone tool. We use Java Mission Control (JMC), which contains a plugin that allows us to visualize the data collected by JFR. These tools working together form a suite for collecting low-level runtime information of a running Java program

If we have various versions of Java installed on our computer, it’s important to make sure that the Java compiler (javac), the Java launcher (java) and the above-mentioned tools (JFR, jcmd and JMC) are from the same Java distribution. Otherwise, there’s a risk of not being able to see any useful data because the JFR data formats of different versions might be not compatible.

JFR has two main concepts: events and dataflow.

### Events
JFR collects events that occur in the JVM when the Java application runs. These events are related to the state of the JVM itself or the state of the program. An event has a name, a timestamp, and additional information (like thread information, execution stack, and state of the heap).

There are three types of events that JFR collects:

* an instant event is logged immediately once it occurs
* a duration event is logged if its duration succeeds a specified threshold
* a sample event is used to sample the system activity

### Dataflow
The events that JFR collects contain a huge amount of data. For this reason, by design, JFR is fast enough to not impede the program.

JFR saves data about the events in a single output file, flight.jfr. 

As we know, disk I/O operations are quite expensive. Therefore, JFR uses various buffers to store the collected data before flushing the blocks of data to disk. Things might become a little bit more complex because, at the same moment, a program might have multiple registering processes with different options.

Because of this, we may find more data in the output file than requested, or it may not be in chronological order. We might not even notice this fact if we use JMC, because it visualizes the events in chronological order.

In some rare cases, JFR might fail to flush the data (for example, when there are too many events or in a case of a power outage). If this occurs, JFR tries to inform us that the output file might be missing a piece of data.

### How To Use It
in earlier JDK distributions, we have to activate commercial features in order to use it in production. However, starting from JDK 11, we may use it without activating anything. For JDK 8, to be able to activate JFR, we should start the JVM with the options +UnlockCommercialFeatures and +FlightRecorder. 

In our case I will show how to set up flight recordings inside a JavaFx Desktop app for Windows using Gradle Kotlin, remember you have two options, start JFR when an application starts or whenan application is already running.

#### Create a JFR Recording
I'm using a modular/multi module JavaFx Windows Desktop application with several gradle modules and as mentioned in prev notes there is at least three ways to start a trace/recording, on application start and on demand(while application is running any moment) these two options can be executed in the command line if you're "building" your app on your own but since I'm using Gradle the arguments passed to the JVM to start a recording are configured in a Gradle buildscript, and the third option I know of is using JMC interface. The data that records capture are events, they can be of different four types:

* **Duration Events**: they have duration, a start and stop time
* **Instant Events**: WHen it ocurrs it gets instantly logged, for example, when a thread gets blocked
* **Sample Events**: THeir purpose is to check the health of the system, they are logged on time intervals previously specified, for example, printing heap diagnostics every minute
* **Custom Events**: These events are created by the user using JMC or other APIs, for example starting a trace on starting a certain function call and stoping the trace on function complete

In addition, there are predefined events that are enabled in a recording template. Some templates only save very basic events and have virtually no impact on performance. Other templates may come with slight performance overhead and may also trigger garbage collections to gather additional data. The following templates are provided with Flight Recorder in the <JDK_ROOT>/lib/jfr directory:

* **default.jfc**: Collects a predefined set of data with low overhead.
* **profile.jfc**: Provides more data than the default.jfc template, but with overhead and impact on performance.

Flight Recorder produces following types of recordings:

* **Time fixed recordings(the one I needed in my case because of what the use cases for it can be as described below)**: A time fixed recording is also known as a profiling recording that runs for a set amount of time, and then stops. Usually, a time fixed recording has more events enabled and may have a slightly bigger performance effect. Events that are turned on can be modified according to your requirements. Time fixed recordings will be automatically dumped and opened.

  Typical use cases for a time fixed recording are as follows:

    * Profile which methods are run the most and where most objects are created.

    * Look for classes that use more and more heap, which indicates a memory leak.

    * Look for bottlenecks due to synchronization and many more such use cases.

* **Continuous recordings**: A continuous recording is a recording that is always on and saves, for example, the last six hours of data. During this recording, JFR collects events and writes data to the global buffer. When the global buffer fills up, the oldest data is discarded. The data currently in the buffer is written to the specified file whenever you request a dump, or if the dump is triggered by a rule.

  A continuous recording with the default template has low overhead and gathers a lot of useful data. However, this template doesn't gather heap statistics or allocation profiling.

##### Donwload JMC
This tool will let us monitor all processes runing on JVM or a JVM(deployed java produced .exe  files), it will also let us read JFR recordings and start one as well.

1. [Download Java Mission Control 9](https://www.oracle.com/java/technologies/javase/products-jmc9-downloads.html)
2. Decompress the file and find the application called `jmc.exe`

##### Start a JFR recording on Application Start
As mentioned before since I'm building/running the app using Gradle I just add the following configuration to the project's build script and then when I run the app(`./gradlew run`) or deploy it as a desktop app(`./gradlew jpackage`) and then run, it will automatically start a recording with the specifications I configured. Note that I'm using Gradle Kotlin
```build.gradle.kts
application {
    mainModule.set("COLINS.app.main")
    mainClass.set("com.colins.Colins")
    applicationDefaultJvmArgs = listOf(
//        "-XX:+FlightRecorder", seems this is deprecated, it is not required to turn this feature on
        "-XX:FlightRecorderOptions=stackdepth=512",
        "-XX:+UnlockDiagnosticVMOptions",
        "-XX:+DebugNonSafepoints",
        "-XX:StartFlightRecording=duration=6s,filename=myrecording.jfr",
//        "-XX:+UseParallelGC",
        "-XX:+HeapDumpOnOutOfMemoryError",
    )
}
```

You can specify more options to the "start command"/"start argument" with the parameters defined [here](https://docs.oracle.com/javacomponents/jmc-5-4/jfr-runtime-guide/comline.htm#BABGCBBA) or following the instructions [here](https://docs.oracle.com/javacomponents/jmc-5-5/jfr-runtime-guide/run.htm#JFRRT172) you can define other arguments to configure your recording(`-XX:FlightRecorderOptions`). For example, remember you can define a template used to defined what events or information you want to record and there is already two predeifined templates(default and profile, being profile a more detailed record), you can create your own but it might be easier to do it using JMC as it is more graphic, I would like to make sure a `profile` recoding is being made, so I define the following argument
```
"-XX:FlightRecorderOptions=defaultrecording=false,dumponexit=true,dumponexitpath=path"
```
If you were running it without Gradle this commands would have to be passed when you run the application using `java` for example `java -XX:+UnlockCommercialFeatures -XX:+FlightRecorder -XX:StartFlightRecording=duration=60s,filename=myrecording.jfr MyApp`

Now just open JMC and open the recording file from it

##### Start a JFR recording When App is running
We will use the java utility called `jcmd`, you might want to add it to your OS path this way you don't have to navigate to the JDK's `bin` directory to be able to run this app.

1. Run your app any how you want
2. Get the process id by running from the command line the command `jcmd`, this will print all running java processes, identify yours(it should be easy) and copy the ID
3. `jcmd 10828 JFR.start duration=3s filename=flight2.jfr name=profile`
4. You can add more configurations to the start command as mentioned in a link in the prev section

`defaultrecording=false` should be the default value so there should not be any need to specify this but if you still want to do it you will have to combine `jvmargs` and `jcmd` commands, so you have to specify this as in the previous section with the `-XX:FlightRecorderOptions` argument and then just start a recording with any of the configurations indicated in the same [link](https://docs.oracle.com/javacomponents/jmc-5-5/jfr-runtime-guide/comline.htm#BABHIICD) indicated in the prev section

##### Start a JFR recoding using JMC
The steps are defined [here](https://docs.oracle.com/en/java/java-components/jdk-mission-control/9/user-guide/using-jdk-flight-recorder.html#GUID-88CC453C-0CED-45D6-9E93-28A03F3752F2) but in my own words follow steps below:

1. open JMC
2. Run your app
3. You will see on the left a section called `JVM Browser`
4. Identify your app(should be easy to so)
5. Right click the app in the list and click on `Flight Recorder`, optionally you can expand the app with the arrow on the left and double click `Flight Recorder`
6. Choose the templace you want to use or you can modify an existing template which will generate a new one with all your changes

###### Check out MBean Server
This is not a recoring but it is a functionallity in JMC that lets you see more info 

1. Expand the app you want in the section `JVM Browser`
2. Double click `MBean Server`
3. On the "Dasboard" section you will see a green plus sign that lets you add other vizualization, I would go the "Memory" section and then `FreeHeapMemory`
4. At the bottom you will have tabs you can check out, again I would be interested maybe mainly in the "Memory" tab

# Other Performance Tools
* JProfiler
* Glowroot
* Sematext
* Dynatrace
* JCMD

## JCMD
This is a very important tool, at least for me because it helped me understand the solution described in the section below and also it helped me understand a JVM behaviour I was not expecting and was not aware of it. This toola enables us to do "native memory tracking", you can get more details [here](https://www.baeldung.com/native-memory-tracking-in-jvm)

Before start using this tool you need to enable it with the JVM flag

* `-XX:NativeMemoryTracking=off|sumary|detail`, I used teh `sumary` option

After finding the configurations that helped me reduce the memory usage which in short I just had to select `ZGC` garbage collector and restrict the inital and max heap size to 400 both, I saw a big decrease in RAM usage, however after trying the application in another computer I found that the RAM being used was higher so I went on to investigate and found that the `JCMD` tool lets us trac the native memory usage, and as you can see in the article I reference before an application could be consuming more RAM than the value we assigned as a max heap size, and that depends on the JVM ergonimics, first we have to understand that the JVM needs to allocate memory for other components of the JVM such as the following

* **Metaspace**: Previous Java 8 this was called PermGen or Permanent Generation, This contains metadata about the loaded classes
* **Threads**: One of the most memory-consuming data areas in the JVM is the stack, created at the same time as each thread. The stack stores local variables and partial results, playing an important role in method invocations. The default thread stack size is platform-dependent, but in most modern 64-bit operating systems, it’s around 1 MB. This size is configurable via the -Xss tuning flag. In contrast with other data areas, the total memory allocated to stacks is practically unbounded when there is no limitation on the number of threads. It’s also worth mentioning that the JVM itself needs a few threads to perform its internal operations like GC or just-in-time compilations.
* **Code Cache**: When the JVM compiles bytecode to assembly instructions, it stores those instructions in a special non-heap data area called Code Cache. The code cache can be managed just like other data areas in the JVM, however if we reduce this area our application will have to constantly interpret and then compile assembly code, the JIT compiler is in charge of this functionality, if we make it too small we could gain less RAM usage in exchange of a less performant app since parts of our app that are frequently used may have to be constantly compiled over and over again
* **Garbage Collection**: There are various garbage collectors, all of them share one common trait: they need some off-heap space to store data structures they use to perform their tasks, in my case since I choosed ZGC because after testing other GCs, this was the one that was helping me reduce RAM usage this may be because this GC strategy to unload classes in Metaspace is agressive, also this garbage collector creates threads depending on the host capability and these two characteristics can be specifically defined with their corresponding flags, for more agressive class unloading `-XX:+ClassUnloadingWithConcurrentMark` and `-XX:+ClassUnloading`, for limitting GC threads `"-XX:ConcGCThreads=2"`, other characteristics we can set are `-XX:ZUncommitDelay=1` for uncommit(returning) unused pages after 1s back to OS, however this last flag and the threds limit flag was not making my app reduce its RAM usage, instead the ram usage was lower without setting this flags, and I choosed not to unload metadata(loaded classes) too agressively since this could actually make my app consume more CPU as it is without it

There are other reasons why the JVM might be using more RAM than what I defined in the heap like Symbols(strings) and string pool, native byte buffers and they are mentioned in the docuoment previously shared but they are not a problem in our app since for most strings I use an `strings.properties` file which is a recommneded approach in Java.

If you want to know/find almost all tunning flags related a concept mentioned here you can use the following command
```
java -XX:+PrintFlagsFinal -version | grep <concept>
```

use it like this: `java -XX:+PrintFlagsFinal -version | grep Metaspace`

### Native Memory Tracking
In order to better understand the information this functionality can provide us we needed to know more about the previous concepts of the JVM ergonomics because the information it is going to share is basically indicating us how much RAM each concept is using

1. Launch your app(you can do this anyhow), in our example we will launch it from the command line `java -XX:NativeMemoryTracking=summary -Xms300m -Xmx300m -XX:+UseG1GC -jar app.jar`

2. Find the java process id, you can either do that with the command `jps -l` or `jcmd`(alone, no flags or any parameters)

3. Take a snapshot `jcmd <pid> VM.native_memory` or `jcmd <pid> VM.native_memory summary`

4. You can track it over time by defining a baseline to compare against later, set a baseline first `jcmd <pid> VM.native_memory baseline`

5. compare with another snapshot with `jcmd <pid> VM.native_memory summary.diff`

You could even get more detail information with the flag `-XX:NativeMemoryTracking=detail`

### Conclusions obtained using this tool
My first issue was that my app was using too much RAM, this was solved with the confugartions indicated in this section previously but alos as indicated in the "Solution" section below. After that I found another "issue", or that is what I thought it was at the beginning, I had a computer with 16GB ram and another with 32GB ram, the total native memory being used was higher on the 32GB ram computer on app start it was using around between 80MB and 90MB more than in the other computer and at some point, after some usage, it reached arount 80MB to 120MB more that on the 16GB ram computer, after investigating with this tool I found that it was basically the JVM behavior expected for a computer with more core(threads), the 16GB computer cpu had fewer cores/threads than the other computer, so depending on the cmputer(host) running the JVM it will allow the off-heap conpcepts/stuctures to grow larger than in other computers, meaning in my 32GB computer the metaspace was allowed to load more classes, the code cached handled by the JIT compiler was allowed to store more compiled code, the GC was loding more metadata(“GC” category), ZGC maintains internal tables and marking data proportional to the heap and thread count. Thread stacks, ZGC on the larger-core machine spun up more collector helper threads even though the ammount of RAM used by this thread stack was fairly small, it is still worth to mention it. In conclusion there was nothing else for me to change, meaning there was no need for me to change, add or remove any JVM argument since my app was working as expected in both computers 

# Performance Tips
## Avoid recursion
Recursion is a technique that can be quick and effective in languages that provide tail call optimization. Java, however, is not one of these languages. Recursion is 
hence an expensive procedure. In most cases, you should choose an iterative solution utilizing loops over a recursive solution with Java. However you can do "Tail Call Elimination" as mentioned before by using loops

## Leverage StringBuilder
Java offers a bewildering array of options for combining shorter strings into longer ones, but most of these options follow a two-sequence approach to buffering a string into a long thread, adding significantly to the Java heap.  Because of this, memory duplication is required when an operator is initialized. Java has Stringbuilders that employ a one-sequence approach. 

The StringBuilder is a mutable asynchronous function that provides a string-like class that allows you to initialize an operator in a single sequence. StringBuilder doesn’t have any overhead from thread synchronization and is, therefore, the fastest way to build large strings from smaller pieces.

## Static Final
Avoid them as according to some comments [here](https://stackoverflow.com/questions/6470651/how-can-i-create-a-memory-leak-in-java) this could cause a memory leak

## Valhalla Project
It aims to adapt Java Language and rumtime to modern hardware. The enhancements are described in their respective "Java Enhancement Proposal"(JEP)

* JEP 401: Value Objects
* JEP 401: Primitive Classes
* JEP 402: Classes for the Basic Primitive
* JEP draft: Universal Generics
* JEP 218: Generics over Primitive Types

## Vector API
Basically it flattens objects into other objects in a similar manner as in project Valhalla according to [this](https://www.youtube.com/watch?v=SPc9YpLsYo8) video on minute 11:00, basically you can do things like adding two int arrays with their respective index in the two arrays and will be added using "JEP401". This API could have started as part of tbe Java "Panama Project", Project Panama aims to ease the interaction between Java and foreign (non-Java) APIs, i.e., native code written in C, C++, etc.

## JavaFX Specific
### Navigation/Displaying Different Screens
#### Avoid Creating New Stages Frequently
Unless you really need multiple OS-level windows, avoid using new Stage. They create new rendering pipelines and memory contexts. Creating new Stage and Scene objects every time you switch screens prevents JavaFX from reusing internal rendering buffers, leading to repeated allocation. **Stick to swapping views or changing root nodes**, in my case I used `scene.setRoot()` method.

### Image Optimizatuion
Compress your image size with any image compressor tool and when displaying them make sure to use an `Image` and set the correct `requestedWidth`, and `requestedHeight` attributes, and then wrap in inside an `ImageView`, do not load them directly from `imageView`, this will only use the memory required to display the size you want.

### Observations
#### Resize
Rezising a stage that contains a scene with any view inside a ScrollPane will increase memory usage and it will not be freed, the question is "is this considered a memory leak?", it could be because JavaFx stores something in a buffer when the size changes, this behaviour is more noticeable when you have two screens, even if you use the same stage and same scene(just swapping the scene's root)

At the moment I don't see any solution but we can try to define some logic that restricts the minimun and the maximum size of a screen.

This observation was not tested with responsive views like `VBox`, `HBox`, `BorderPane` and `GridPane`, so building a responsive layout may be the solution

#### Responsive Layout/ui(TODO)
Articles about responsive layouts are [this](https://www.demo2s.com/g/java/how-to-do-responsive-design-in-javafx-in-java.html) and [this](https://moldstud.com/articles/p-explore-javafx-for-modern-java-user-interfaces). In web development, with HTML and CSS, we have `FlexBox` is a very powerful tool to create responsive layouts and in JavaFx there is this tool, [FlexBoxFxj(https://github.com/onexip/FlexBoxFX) which I stil havent't tested but the memory usage might be very high

### Performance Articles
* https://www.reddit.com/r/JavaFX/comments/uxg99y/javafx_and_switching_scenes/?rdt=50676
* https://forums.oracle.com/ords/apexds/post/how-to-free-the-memory-after-closing-javafx-stage-8830
* https://moldstud.com/articles/p-10-bizarre-bugs-encountered-by-javafx-developers-and-how-to-fix-them
* https://codingtechroom.com/question/javafx-resource-cleanup

# TODO
## Try Using a DI framework
* https://javanexus.com/blog/mastering-dependency-injection-javafx-dagger
* https://www.pragmaticcoding.ca/javafx/swap-scenes

# My analysis(personal notes)
I'm trying to optimize HYU app memory usage, I created a copy of HYU app from zero called "conElG" in a folder called "conG" both mean "con el gradle", first with just the "Welcome Screen", from this I learned how to optimize images. Then I learnt the rezising issuge in a ScrollPane as noted in the "Observations" section. Then I added a "presentation"(Interaction Module) module, but no other layers modules from domain or data layer, then I moved everything to the single module(this changes are in the git stash currently), So I build the executables in both scenarios and copied them in the **download8** folder, one is called "unModule" and the other "dosmodulos", these were using JavaFx 21, and in a comparisson the "dosmodulos"(multimodule) seem to free memory more effiicently and this was even more noticeable when I switch to javafx 23, which is my third scenario and the folder is called 'dosmodulos23", I might want to check how this perform in a single module but with javaFx 23 but **best memory usage** out of this three was the last, multimodule with javaFx 23

When I return to work to this project the first thing I need to do is bring the single module app from the stash(don't run it from a terminal in intellj, just use an indepented teminal to avoid directories reordering issues), build it and then do some testing(only functionality available is navigating to standard and heteriogenity moduless, do it repetitively for a period of about 3 to 4 minutes, rezise the screen several time, do it wider, tighter, taller, smaller, you can not plot anything yet)

The best performance(multimodule app with javafx3) could free up from around 400MB back to 300MB aprox but very rarely a litlte bit lower than 300MB. In all three executables the app started at around 96MB to 105MB aprox and then increased to around 150MB to 180MB if I opened the two modules then increased to the the range of 220MB to 280MB and then here is where the behaviour was really different, the single module app could go up to 450MB maybe and then stay in the range of 350MB to 400MB. Multimodule with javaFx 21 will have similar behaviour but return to a lower value generally maybe around 330MB to 380MB, and then the best which is multimodule with JavaFx 23 can go from 460MB back to 300MB and even a little lower than 300 and seemed to freed up memory more often and to lower values

I added a function to resize the stage to the size of the scene, the scene size depend on its root size, so I'm not sure how this will affect the memory usage but setting the size from start should reduce the user need to reize the screen which at the same time should reduce the memory usage(this is a probability and an hipotesis only).

## Solution
I was actually not cappable to identify anything in the JFR recordings but is mostlikely because I still need to learn how to read the information in the recordings. I have pending to do more investigation to learn how to read the info better, also try to do a "heap dump". But since JFR was not being helpful I tried something new and got into fine tunning JVM by deffining the heap initial and max size, GC max pause time, thread max size, also choosing the right garbage collector, these settings where choosed after doing experimentation in two different computers as there is no deffined settings for a Java app and is actually suggested for you to experiment and find the best settings for your app

Initially only heap initial and max size and the garbage collector was deffined, the first initial and max size value was 200MB and the G1GC garbage collector, with these settings the app was working good and it reduced it size and it reached a max RAM usage of between 390MB and 460MB, however after investigating I found a newer GC called ZGC which reduced the app max RAM usage to valued between 310MB and 400MB, so this was working good but this was the behavior observed through the windows task manager and not JFR, that is why this I will consider doing some monitoring of the app with JFR as pending or TODO, and this behavior was observed in a Windows 11 Samsung computer with 16GB of RAM, and an intel i7 CPU, and the app worked great, of course I initially tried lower heap MAX sizes but the app either crashed at some point or was not able to complete task because the RAM was not suffucient, after this I got a new Dell computer with Windows 11 with 32GB of RAM and an "Intel(R) Core(TM) Ultra 9 185H   2.50 GHz" cpu, and here I started seing something weird, the app started with around 70MB to 80MB more than in the other computer, the reason why this happens is still not clear right now, and it stopped working at some point so I had to modify the heap values, I found out that 400MB as initial and max size was good enough and again the ZGC compiler was the best it reached a max of between 410MB and 500MB and in the previous computer all was working the same or similar way, the RAM usage was still similar as with the previous settings, I was worried my app was doing something wrong with the app so I created a very basic JavaFX app with the same Gradle configurations and observed the same behavior, the app's RAM usage in my previous computer was lower by, between, 60MB to 70MB in the Samsung computer, so here I confirmed it was not the application it is something that is related between Java itself and the hardware a JVM runs over. Following is a comparison, be aware that gradle configurations was the same in the project's gradle file

|  | Samsung(i7, 16GB RAM)| Dell(Ultra 9, 32GB RAM) |
|------|----|----|
| Very simple JavaFX app(single module project) app start | between 80MB - 90MB | Between 174MB - 178MB |
| HYU app start -|- between 120MB - 130MB | between 207MB - 220MB |
| HYU app max RAM usage reached | between 280MB - 310MB | between 410MB - 450MB |

They both still represent a drastic drop in RAM usage as originally it was using up to 1.5GB.

This is effect of the configurations on the JVM

* Initial and max heap size: I used the same values, this will avoid the overhead of changing the heap size on demand, and setting it to a proper value will make garbage collect more predictable as it should trigger garbage collections more often
* Thread max size: Not clear yet but as long as I define a max thread size that is enough for the app start, the max RAM usage will drop
* Garbage collector: The ZGC may come at the cost of some little more RAM than G1GC but it keeps max RAM usage lower than all other garbage collectors
* GC max pause time: I kept the default value of 200 milli seconds, this is the time the JVM has to pause all threads in the JVM to perform a full garbage collection if this time is too large the app will stop for too long if the garbage is too much, but this should not be a problem in our app, if it is too low it is unclear what consequences this implies to the performance at least to me as of right now, I would have to investigate more about the effects of this setting at large scale apps

# Commands used
* `./gradlew jpackage`(will create executable in the build folder inside jpackage directory)
* `./gradlew run`


# [Analysing a HEap Memory Leak](https://www.youtube.com/watch?v=JoQN4xoXY5Y)
Another interesting talk [here](https://www.youtube.com/watch?v=NI16bqeGv7U&t=550s) also.

First you need to understand how JVM manages memory, [this video](https://www.youtube.com/watch?v=vz6vSZRuS2M&t=2916s) explains it greatly

This example only analyses the heap usage and not other memory sections, this means we can not identify native memory exhaustion leaks using these methods, but at least analyzing the heap is great

## Java GC Visualizers/Analyzers
There are many like: GCPlot, IBM GCMV, GCeasy, GCViewer, SolarWinds Loggly, Sematext Logs. To use them you have to turn GC login on

Just be aware that jvisualvm is an all-purpose GUI-based monitoring tool. It doesn’t specifically monitor garbage collection, but shows memory usage over time graphically, which gives a good idea of whether the GC is working efficiently.

In this case we will use GCViewer, any GC log that your JVM produces you can load it into this tool, also load them live as they are generated using the UI you will have these options. Basically you can see the memory available in the heap and also the actual heap memory being used, also GC collections and how long they lasted, if you see the actual heap being used going up and down it most likely is because of the JVM using GC to collect young generation, when young generation is full a GC is triggered and it collects/deletes objects that nobody/nothing is referencing

Using a GC Analyzer will let answer the **"Do I have a leak?"** question which is important and can be a starting point

## JPS and JMAP Java Utilities
This tools will let us answer the **"What is leaking(which classes)?"** question

1. Run the `jps` command from your terminal, if you have the JAVA_HOME or the Java's bin directory on your PATH environment variable you can just execute it without the full address to the bin directory, this will give you the java processes list along with their ID number that are running in your computer

2. Run the `jmap -histo:live <java_process_id> > file1.txt` command in your terminal, again this tool is in the JDK's bin directory. This command will monitor the process so wait for a moment and interact with your if you need to make it do some processing that you can capture to analyze in a histogram, basically we are getting a histogram which is written in the `file.txt` file. You can open this file and see there the class names, the number of instances of each class and also the bytes all those instances sum up `[C` stands for char `[B` for byte and `[I` for integer primitives

3. You can take a second histogram and store in another file like Run the `jmap -histo:live <java_process_id> > file2.txt` and then use the bash utility called `perl` with the following command `perl file.pl file1.txt file2.txt > file.csv`, this will merge the files and make it easy for you to read. Remember if running on windows to use this utility you have to install "git bash"(git for windows). You should end up with a CSV that has five columns, first the class name as a key, second you have a pair of pairs, each pair is a combination of "number of instances" and "bytes used by instances" for the first take and then the second take pair. You should work with this CSV file and add two columns, one to find the difference of the number of instances of that object between the two takes and then the same but for number of bytes so you have the delta between the two takes and then you can create a pivot table from all this data and sort it by the "total number of instances" of each class, now it is a little hard to identify the leak but if the impact of a leak is very high it should be fair easy to identify it, this means if there is a memory leak causing a very bad impact you will se a lot of instances or bytes being created, if not an easy leak to identify or if everything is working good the difference between takes should be roughly the same or zero

## Heap Dump
Heap dump is basically a description of the heap at a certain moment in time and this will helps us answer **What is keeping objects alive(an instance in the app)?**

1. Enable heap dumps when out of memory errors occur using this argument `-XX:+HeapDumpOnOutOfMemoryError`

2. Use jmap `-dump:live,file=<file-path> <pid>`, you can remove the `:live` in the command which will let you see the dead objects in the histogram(not yet been garbage collected), if you use the `:live` part a garbage collection will be forced before the dump

3. Other way to do a heap dump JMX:com.sun.management.HotSpotDiagnostic.dumpHeap(), you can also do it from jconsole, visualvm, and even programmatically

4. Other way to do it is with the java utility `jcmd`, use command `jcmd <pid> GC.heap_dump <file_path>`

### Heap Dump Viewers
You need a profiler and some utilities for this. you can try "Ecplipse MAT". You can just load a heap dump using its UI. Just open it and it can analyze it and identify possible suspects. Eclipse MAT is a great tool that you can use to start drilling down to identify the instance in the app that is causing this problem

## Profiling
Any profiler that shows you the generations in the heap, should help you answer the question **Where is it leaking from(code where the objects are created and/or assigned)?**. In this case you can use "jvisualvm"

1. First identify the JVM process, click it

2. You should see some different tabs, "Overview", "monitor", "Threads", "Sampler", "Profiler", go to "Profiler", you will see more sections on your screen, to the right below the section with the those tabs you will another section with tabs, "CPU Settings" and "Memory settings", make sure "Profile object allocations and GC" and "Record Allocation Stack Traces" are checked and then click the button that says "Memory", which should be between "CPU" and "Stop" buttons, it will give pretty much similar numbers to the histogram but with an additional column called "Generations" this tells you how many age objects there are and not the age of the objects. It shows you dead objects but have not been garbage collected yet, for that go to the "Monitor" tab and click on "PerformGC" so dead objects are gone this will let you alone only with objects that are still alive, go back to "profiler", there might be a difference between the histogram you got from JMAP previously and the data, this depends on your configurations for example if you're tracking every 10 allocations and not every allocation and also this is a free tool so it is not perfect but it should do the job good enough.

3. Now you can right click any occurrence you see on your screen and, maybe any object with high live objects/live bytes and choose "Take a Snapshot and Show Allocation Stack Traces", for example you can check a "String" object details, there you will see the parts in the app that are contributing to the number of instances/bytes of the class you're analyzing, in this case String. Basically you can track the stack to see where in the code there is your bytes mostly being created
