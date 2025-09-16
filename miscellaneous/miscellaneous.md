## AI courses
_BEeYy.iv!ad4XJ

* Exploring Adversarial Machine Learning - tract_tarball.5i@icloud.com
* Fundamentals of Accelerated Computing with CUDA Python - ample_cubism8b@icloud.com
* Generative AI with Diffusion Models - umpire.5-pedants@icloud.com
* Getting Started with Accelerated Computing in CUDA C/C++ - pallor.seat_4v@icloud.com
* Getting Started with Deep Learning - stall-ruddier.0t@icloud.com
* Introduction to Deploying RAG Pipelines for Production at Scale - 29resist.cast@icloud.com
* Introduction to Transformer-Based Natural Language Processing - aisles-solder.8p@icloud.com
* Sizing LLM Inference Systems - scuba.liners.00@icloud.com

## Java Microservices Frameworks
* Payara, is server just like apache tomcat
* Microprofile, in [this repo](https://github.com/tuxtor/kukulkan-ee?tab=readme-ov-file) you an find an archetype to generate a project that sets up this framework along with Jakarta EE. This framework is capable to deploy applications that run in the CLI, this makes possible to execute our applications in Docker or Kubernetes or any other orchestator
* Spring
* Quarkus, is based on Microprofile. This framework is capable to deploy applications that run in the CLI, this makes possible to execute our applications in Docker or Kubernetes or any other orchestator
* Helidon, is based on Microprofile. This framework is capable to deploy applications that run in the CLI, this makes possible to execute our applications in Docker or Kubernetes or any other orchestator

### Note
Traditional/legacy frameworks had a Java Web server with several applications, which were packed as .war files, installed and hopped the server not to go down, however this approach changed with mircroservices, the frameworks that helps us creating this are listed above. However several traditional frameworks now allows apps to be organized across different servers/microservices. Java apps still are created as .war files but those .war files are packed along with its dependencies, uber/fat jars, so they can be run from the command line

#### Cual es el mejor?
[Source](https://tuxtor.shekalug.org/)

Personalmente tiendo a preferir Payara si necesito un servidor independiente, principalmente porque tengo considerable experiencia en Glassfish. Además, si necesito distribuir una aplicación simple en un fatjar, tiendo a usar Payara Micro o Apache TomEE .

Si necesito una arquitectura de microservicios, probablemente usaré Quarkus o Helidon .

Si necesito una función lambda, Quarkus seguramente.

## Backend Technologies

* OpenTelematry
* Htop, is not only for backend but helps monitoring for unix like systems, mostly for Linus
it would be the equivalent to Windows "Task Manager" but this is more powerful
* Java's Project Loom, aka virtual threads
* Java's Project Panama, native code execution, I think is better known as FFM(foreign function management) or FFI(foreign function interface), which should be similar to JNI(Java Native Interface) but I have to see what are the differences
* Java's Project Valhalla, Aims to reduce and simplify memory use
- Jbos and Glassfish is JAVA EE server


## Backend Standards

* Jakarta EE(AKA J2EE)

## Random Techonologies

* jni(from graalpy vid)
* truffle(from graalpy vid)
* SNI(server name indicator)
* JMX(Java monitoring extensions from springboot documentation)
* Servlet, this is a term. Is basically what 
* Picocli librearia for creating java or kotlin CLI applications, this could be used in backend
* Java performance with: Java Mission Control, Flight Recorder those are the main two, at least for me, but there is more like
Java VisualVM, Oracle Java Mission Control, JProfiler and JvisualVm. **JvisualVm** is a performance monitoring tool because it helps us visualize resources comnsumed by a java app, this was part of the GraalVm SDK APIs but it looks like it is not included anymore.
* Java RMI(Remote Method Invocation), here we see the term stub which is a class that a client uses
to communicate with a backed(Skeleton)
* JSP (Java Server Pages), Java inside html
* Linkerd is a service mesh
* Chaos Mesh tool to test a service mesh to the limit

## Linux/Unix Tools

* Monitoring: TOP, HTOP, FREE
* grep, searches text

## Random Notes

* `source ~/.bash.rc` would reload profile in unix like OSs/shells

* A Java EE stack would include Enterprise Java Beans, CDI, JPA, Ajax-RS

* Analysis of different frameworks to create java microservices. Spring by itself is an ecosystem because extensions for things like Kafka, Camel, Spark and whole lot more, practically anything, already exists, and spring has its own programming model. Microprofile on the other hand is a specification, is a standard, if you understand learn to use Microprofile you can program in frameworks like Redhat, Quarkus, Helidon, Apache Tommy, etc.
