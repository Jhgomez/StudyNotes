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

## Spring Framework
Is the application development framework for JavaEE. It’s an open-sourceThe. Its core feature is developing any Java application and this targets to make J2EE development easier to use. It enables developing enterprise-class applications using POJO (Plain Old Java Object).

While it does not use Java EE under the hood, it is based on Java EE specifications and is designed to work with them. Spring provides a flexible and modular architecture, allowing developers to build applications using Java EE technologies while leveraging the benefits of the Spring Framework. Spring is slower than JavaEE.

## Spring Boot
Is an extension of the Spring Framework that aims to simplify the development of Spring applications, and it is built on top of Spring Framework. It provides a set of conventions and defaults to reduce the amount of configuration required, in Spring Framework you have to configure things like the dispatcher servlet, view resolvers, and security settings

Spring Framework is suuitable for complex applications that require fine-grained control over configuration and components.

Spring Boot is ideal for microservices and rapid application development, where simplicity and speed are essential

while the Spring Framework provides a comprehensive set of tools for building Java applications, Spring Boot simplifies the process by reducing configuration and providing sensible defaults. Spring Boot is built on top of the Spring Framework and is not a replacement but rather a complement to it

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

All these APIs are part of OpenJDK and Java SE(Standard Edition) and all of them can be used to create simple either client or servers, note that more robust servers can be built using the options noted above(Java EE/Jakarta EE, Spring Framework, Spring boot)

All of these APIs are still supoorted in Java, however it could be said that making connections using `URL`, `URLConnection`, is a legacy way to do it and since Java 11 `HttpClient` is a modern way to do the same. 


