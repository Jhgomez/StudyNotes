# JDK Performance Monitoring Utilities
The bin folder contains the following programs that can be used for profiling and monitoring:

* Java ViusalVM: It used to be part of the Oracle and Open JDK distributions in the past but that changed after JDK 9 since it is no longer included and has to be downloaded separately
* JConsole
* Java Mission Control
* Diagnostic Command TOol

## Java Flight Recorder
This is just another monitoring program but I will focus on it because I want to use it to monitor my apps. This isn't a standalone program. Its usage is closely related to two tools, "Java Mission Control" and "Diagnostig Command Tool"

JFR collects information about the events in a Java Virtual Machine (JVM) during the execution of a Java application. JFR is part of the JDK distribution, and it’s integrated into the JVM. JFR is designed to affect the performance of a running application as little as possible.

In order to use JFR, we should activate it. We may achieve this in two ways:

1. when starting a Java application, from the command line. 
2. passing diagnostic commands of the jcmd tool when a Java application is already running

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
I'm using a modular/multi module JavavaFx Windows Desktop application with several gradle modules and as mentioned in prev notes there is three ways to start a trace/recording, on application start and on demand(while application is running any moment). The data that records capture are events, they can be of different four types:

* **Duration Events**: they have duration, a start and stop time
* **Instant Events**: WHen it ocurrs it gets instantly logged, for example, when a thread gets blocked
* **Sample Events**: THeir purpose is to check the health of the system, they are logged on time intervals previously specified, for example, printing heap diagnostics every minute
* **Custom Events**: These events are created by the user using JMC or other APIs, for example starting a trace on starting a certain function call and stoping the trace on function complete

In addition, there are predefined events that are enabled in a recording template. Some templates only save very basic events and have virtually no impact on performance. Other templates may come with slight performance overhead and may also trigger garbage collections to gather additional data. The following templates are provided with Flight Recorder in the <JDK_ROOT>/lib/jfr directory:

* **default.jfc: Collects a predefined set of data with low overhead.
* **profile.jfc: Provides more data than the default.jfc template, but with overhead and impact on performance.

Flight Recorder produces following types of recordings:

* **Time fixed recordings(the one I needed in my case because of what the use cases for it can be as described below)**: A time fixed recording is also known as a profiling recording that runs for a set amount of time, and then stops. Usually, a time fixed recording has more events enabled and may have a slightly bigger performance effect. Events that are turned on can be modified according to your requirements. Time fixed recordings will be automatically dumped and opened.

  Typical use cases for a time fixed recording are as follows:

    * Profile which methods are run the most and where most objects are created.

    * Look for classes that use more and more heap, which indicates a memory leak.

    * Look for bottlenecks due to synchronization and many more such use cases.

* **Continuous recordings**: A continuous recording is a recording that is always on and saves, for example, the last six hours of data. During this recording, JFR collects events and writes data to the global buffer. When the global buffer fills up, the oldest data is discarded. The data currently in the buffer is written to the specified file whenever you request a dump, or if the dump is triggered by a rule.

  A continuous recording with the default template has low overhead and gathers a lot of useful data. However, this template doesn't gather heap statistics or allocation profiling.

##### Start a JFR recording on Application Start

1. [Download Java Mission Control 9](https://www.oracle.com/java/technologies/javase/products-jmc9-downloads.html)
2. Decompress the file and find the application called `jmc.exe`
3. 

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
