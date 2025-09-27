# Java EE/Jakarta EE vs Spring Framework vs Spring Boot

## JAVA EE/Jakarta EE
Java EE extends Java SE with specifications for enterprise features such as distributed computing and web services. Java SE is used for General-purpose programming. Java EE Enterprise-level and large-scale applications and Includes APIs for web, enterprise and cloud applications.

Java SE(Standard Edition) key features are:
* Core Libraries: Provides fundamental libraries such as java.lang, java.util, java.io, and java.nio.
* Swing and AWT: Offers APIs for creating GUI-based desktop applications.
* Networking: Includes APIs for building network-based applications.
* Concurrency: Supports multithreading and concurrent programming through java.util.concurrent.
* JDBC: Java Database Connectivity (JDBC) for database interactions.

Common Use Cases of Java SE:
* Desktop applications
* Console-based applications
* Utilities and tools, such as file editors and parsers
* Educational tools for learning programming

Key Features of Java EE:
* Servlets and JSP: Used for building web applications.
* Enterprise JavaBeans (EJB): A framework for developing scalable and secure enterprise-level applications.
* JPA (Java Persistence API): Simplifies database interactions using Object-Relational Mapping (ORM).
* JMS (Java Messaging Service): Supports asynchronous messaging for enterprise systems.
* Web Services: Provides support for RESTful and SOAP-based web services.
* RESTful web services (JAX-RS)

Common Use Cases of Java EE:
* E-commerce websites
* Banking applications
Enterprise Resource Planning (ERP) systems
Customer Relationship Management (CRM) systems
Complex distributed systems requiring scalability, security, and transaction management

Typically, you would need an application server/container, like "Apache Tomcat", "Glassfish", "Payara", to run a Java EE HTTP server. Java EE applications rely on the infrastructure provided by application servers to manage components like servlets, EJBs (Enterprise JavaBeans), JSPs (JavaServer Pages), and other enterprise features.

If your HTTP server uses only servlets(servelets seem to be "endpoints"/"services" and are under control of the Servlet Container) and does not rely on the full Java EE stack (like EJBs, JMS, etc.), you could technically run it using a servlet container like Tomcat or Jetty, which are lighter-weight options.

But if you're using full Java EE features, like EJBs, JPA, or any other enterprise component, you would need a more complete application server (e.g., WildFly, GlassFish).

These containers are runtime environments that manage the lifecycle, deployment, and execution of Java EE components. They provide essential services such as security, transaction management, and resource pooling. 

## Spring Framework
Is the application development framework for JavaEE. It’s an open-sourceThe. Its core feature is developing any Java application and this targets to make J2EE development easier to use. It enables developing enterprise-class applications using POJO (Plain Old Java Object).

While it does not use Java EE under the hood, it is based on Java EE specifications and is designed to work with them. Spring provides a flexible and modular architecture, allowing developers to build applications using Java EE technologies while leveraging the benefits of the Spring Framework. Spring is slower than JavaEE.

All REST API has to be deploy to a server, same as Java EE. You have to run your application inside a Servlet container (like Tomcat) or an application server like WildFly or WebLogic, depending on your use case. However, you can still configure your own embedded servlet container if you want to avoid a large application server.

You don’t need a full Java EE/Jakarta EE application server to run Spring applications. The Spring Framework is not dependent on an application server for things like servlets, transaction management, or dependency injection. It can work on its own, with either an embedded or external web server.

In this context as well as in Spring Boot context Controllers are what you'd call Servlets in Java EE. In spring framework you have to annotate your controllers and this will make them available to the IOC container, that you can access through "Front Controller" who then access the "Dispatcher Servlet" and this last one has access to the "application context" which can be seen as a container that has all existing contollers and this is basically how the front contoller directs incoming requests to the right controller, but you have to register your controllers inside a "configuration file" which is responsible to scan for all existing controllers. There can be many "Front controller"s and each is attach a URL pattern and is the base to all paths/endpoints/services indicated by each controller, each dispatcher servlet will have its own config file and there a IOC container. Configuration files are basically Java classes that you have to annotate, also a dispatcher servlets are Java classes but this one has to extend some class I won't mention here for simplicity

## Spring Boot
Is an extension of the Spring Framework that aims to simplify the development of Spring applications, and it is built on top of Spring Framework. It provides a set of conventions and defaults to reduce the amount of configuration required, in Spring Framework you have to configure things like the dispatcher servlet, view resolvers, and security settings

