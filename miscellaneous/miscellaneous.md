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

* Java versions after 8.191 handles a concept called [ergonomics](https://docs.oracle.com/en/java/javase/23/gctuning/ergonomics.html) which is very helpful when runnig/deploying java applictions in containers, we can print the default configurations by printing flags with command `java -XX:+PrintFlagsFinal -version | grep ergonomic` here we are using command line utility called "grep" to find text, this means the 

* Even though we can use ergonomics there might be cases when we want to tune the memory size values like when using Kafka, camel and spark you may tune it to use around 5 to 10 gigabytes.

* Cgroups + ergonomics is safe, it will use cgroups info to determine the limit. Be aware that if for some reason we create/modify something like a JVM plugin to try to access memory outside what is managed by cgroups but this will generate an exception in the kernel and cgroups will kill the process, ergonomics will also safely use CPU resources by creating a Thread Pool with the correct size and/or limits.

* If we need to determine/tune memory sizes limits manually we can combine tools like "JMeter" to simulate workloads, java profiler like "YourKit", in combination or alternativaly with "JVisualVm", and finallly analize JVM telematry data.

* Tunning memory sizes manually is also required in old Nodejs versions, check "Node.js in Kubernetes World", it is an IBM article. NodeJs is similar to Java's in the sense how it calculates the memory size. This, again, happens because a heap is created with memory that is beyond what "cgroup" allows

* Oracle JVM after version 8.202 when used in production environment has to be used with a paid license. In AWS and Azure you can use their JVM implementation and avoid beingh charged by not using Oracle's JVM. Android Studio and Intellij has their own JVM which is compiled by Belsoft

* To avoid wasting memory in context like server applications Java is now modular, that is why javafx, awt, swing is not part of the JDK. GraalVM is not part of the JDK either, the native applications it can produce are important because in some cases it is more important how fast the app can start but not the peak performance, so we are gaining with AOT compilation but loosing benefits of peak performance of JIT compilation

* Helidon, Quarkus, Micronaut and Spring Native are Java frameworks that aims to create web applications that has a quick start and use less memory. These frameworks starts the apps fast and were created with the Docker and Kubernetes era

* In linux any OpenJdk version works good, so you can use the one that is installed by default. In Windows, AdoptOpenJdk is a great option because it runned by IBM, in mac this openJdk implementation is available in homebrew

* Native apps compiled and packed with GraalVm are packed with Sulong, which is a mini virtual machine which is the VM that the app is executed on top on


## [DevSecOps: Kubernetes + OPA](https://www.youtube.com/watch?v=FRHkATZUf_k)
It demoes how to use OPA as admission controller to Kubernetes, OPA is Open Policy Agent


# More

* CISA - cybersecurity and infrastructure security agency, they have a catalog which is important in cybersecurity as it describes systems vulnerabilities and is called "Kown Exploited Vulnerabilities Catalog"

* Aaron Swartz: Self-taught programmer, founder of reddis and helped to develop RSS protocol, RSS protocol is not used a lot these days  but it lets you "subscribe" to websites and get new content from them, it looks like it might still live inside some of googles products like YT. He commited suicide. [ https://archive.org/details/firmwarelibrary]

* llya Sutskever, cofounder of OpenAI

* https://archive.org/details/firmwarelibrary

* Gimp is image editor it can be comparable to Photoshop but it is open source and free

* lftp is a GNU program/command in Linux that lets you mirror a folder in a remote computer

* JSTOR - Journal storage, it is a scientific journal

* PERL: high level programming language

* Directory Listing: Web server function that displays contents of a directory that has no index file. It considered a security vulnerability if not configured correctly, wordpress websites has this issue

* Wordpress activates an API by default, you should turn it off

* You can see a website source code by putting `view-source:`

* Cloudflare can help you implement a rate limit

* [C++ is a blast, games approach](https://learncodethehardway.com/blog/31-c-plus-plus-is-an-absolute-blast/)

* FedCM(Federated Credential Management)

* String Interpolation

* Kotlin coding conventions tells about backing properties

* Watson Studio - IBM tool for building AI LLM models

* Gradio is the fastest way to demo your machine learning model with a friendly web interface so that anyone can use it, anywhere!

# TODO

* Caching mechanisms for web servers
* Database query optimizations
* Resource pooling
* Response compression
* Http caching headers

## Monitoring

* Opentelemetry used to make software observable, telemetry are the measurements and data at remote points and their automatic transmission to receiving equipment for monitoring. Telemetry data can include traces(path from point A to point B. trazados se refiere al camino que se recorre desde un punto A a un punto B. lifecycle of requests to a system), logs(detailed debugging info emitted by processes) and metrics(summary statistics)
* Instrumentation code is "how" we get telemetry
* Distributed tracing tools: OpenCensus, Open Tracing
* instrumentation refers to the measure of a product's performance, to diagnose errors, and to write trace information.
* OpenCensus + OpenTracing = OpenTelemetry. Opencensus Provides APIs and instrumentation that allow you to collect application metrics and distributed tracing. OpenTracing Provides APIs and instrumentation for distributed tracing. OpenTelemetry is An effort to combine distributed tracing(lifecycle of requests to a system), metrics(summary statistics) and logging(detailed debugging info emitted by processes) into a single set of system components and language-specific libraries.
* Jaeger(golang) performance insights, known for providing distributed tracing, it can be added to LinkerD
* Prometheus time-series db for monitoring metrics,  enabling system monitoring and alerting
* LinkerD + Flagger(kustomize) to do canary deployments. LinkerD is a service mesh, it doesn't provide and ingress so you have to get one like Nginx. [More on LinkerD](https://cloudnativenow.com/topics/cloudnativedevelopment/what-is-service-mesh-and-why-do-we-need-it/)
* A network sniffer, also known as a packet analyzer, is either software or hardware that can intercept data packets as they travel across a network. Admins use network sniffers to monitor network traffic at the packet level, helping ensure network health and security.
* Istio is another service mesh, it already provides and ingress called emboy
* Golden Metrics are 1) Latency: time it takes to service a request, 2) Traffic: how much demand is being placed on a service 3) Error: rate of requests that fail 4) Saturation: How full is the service, measures system utilization, emphasizing the resources that are most constrained. These are the metrics we should aim to get with Telemetry and observability so we can monitor and analyze them
* Another popular alternative to make your system observable is ELK
 
