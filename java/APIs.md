## JNDI Java Naming and Diretory Interface

### When is it used?
While JNDI plays less of a role in lightweight, containerized Java applications such as Spring Boot, there are other uses. Three Java technologies that still use JNDI are JDBC, EJB, and JMS. All have a wide array of uses across Java enterprise applications.

Also when used with `ClassLoader`s. However, sometimes when JVM core classes need to dynamically load classes or resources provided by application developers, we might encounter a problem.

For example, in JNDI, the core functionality is implemented by the bootstrap classes in rt.jar. But these JNDI classes may load JNDI providers implemented by independent vendors (deployed in the application classpath). This scenario calls for the bootstrap class loader (parent class loader) to load a class visible to the application loader (child class loader).

J2SE delegation doesn’t work here, and to get around this problem, we need to find alternative ways of class loading. This can be achieved using thread context loaders.

The java.lang.Thread class has a method, getContextClassLoader(), that returns the ContextClassLoader for the particular thread. The ContextClassLoader is provided by the creator of the thread when loading resources and classes. As of Java SE 9, threads in the fork/join common pool always return the system class loader as their thread context class loader.
