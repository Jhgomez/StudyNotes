# Java APIs Found in [FXLauncher](https://github.com/edvin/fxlauncher/tree/8d8aa93f1bd1f676f9d72773b30e495e93a346ff)
FxLauncher is a library for JavaFx that lets you upload files to a server using some of the bellow Java APIs and also, it uses the Linux command/utility called secure copy `scp` to copy files to a remote server usings SSH.

## JNDI Java Naming and Diretory Interface

### When is it used?
While JNDI plays less of a role in lightweight, containerized Java applications such as Spring Boot, there are other uses. Three Java technologies that still use JNDI are JDBC, EJB, and JMS. All have a wide array of uses across Java enterprise applications.

Also when used with `ClassLoader`s. However, sometimes when JVM core classes need to dynamically load classes or resources provided by application developers, we might encounter a problem.

For example, in JNDI, the core functionality is implemented by the bootstrap classes in rt.jar. But these JNDI classes may load JNDI providers implemented by independent vendors (deployed in the application classpath). This scenario calls for the bootstrap class loader (parent class loader) to load a class visible to the application loader (child class loader).

J2SE delegation doesn’t work here, and to get around this problem, we need to find alternative ways of class loading. This can be achieved using thread context loaders.

The java.lang.Thread class has a method, getContextClassLoader(), that returns the ContextClassLoader for the particular thread. The ContextClassLoader is provided by the creator of the thread when loading resources and classes. As of Java SE 9, threads in the fork/join common pool always return the system class loader as their thread context class loader.

## Class Loaders
A class loader is an object that is responsible for loading classes. Further, class loaders load Java classes dynamically to the JVM (Java Virtual Machine) during runtime. They’re also part of the JRE (Java Runtime Environment). Therefore, the JVM doesn’t need to know about the underlying files or file systems to run Java programs thanks to class loaders.

Furthermore, the JVM doesn’t load these Java classes into memory all at once, but rather when an application requires them. This is where class loaders come into the picture. They’re responsible for loading classes into memory.

### Use Cases
Custom class loaders are helpful for more than just loading the class during runtime. A few use cases might include:

Helping to modify the existing bytecode, e.g. weaving agents
Creating classes dynamically suited to the user’s needs, e.g. in JDBC, switching between different driver implementations is done through dynamic class loading.
Implementing a class versioning mechanism while loading different bytecodes for classes with the same names and packages. This can be done either through a URL class loader (load jars via URLs) or custom class loaders.