### Metrics
* Gauges: e.g CPU utilization
* Cumulative counters: e.g request counts
* Cumulative histograms: Grouped counters for ranges, e.g. 0-10ms, 11-20ms
* Rates: Typically is a derivate of a counter e.g. requests per second
* Aggregation by tags: Data joined along shared tags, e.g. hostname, cluster name

### Tracing
* Span: Includes operation name, start and finish timestamps, parent span ID, span ID
* Trace: Directed acyclic graph of spans where the edges between spans are defined as parent/child relationships
* Distributed Context: Its the tracing IDs, tags, and options that are propagated from parent to child spans

## More
* Rancher: container management platform. Makes easy to run Kubernetes everywhere. Also helps you manage Kubernetes cluster
* Traefik: Is an open-source Application Proxy that automatically discovers and routes requests to your services
* Meshery: Lets you install the service mesh in Kubernetes clusters using a dashboard interface
* Fault injection is a testing technique for understanding how computing systems behave when stressed in unusual ways.
* Logrocket vs Datadog
* For more technologies by architecture components search for [cncf landscape](https://landscape.cncf.io/)
* Hadoop: Is a collection of software used in distributed computing
* io Uring: Linux Kernel syscall interface designed for asynchronous I/O operations, addressing performance issues with traditional interfaces like read()/write() or aio_read()/aio_write()
* Java Jextract: Is a Java API that lets you extract a C 
* Java Foreign Function and Memory(FFM): This API enables Java programs to interoperate with code and data outside the Java runtime. This API enables Java programs to call native libraries and process native data without the brittleness and danger of JNI. The API invokes foreign functions, code outside the JVM, and safely accesses foreign memory, memory not managed by the JVM.
* Java Language Summit: Is a great educational resource about Java
* Java Intersection Types: Is a type that combines two types, this is done using generics
* meliorator software: AI enabled bot farms
* VMWare Network modes: Bridged(When you need the VM to act as a real device on the network. No so safe for testing suspicious or malicious software), NAT(When you need internet access but don’t want the VM exposed. More secure when testing suspicious software), Host-Only(When you need an internal test network. Can not communicate with the internet, it can only communicate with host and other VMs)
* Server Driven UI
* java service loader
* Network link conditioner
* scp/secure copy, is a command/utility in Linux is used to securely copy files and directories between two locations using SSH for authentication and encryption
* javax.sql.datasource - alternative to `drivermanager` to interact with databases https://www.youtube.com/watch?v=-tcxX-beP3c
* Jboss server, application server designed for building, deploying, and hosting highly transactional Java applications and services. supports Java EE standards, making it cross-platform and compatible with any operating system that supports Java.
* Java OSGi, whenever we have to guarantee that a single application has to be updated without any disservice, OSGi can be a viable solution. Implementations can be Apache Felix, Apache Karaf(based on Apache Felix). demo video https://www.youtube.com/watch?v=LfMS7XzwxpU using maven modular app. https://github.com/edvin/tornadofx/wiki/OSGi
* [Using OSGi in a desktop standalone application](https://stackoverflow.com/questions/8518837/using-osgi-in-a-desktop-standalone-application)
* [Building Pluggable Swing Modules with OSGi](https://www.javacodegeeks.com/2025/07/building-pluggable-swing-modules-with-osgi.html)
* [How to Run HTML File on Localhost](https://devpractical.com/host-a-html-page-on-localhost/)
* [Deploy a Static Website on GCP](https://www.youtube.com/watch?v=yv_gpBE_AbM)
* [Malware Analysis tools](https://www.youtube.com/watch?v=J9I-Sewaihs&t=58s) like "bintext" scans strings in an executable "PEId" tells you what language an executable was written in or was compiled with and what kind of file it is. [Practical Malware Analysis](https://samsclass.info/126/126_S25.shtml)
* Hex Editor: this tools lets you examine the strings in any file it can be an executable
* [BSP trees](https://www.youtube.com/watch?v=_t4ijMAsCU8&t=1s): Binary space partitioning trees are a form of geometric decision trees. BSP trees uses planes to subdivide space into regions that are either inside the object or outside the object so it carves up space a opposed to the standard boundary representation which just defines a surface and doesn't really say anything explicitly about the 3D space per se, you can draw inferences from that surface about the space but you don't have an explicit representation of the space. The other thing that is different about BSP trees is that it gives you a solid representation as opposed to just a surface representation and with that you are able to do set operations and support the semantics of solids. Another important property in BSP trees is visibility, the painters algorithm helps get the correct rendering of opacity in graphics that use BSP trees, by testing the location of the viewer with respect to a first plane(the side of a cube for example) you can order other objects in the space, that way the program knows who to draw first and who second. BSP trees can represent any piecewise-linear object(made with piecewise-linear functions) which are generally called polytopes or polyhedral, it can represent a set of them within a genus(search for "genus in computer graphics") and can be non-manifold(edges shared by more than two faces in 3D geometry) and 2D semi-infinite and it doesn't matter, it can handle it because you have only one tree representing all the figures. In order to do transparency you must have and ordering on the faces you can't just use a z-buffer, this way you can see how an object/geometric figure is inserted inside another object, this means you must order the faces, and because you can order faces from nearest to farthest you can simulate transparency. Another important aspect for having visibility ordering is to enable occlusion culling. This approach was invented by "Bruce Naylor" however it seems to be other alternatives more performant than this, however it all depends on your use case a comparison with the alternatives is below. Some of his work is [Sculpt : an interactive solid modeling tool](https://www.researchgate.net/publication/242609970_Sculpt_an_interactive_solid_modeling_tool), his approach was using CSG with BSP trees however in a CAD application it seems to be that it is more used the B-Rep with NURBS(used for curves) at least parasolid modeling kernel uses it, one CAD app using that kernel is `Plasticity`, another options is `Blender` but that uses polygonal meshes
* texture mapping, basically lets you display an 2D image in or color in a 3D model, this helps simulate material very easily
* ray tracing, vertex processing vs rasterization processing in modern GPUs
* B-Rep(binary representation) vs CSG(Constructive Solid Geometry), (this)[https://www.pre-scient.com/knowledge-center/geometric-modelling/brep-csg/] is a good comparison between B-Rep and CSG, both are techniques to do Solid Geometric Modeling/Solid Modeling, in here we will learn that CSG has some limitations like not being able to represent fillets, chamfers, and other context-based features. B-rep is a form to express solid models, so it is CSG, solids are described as a collection of connected surface elements.
* [Precise Construction and Control of Implicit Fillets in the BlobTree](https://webhome.cs.uvic.ca/~blob/publications/filletSMI10.pdf) blob trees are known for how easy is to create fillets but they lack the ability to represent sharp edges like in CSG. However in this article it is show that is actually possible to get the advantages to create sharp edges in BlobTrees and at the same time leverage the ease of creating fillets
* [Comparing Spatial Partitioning Methods | Octree, Kd tree, & BSP tree](https://github-wiki-see.page/m/SlaggyWolfie/slaggy-engine/wiki/Comparing-Spatial-Partitioning-Methods-%7C-Octree%2C-Kd-tree%2C-%26-BSP-tree), in this document according to them the least efficient method is BSP. BSP-Trees have the drawback that you may have to split your geometry into smaller pieces. This can increase the overall polygon-count of your data-set. They are nice for rendering, but they are much better for collision detection and ray-tracing
* BlobTree vs CSG, could not find a versus but we already know a little about CSG, so we just need to understand BlobTree better, for that you can check [Extending the CSG Tree. Warping, Blending and Boolean Operations in an Implicit. Surface Modeling System](https://perso.liris.cnrs.fr/eric.galin/Articles/1999-blobtree-model.pdf) and [Efficient Data-Parallel Tree-Traversal for BlobTrees (revised)](https://webhome.cs.uvic.ca/~blob/publications/gdspm.pdf)
* BlobTree vs CSG vs B-rep in CAD applications, all these options lets you do Solid Modeling, however it seems like BlobTrees is not the best option in the context of CAD because even though they make very easy to create precise curves/blends/fillets and procedural shapes, look [here](https://webhome.cs.uvic.ca/~blob/publications/filletSMI10.pdf), modeling kernels have been using B-rep with NURBS too long now so moving to this approach can be considered and area of experimentation, CSG is a good concept but remember it has its limitations in representing things like fillets and chamfers, so CAD actually uses Modeling Kernel/Geometric Kernel/Geometric Modeling Kernel and these tools/libraries uses B-rep with NURBS as shown [here](https://old.opencascade.com/doc/occt-7.4.0/overview/html/technical_overview.html), at least OpenCascade and Parasolid works this way, I'd have to investigate C3D and ACIS kernels to confirm
* Plasticity vs Blender, plasticity uses Parasolid modeling kernel as shown [here(What is a Geometry Kernel? C3D vs ACIS vs Parasolid)](https://www.youtube.com/watch?v=WvwiH1DOK1M), this allows it to use mathematics to do very complex solid modeling, makes it very powerful and dynamic, this kernel mostlikely uses b-rep and NURBS(used to draw exact/precise curves and surfaces). Blender uses polygonal meshes. You can check a review [here, Why I don't use Plasticity](https://www.youtube.com/watch?v=Lgc8EadiHNI)
* Sistema Lorenz, es un sistema de caos, su grafica tiene forma de mariposa(atractor de Lorenz)
* visibility in computer graphics
* sigmoidal curve, Bezier curve
* BLOB stands for Binary Large Object. It refers to a collection of binary data stored as a single entity in databases or cloud storage systems. Blob storage is primarily used for storing unstructured data, such as multimedia files (images, videos, audio), backups, logs, and other large datasets. Amazon S3 can be considered a blob database/storage, google drive can be considered blob storage as well
* noise maps in java(Minecraft)
* FFmpeg: open-source software to record, convert and stream audio and video.

# Databases

* Conceptual layer requires an entity-relation model
* Logical layer requires a relational scheme
* Physical Layer requieres a 


# Markdown cheats
```
<a href="#download">![Download APK](https://img.shields.io/github/downloads/SkyTubeTeam/SkyTube/total.svg?label=SkyTube+Extra+Downloads)</a>
<a href="https://hosted.weblate.org/engage/skytube/?utm_source=widget"> <img src="https://hosted.weblate.org/widgets/skytube/-/svg-badge.svg" alt="Translate"/> </a>

<p align="center">
  <a href="#features">Features</a> | 
  <a href="#download"><img src="https://i.imgur.com/BYKw7FK.png" />Download</a> | 
  <a href="#why-skytube">Why SkyTube?</a> | 
  <a href="#screenshots">Screenshots</a> | 
  <a href="#contribute">Contribute</a> | 
  <a href="#translate">Translate</a> | 
  <a href="#license">License</a>
</p>
```
