# JDK Performance Monitoring Utilities
The bin folder contains the following programs that can be used for profiling and monitoring:

* Java ViusalVM: It used to be part of the Oracle and Open JDK distributions in the past but that changed after JDK 9 since it is no longer included and has to be downloaded separately
* JConsole
* Java Mission Control
* Diagnostic Command TOol

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
