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
//        "-XX:StartFlightRecording=duration=6s,filename=myrecording.jfr",
//        "-XX:+UseParallelGC",
        "-XX:+HeapDumpOnOutOfMemoryError",
    )
}
```

You can specify more options with the parameters defined [here](https://docs.oracle.com/javacomponents/jmc-5-4/jfr-runtime-guide/comline.htm#BABGCBBA), for example, remember you can define a template used to defined what events or information you want to record and there is already two predeifined templates(default and profile, being profile a more detailed record), you can create your own but it might be easier to do it using JMC as it is more graphic, I would like to make sure a `profile` recoding is being made, so I define the following argument
```
"-XX:StartFlightRecording=duration=6s,filename=myrecording.jfr,name=profile"
```

Now just open JMC and open the recording file from it

##### Start a JFR recording When App is running
We will use the java utility called `jcmd`, you might want to add it to your OS path this way you don't have to navigate to the JDK's `bin` directory to be able to run this app.

1. Run your app any how you want
2. Get the process id by running from the command line the command `jcmd`, this will print all running java processes, identify yours(it should be easy) and copy the ID
3. `jcmd 10828 JFR.start duration=3s filename=flight2.jfr name=profile`
4. You can add more configurations to the start command as mentioned in a link in the prev section

# Other Performance Tools
* JProfiler
* Glowroot
* Sematext
* Dynatrace

# Performance Tips
## Avoid recursion
Recursion is a technique that can be quick and effective in languages that provide tail call optimization. Java, however, is not one of these languages. Recursion is 
hence an expensive procedure. In most cases, you should choose an iterative solution utilizing loops over a recursive solution with Java. 

## Leverage StringBuilder
Java offers a bewildering array of options for combining shorter strings into longer ones, but most of these options follow a two-sequence approach to buffering a string into a long thread, adding significantly to the Java heap.  Because of this, memory duplication is required when an operator is initialized. Java has Stringbuilders that employ a one-sequence approach. 

The StringBuilder is a mutable asynchronous function that provides a string-like class that allows you to initialize an operator in a single sequence. StringBuilder doesn’t have any overhead from thread synchronization and is, therefore, the fastest way to build large strings from smaller pieces.





Avoid Creating New Stages Frequently
Unless you really need multiple OS-level windows, avoid using new Stage. They create new rendering pipelines and memory contexts. Creating new Stage and Scene objects every time you switch screens prevents JavaFX from reusing internal rendering buffers, leading to repeated allocation

Stick to swapping views or changing root nodes.



https://docs.oracle.com/javacomponents/jmc-5-4/jfr-runtime-guide/comline.htm#JFRUH188
https://docs.oracle.com/en/java/java-components/jdk-mission-control/9/user-guide/using-jdk-flight-recorder.html#GUID-D38849B6-61C7-4ED6-A395-EA4BC32A9FD6


https://www.reddit.com/r/JavaFX/comments/uxg99y/javafx_and_switching_scenes/?rdt=50676


https://forums.oracle.com/ords/apexds/post/how-to-free-the-memory-after-closing-javafx-stage-8830
https://moldstud.com/articles/p-10-bizarre-bugs-encountered-by-javafx-developers-and-how-to-fix-them
https://codingtechroom.com/question/javafx-resource-cleanup



https://javanexus.com/blog/mastering-dependency-injection-javafx-dagger
https://www.pragmaticcoding.ca/javafx/swap-scenes
