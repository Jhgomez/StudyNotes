# Projects
These projects bring big changes in the JVM, they are develop over OpenJDK using JEPs(Java Enhancements Proposal) which at the same time have incubetors which is a way to divide all the work that needs to be done, the requirements might change throughout time but main goal should remain, be aware that a change can "fail", and every project represents a lot of analysis and experience from lessons learned from previous implementations

# Amber
New goals include generalizing records and pattern matching to apply to classes and even interfaces which will address some of the current restrictions of records, offer a refactoring path to classes and unblock withers

## New APIs/Concepts
* String templates: Still needs lot of work
* pattern-matching: There are two explorations that came out really well, Constant patterns(this is really interwined with primitive patterns). The second is "pattern assignments" which allow unconditional deconstruction of instances into their components

# Leyden


## New APIs/Concepts
* AOT(Ahead of Time) compilation: A JEP about this feature is not finished yet but starting Java 26 AOT cache contains loaded and linked classes as well as method profiles and now it will also contain machine code that the JIT compiler generated. In a production run this means the runtime can just pull optimized code out of the cache, thus considerably reducing warmup times. Be aware cache has little portability because high-performance code is bound to the exact hardware micro-architecture it was created and since it also contains the GC write barriers it is also bound to the GC, however the possiblity to make this cache portable is being explored(JEP 516) and in Java 25 you can try a preview feature that lets you use iterative trainning in which a firts run can be used to train the next run to build the cache all as one and in Java 26 you can make cache GC agnostic

# Babylon
At its core this project is currently working in "code reflection". Code reflection lets you do things like analyze, process, and change java code in a method or lambda which you can then run as java bytecode, or as a GPU kernel, and also as an SQL statement, actually it is said that you could run this code in whatever platform you want. This project is working in some POC(Proof of Concept) which use code reflection, one is running ML models on the GPU by adapating ONNX and the second is the same, running ML models, but this one by creating a GPU sympathetic JAVA API that transforms the code to a runtime like CUDA or OpenCL. Plans for 2026 are shipping code reflection as a incubator and publish a JEP on code reflection

## New APIs/Concepts
* Code Relfection

# Valhalla
Probably in java 28 we will have the JEP-401(Specifically Value Types) implemented, after this feature is delivered the next feature will be "nullness markers", this will allow the JVM identify instances of value types that cannot be `null` and, thus, can be flattened. After those changes further features/changes will deal with array imporvements amd the unification of primitives and their value class wrappers, but this is going to take time

## New APIs/Concepts
* Values Types

# Loom
Plans for 2026 in this project are basically to preview changes in the structured concurrency API and hopefully ship it this year also.

# Panama
Vector API(JEP 529) will benefit a lot from having "Value Types", from project Valhalla. Currently this project is not making much changes other than general improvements and regular maintenance, as mentioned the Vector API should be the next big change when value types are available

## New APIs/Concepts
* Vector API: This one is waiting on value types from valhalla
* Jextract: Java tool (part of the OpenJDK Code Tools project) that automatically generates Java bindings from native C/C++ header files. It works with the Foreign Function & Memory API (introduced in Java 19 and finalized in Java 22) so you can call native libraries without writing JNI code manually.
* FFM API: Basically a replacement for JNI
