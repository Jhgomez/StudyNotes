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

# Performance Tips
## Avoid recursion
Recursion is a technique that can be quick and effective in languages that provide tail call optimization. Java, however, is not one of these languages. Recursion is 
hence an expensive procedure. In most cases, you should choose an iterative solution utilizing loops over a recursive solution with Java. 

## Leverage StringBuilder
Java offers a bewildering array of options for combining shorter strings into longer ones, but most of these options follow a two-sequence approach to buffering a string into a long thread, adding significantly to the Java heap.  Because of this, memory duplication is required when an operator is initialized. Java has Stringbuilders that employ a one-sequence approach. 

The StringBuilder is a mutable asynchronous function that provides a string-like class that allows you to initialize an operator in a single sequence. StringBuilder doesn’t have any overhead from thread synchronization and is, therefore, the fastest way to build large strings from smaller pieces.

## Static Final
Avoid them as according to some comments [here](https://stackoverflow.com/questions/6470651/how-can-i-create-a-memory-leak-in-java) this could cause a memory leak

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
I'm testing theying to optimie HYU app memory usage, I created a copy of HYU app from zero, first with just the "Welcome Screen", from this I learned how to optimize images. Then I learnt the rezising issuge in a ScrollPane as noted in the "Observations" section. Then I added a "presentation"(Interaction Module) module, but no other layers modules from domain or data layer, then I moved everything to the single module(this changes are in the git stash currently), So I build the executables in both scenarios and copied them in the **download8** folder, one is called "unModule" and the other "dosmodulos", these were using JavaFx 21, and in a comparisson the "dosmodulos"(multimodule) seem to free memory more effiicently and this was even more noticeable when I switch to javafx 23, which is my third scenario and the folder is called 'dosmodulos23", I might want to check how this perform in a single module but with javaFx 23 but **best memory usage** out of this three was the last, multimodule with javaFx 23

When I return to work to this project the first thing I need to do is bring the single module app from the stash(don't run it from a terminal in intellj, just use an indepented teminal to avoid directories reordering issues), build it and then do some testing(only functionality available is navigating to standard and heteriogenity moduless, do it repetitively for a period of about 3 to 4 minutes, rezise the screen several time, do it wider, tighter, taller, smaller, you can not plot anything yet)

The best performance(multimodule app with javafx3) could free up from around 400MB back to 300MB aprox but very rarely a litlte bit lower than 300MB. In all three executables the app started at around 96MB to 105MB aprox and then increased to around 150MB to 180MB if I opened the two modules then increased to the the range of 220MB to 280MB and then here is where the behaviour was really different, the single module app could go up to 450MB maybe and then stay in the range of 350MB to 400MB. Multimodule with javaFx 21 will have similar behaviour but return to a lower value generally maybe around 330MB to 380MB, and then the best which is multimodule with JavaFx 23 can go from 460MB back to 300MB and even a little lower than 300 and seemed to freed up memory more often and to lower values

I added a function to resize the stage to the size of the scene, the scene size depend on its root size, so I'm not sure how this will affect the memory usage but setting the size from start should reduce the user need to reize the screen which at the same time should reduce the memory usage(this is a probability and an hipotesis only).


# Commands used
* `./gradlew jpackage`(will create executable in the build folder inside jpackage directory)
* `./gradlew run`