Spring Framework is suuitable for complex applications that require fine-grained control over configuration and components.

Spring Boot is ideal for microservices and rapid application development, where simplicity and speed are essential

while the Spring Framework provides a comprehensive set of tools for building Java applications, Spring Boot simplifies the process by reducing configuration and providing sensible defaults. Spring Boot is built on top of the Spring Framework and is not a replacement but rather a complement to it

No need for an application server; you can run an embedded web server (e.g., Tomcat, Jetty).

It is great to understand Spring Framework before Spring Boot, and a great comparisson between these two with an introduction to Spring Framework can be found [here](https://www.youtube.com/watch?v=F_rGkDeihBg&t=3s)

# URI vs URL
Before talking about APIs to create http client and http servers, we need to know the difference between URI and URL, Every URL is an URI but not every URI is an URL, you could say URI is the parent of URL. URI contains the following parts

* scheme − for URLs, is the name of the protocol used to access the resource, for other URIs, is a name that refers to a specification for assigning identifiers within that scheme
* authority − this part is comprised of user authentication information, a host and an optional port
* path − it serves to identify a resource within the scope of its scheme and authority. Sometimes refered to as file or filename if dealing with resources and not services.
* query − additional data that, along with the path, serves to identify a resource. For URLs, this is the query string
* fragment − an optional identifier to a specific part of the resource. Also known as reference

```
  protocol://host:port/path?query#ref
  https://www.amrood.com/index.htm?language=en#j2se
```

It is said that URI describes where a location, URL also describes a location but also how to access it(by specifing the protocol like ftp, http, https, gopher, mailto, news, nntp, telnet, wais, file, or prospero), also a URL works over the network, it retrieves resources or services over the network

# ServerSocket, Socket, URL, URLConnection, HttpURLConnection, DatagramSocket, HttpClient, HttpServer
You can find information [in tutorials point](https://www.tutorialspoint.com/java/java_networking.htm) and in [Which Java HTTP client should I use in 2024?](https://www.wiremock.io/post/java-http-client-comparison). HTTP has become the dominant protocol for integration of networked programs. We’re only going to discuss clients that actually implement the HTTP protocol, so libraries such as Spring’s `RestTemplate`(now replaced by `WebClient`), `Retrofit`, or `Feign` that act as higher-level wrappers will not be discussed in this section.

## Socket, ServerSocket, DatagramSocket
Part of OpenJDK and Java SE(Standard Edition). `Socket` is the client and `ServerSocket` is the server, both could be considered legacy APIs, both uses HTTP with TCP to stablish a two way connection between these two, it is a socket, that means you can send bytes from and to each other at the same time, you will be reading and writing bytes using an `OutputStream` and `InputStream`.

`DatagramSocket` uses UDP protocol, UDP doesn't guarantee packages to be delivered while TCP does. Header size of TCP is 20 bytes while Header size of UDP is 8 bytes. TCP introduces overhead due to its acknowledgment and retransmission mechanisms, which can slow down data transfer. `DatagramSocket` is used for network communication via the UDP, is suitable for applications where speed is more critical than reliability, and can be used to both send and receive data. Both, sender and reciever, uses `DatagramSocket` with `DatagramPacket` in both actions, sending and receiving.

## URL, URLConnection, HttpURLConnection, HttpsURLConnection (All considered legacy)
Part of OpenJDK and Java SE(Standard Edition). `URL` can still be used to create http clients, first you have to create the `URL` object, call the `openConnection` method to get an instance of `HttpURLConnection`, actually depending on the scheme(protocol) you're using in the URL string you could be returned an `HttpsURLConnection` object or even other types, you can execute REST methods, GET, POST, PUT, DELETE by specifying the `setRequestMethodd`. You could use Virtual Threads to do async calls but out of the box it only supports synchronous operations. Doesn't supoort HTTP/2, doesn't have cookies, authentication, compression, caching and websockets support. **Spring’s RestTemplate** will use Http(s)URLConnection as their default underlying HTTP implementation **under the hood**, so be carefull and always check the underlying implementation of your HttpClient implementation. Supports the basic set of configuration options you’d expect, but not much more. The connection pool limit and keep-alive idle timeout are only available as system properties. Some developers thinkg the default behaviour/settings are kind of awful and/or buggy, customization is not a characteristic of these APIs. If you want to do quick test this API may be good but avoid using it in production.

## HttpClient, HttpServer


