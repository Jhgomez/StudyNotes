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

* Spring uses "Autowire" for dependency injection, "Spring Rest" for REST, "Spring Testing" for testing, to start you would learn CDI, JAX-RS, for testing "TestContainers" or "Arquilian"

## [Ergonomics JVM, Docker and Kubernetes](https://www.youtube.com/watch?v=M4j2Wn5cy7w)

These are concepts found in the video link inserted in the title

* when created java program assigns a default memory size and a max memory size, when default memory runs out the memory the default memory size will be increased in cycles repeating this behaviour until the max size is reached, besides this theres is also some aditional space called "meta space" in which byte code and native code produce by JIT are stored.

* Docker and podman environments/technolgies and similar use "cgroups" to manage memory this implies some requirements, which could be seveal(investigate or take this into account) like the kernel has support for cgroups. By default the containers don't suppor "cgroup" which seems not to be the case when installing a full Operating system like Linux distribution which mostlikely will suppor cgroup by default, without these tool, tools like HTOP, TOP and FREE will not detect the actual memory usage by applications we 

* Commands to run docker on Linux:
    * `docker run --name olinux --rm oracleLinux:8 bin/sh` this starts an oracle linux image. 
    * `docker run --name olinux --rm oracleLinux:8 free -m` this starts the container but show how much memory it used `free -m` is a linux command, FREE is a Linux tool for system monitoring
    * `docker run -m=100m --name olinux --rm oracleLinux:8 free -m`. This starts container with only 100MB of RAM


* In Linux we can use a concept called "Swap Memory" or "Swap Space" which is process that creates 'virtual RAM' this means that when physical RAM runs out the kernel will assign some hard drive memory to be treated as RAM. The space in the hard drive treated as RAM by the kernel is then called "Swap Space"

* TOP, HTOP, FREE are tools with the same purpos, help the user to monitor performance or resources and processes

* There is a problem when running a docker container 'from scratch', limit the memory that it can use and try to see the memory available inside it using FREE. Like in the section above even though the memory was limited, when monitoring the system it will read the whole memory available in the computer that this image is running on, this is because "cgroups" is not compatible by default in our images. This suppose another issue, when installing for example a java application, like our backend applications, when installed in the container the apps will set the default and max memory size based on the memory available in the computer running the whole procces instead of the container whihc is bad because the memory limit could have been set to a much lower value than what is available on the system which will cause and error if the Java app is started in the container. Generate the apps file, lets use the default project generated with the [Kukulkan archetype](https://github.com/tuxtor/kukulkan-ee?tab=readme-ov-file) which is a microprofile microservices framework, if we run `mvn clean package` will get a war, which is the file we used to use to run applications in an applications server like jboss, payara, weblogic, this practice has changed with Uber/fat jars which contains all dependencies the app needs to run which is basically what microservices is, each microservices has a server, data base, may load balancers, and communicate using a service mesh, in order to generate a uber jar from this project use `payara-micro` profile with this command `mvn clean package -Ppayara-micro`. To fix this, first we need to pack the jar file inside a container using a dockerfile, which is basically a sort of script, After Java 8.191 the JVM is able to recognize the "cgroups" memory to define the default memory and max memory at start, so we need to choose a Docker image with a proper Java version like a OpenJdk image and copy our jar file `COPY <jar file actual path> <path to copy file in image>`, invoke our application with `CMD ["java", "-jar", "./pathToJar.jar"]`, expose port `EXPOSE 8080`, build docker container image from cli `docker build . -f <dockerFileName> -t <aTagName>`, run it `docker run -p 8081:8080 -rm <tag>` port 8081 of localhost is mapped to 8080 of the image and using its tag name removes container when it is stopped. Run `docker ps` to see the running containers and a description, copy the alias of the container and enter the container with `docker exec -it <alias> /bin/sh` this will run the shell and now type unix/cli commands, `free -m` to see memory, you can exit cli with `exit` command and control+c to stop container. Run it again and limit memory `docker run -m=64mb -p 8081:8080 --rm <tag>`. `dmesg` is program in linux that helps us check things like errors, so you could see if the log if a container failed to run. We could limit java program initial and max memory by adding arguments `CMD ["java", "-Xms64m", "-Xmx128m", "-jar" , "./pathToJar.jar"]`, everytime you edit docker file remember to re build image, if this doesn't work try to find a command from your machine that will run, try it removing arguments or reordering them, when using old java versions we need to tune this parameters using manual methods meaning manual tests, we need to tune the default the max and/or default memory java argument with the limit stablished for the container with manual methods but this process is automated in newer versions
