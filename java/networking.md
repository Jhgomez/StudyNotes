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

# Important Concepts
## HTTP Multipart File Upload
HTTP multipart request is a type of HTTP request that allows clients to send multiple parts of data to a server in a single request. This is particularly useful when uploading files or sending large amounts of binary data. The multipart request is commonly used by browsers and HTTP clients to upload files to the server.

## Transparent content compression/decompression
It refers to whether the client can perform compression and decompression of content via (most commonly) Deflate, GZip or Brotli without requiring the caller to explicitly perform the encode and decode steps.

At present GZip is by far the most common algorithm.

# ServerSocket, Socket, URL, URLConnection, HttpURLConnection, DatagramSocket, HttpClient, HttpServer
You can find information [in tutorials point](https://www.tutorialspoint.com/java/java_networking.htm) and in [Which Java HTTP client should I use in 2024?](https://www.wiremock.io/post/java-http-client-comparison). HTTP has become the dominant protocol for integration of networked programs. We’re only going to discuss clients that actually implement the HTTP protocol, so libraries such as Spring’s `RestTemplate`(now replaced by `WebClient`), `Retrofit`, or `Feign` that act as higher-level wrappers will not be discussed in this section.

## Socket, ServerSocket, DatagramSocket
Part of OpenJDK and Java SE(Standard Edition). `Socket` is the client and `ServerSocket` is the server, both could be considered legacy APIs, both uses HTTP with TCP to stablish a two way connection between these two, it is a socket, that means you can send bytes from and to each other at the same time, you will be reading and writing bytes using an `OutputStream` and `InputStream`.

`DatagramSocket` uses UDP protocol, UDP doesn't guarantee packages to be delivered while TCP does. Header size of TCP is 20 bytes while Header size of UDP is 8 bytes. TCP introduces overhead due to its acknowledgment and retransmission mechanisms, which can slow down data transfer. `DatagramSocket` is used for network communication via the UDP, is suitable for applications where speed is more critical than reliability, and can be used to both send and receive data. Both, sender and reciever, uses `DatagramSocket` with `DatagramPacket` in both actions, sending and receiving.

### `SSLServerSocket` and `SSLSocket`
`SSLServerSocket` is to `ServerSocket` what `SSLSocket` is to `Socket`. These two APIs lets us secure our communications by stabilshing an encrypted connection between server and client. Before using these APIs you should get familiar with **`KeyStore`** API, both, the sender and client, will use this API. A **KeyStore** in Java is a collection of key entries, each identified by an alias, and can store private keys, public keys(Java refers to "Asymmetric Keys" as private and public keys), secret keys(this is how Java refers to "Symmetric Keys"), and trusted certificates(I think these are the Certificate Authorities).

In order to be able to create a secure connection with the SSL version of the sockets server and client, first you need to create a KeyStore, once you create the store you init an `KeyManagerFactory` by passing the KeyStore you created/loaded to the managner's factory and then using the factory to generate a managers instance that you pass to the next object in the next following step, in this step you need to create a `SSLContext`, again, to set up the context, you need to pass it the managers instance, this is where you would need to investigate a little as the context can be set up in different ways, I'm not sure but it seems that you can set up both the same way, or maybe they can be set up in different ways depending on if you're going to create a server or a client, either way, this conext object is what we will use to create either a `SSLSocketFactory` for the client side or a `SSLServerSocketFactory` for the server side using the method `getSocketFactory` or `getServerSocketFactory` respectively.

## URL, URLConnection, HttpURLConnection, HttpsURLConnection (All considered legacy)
Part of OpenJDK and Java SE(Standard Edition). `URL` can still be used to create http clients, first you have to create the `URL` object, call the `openConnection` method to get an instance of `HttpURLConnection`, actually depending on the scheme(protocol) you're using in the URL string you could be returned an `HttpsURLConnection` object or even other types, you can execute REST methods, GET, POST, PUT, DELETE by specifying the `setRequestMethodd`. You could use Virtual Threads to do async calls but out of the box it only supports synchronous operations. Doesn't supoort HTTP/2, doesn't have cookies, authentication, compression, caching and websockets support. **Spring’s RestTemplate** will use Http(s)URLConnection as their default underlying HTTP implementation **under the hood**, so be carefull and always check the underlying implementation of your HttpClient implementation. Supports the basic set of configuration options you’d expect, but not much more. The connection pool limit and keep-alive idle timeout are only available as system properties. Some developers thinkg the default behaviour/settings are kind of awful and/or buggy, customization is not a characteristic of these APIs. If you want to do quick test this API may be good but avoid using it in production.

## Java 17 "Security Developer's Guide"(Found in Java's 17 documentation)
Part of the mentioned guide is the [Java Secure Socket Extension (JSSE) Reference Guide](https://docs.oracle.com/en/java/javase/17/security/java-secure-socket-extension-jsse-reference-guide.html#GUID-93DEEE16-0B70-40E5-BBE7-55C3FD432345)

### **Java Secure Socket Extension (JSSE)**
enables secure Internet communications. It provides a framework and an implementation for a Java version of the TLS protocol and includes functionality for data encryption, server authentication, message integrity, and optional client authentication. Using JSSE, developers can provide for the secure passage of data between a client and a server running any application protocol (such as HTTP, Telnet, or FTP) over TCP/IP.

By abstracting the complex underlying security algorithms and handshaking mechanisms, JSSE minimizes the risk of creating subtle but dangerous security vulnerabilities. Furthermore, it simplifies application development by serving as a building block that developers can integrate directly into their applications.

JSSE provides both an application programming interface (API) framework and an implementation of that API. The JSSE API supplements the core network and cryptographic services defined by the java.security and java.net packages by providing extended networking socket classes, trust managers, key managers, SSL contexts, and a socket factory framework for encapsulating socket creation behavior. Because the SSLSocket class is based on a blocking I/O model, the Java Development Kit (JDK) includes a nonblocking SSLEngine class to enable implementations to choose their own I/O methods.

The JSSE API supports the following security protocols:

* DTLS: versions 1.0 and 1.2
* TLS: version 1.0, 1.1, 1.2, and 1.3
* SSL (Secure Socket Layer): version 3.0

These security protocols encapsulate a normal bidirectional stream socket, and the JSSE API adds transparent support for authentication, encryption, and integrity protection.

JSSE is a security component of the Java SE platform, and is based on the same design principles found elsewhere in the Java Cryptography Architecture (JCA) Reference Guide framework. This framework for cryptography-related security components allows them to have implementation independence and, whenever possible, algorithm independence. JSSE uses the Cryptographic Service Providers defined by the JCA framework.

#### JSSE Features and Benefits
JSSE includes the following important benefits and features:

* Included as a standard component of the JDK
* Extensible, provider-based architecture
* Implemented in 100% pure Java
* Provides API support for TLS/DTLS
* Provides implementations of SSL 3.0, TLS (versions 1.0, 1.1, 1.2, and 1.3), and DTLS (versions 1.0 and 1.2)
* Includes classes that can be instantiated to create secure channels (SSLSocket, SSLServerSocket, and SSLEngine)
* Provides support for cipher suite negotiation, which is part of the TLS/DTLS handshaking used to initiate or verify secure communications
* Provides support for client and server authentication, which is part of the normal TLS/DTLS handshaking
* Provides support for HTTP encapsulated in the TLS protocol, which allows access to data such as web pages using HTTPS
* Provides server session management APIs to manage memory-resident SSL sessions
* Provides support for the certificate status request extension (OCSP stapling), which saves client certificate validation round-trips and resources
* Provides support for the Server Name Indication (SNI) rxtension, which extends the TLS/DTLS protocols to indicate what server name the client is attempting to connect to during handshaking
* Provides support for endpoint identification during handshaking, which prevents man-in-the-middle attacks
* Provides support for cryptographic algorithm constraints, which provides fine-grained control over algorithms negotiated by JSSE

#### JSSE Standard API
The JSSE standard API, available in the **`javax.net`** and **`javax.net.ssl`** packages, provides:

* Secure sockets tailored to client and server-side applications.
* A non-blocking engine for producing and consuming streams of TLS/DTLS data (SSLEngine).
* Factories for creating sockets, server sockets, SSL sockets, and SSL server sockets. By using socket factories, you can encapsulate socket creation and configuration behavior.
* A class representing a secure socket context that acts as a factory for secure socket factories and engines.
* Key and trust manager interfaces (including X.509-specific key and trust managers), and factories that can be used for creating them.
* A class for secure HTTP URL connections (HTTPS).

## HttpClient, HttpServer
Both introduced in Android 11, `HttpClient` replaced `HttpURLConnection` and `HttpsURLConnection`. `HttpServer` was introduced as a solution to easily create a REST API. `HttpClient` supports both synchronous and asynchronous modes of operation, with the latter making use of Futures, it supports HTTP/2, it offers a pluggable authentication mechanism, only provides an implementation of non-preemptive HTTP Basic so if you need anything else you’ll need to implement it yourself, it supports cookies, it doesn't support caching, and it does support websockets(you basically create a `WebSocket` object with `newWebSocketBuilder`)

## Third Party Http Client Alternative APIs
A great comparisson can be found [here](https://www.wiremock.io/post/java-http-client-comparison#apache-httpclient)

### Okhttp
It has a number of fault tolerance features such as the ability to fail over between multiple IP addresses and recover from failed connection attempts. It also implements transparent content compression via Deflate, GZip and Brotli. Its defaults configurations are thoughtfully chosen. Provided you keep to the latest version, you’ll get a fast, secure and reliable setup without needing to do much of your own, however it provides plenty of configuration options and extension points. Everything is configurable at the client instance level, so multiple clients can exist with different settings and it’s straightforward to integrate with your configuration system. A unique feature that may be hard to find in other alternatives is it support separate read and write timeouts. It supports synchronous and asynchronous calls and both uses callback, it supports multiplepart file upload. For large files, consider using streaming to avoid memory issues. It supports cookies, pluggable autenthication, caching and websockets

### Jettyy
supports HTTP/2 and is very configurable, it also offers access to lower-level tuning parameters such as the executor implementation, scheduler and byte buffer pools, hich makes it a good alternative to the OkHttp client. It uses entirely non-blocking code under the hood and presents both synchronous and asynchronous APIs using callbacks. It supports multipart file upload, it supports cookies. It offers authentication using Basic, Digest, SPNEGO, or using a Pluggable solution. It support transparent content compression using GZIP, it doesn't supports caching, and it supports websockets.

# Using `ServerSocket`(Server) with `Socket`(Client)
This example uses the only way to create a Server that supports sockets using only standard libraries, off course there should be 3rd party options, however with this setup we don't need to add any dependency, this was used in a simple JavaFx game which can create several windows of the same app and specify one window as a server and other windows as clients, the server will be in charge of synchronizing all other clients. Clients sockets are created using the legacy option `Socket` instead of creatting the sockets through `HttpCleitn`. In a real world scenario we should be using WebRTC(Web real-time communication) protocol and I will experiment with that later. 

With this setup we will be working with the I/O clases `InputStream`(to read info), `OutpuStream`(to write info), `Readed` and `Writter`, remember all of them are streams even reader and writter too, the difference between the streams and writter/readers is that the first works with any binary values(bytes) while the later pair, depending the implementation you are using, works with characters or strings of characters. When working with these objects through a socket you have to be careful with `outputStream`s and `Writer`s as they have to be flushed, as the OS doesn't guarantee that the data being written will be written instantaneously, this is because writting to a file(this is how the streams are used most commonly) is an expensive operation since it means writting to disk, this implies a round trip from JVM to disk, this could delay the application, if fact if some outputStream or Writters are not flushed, the data will be cachesd in memory only and after some time it will be flushed or even only after the stream is closed, that is why when working with them in sockets you have to check if there is any need to flush the stream manually, this would be necesarry for a stream like below(this would work the same way in both sockets streams, the client as in the server)

```
try (ServerSocket serverSocket = new ServerSocket(PORT)) {

  Socket clientSocket = serverSocket.accept();

  // Accept incoming connections
  while (true) {
      // with below stream, you have to flush, we use the BufferedOutputStream
      // since it is said it provides an performance improvement(at least when
      // working with files but we are wokring with sockets here so maybe it doesn't make any difference)
      // autoflush is the second parameter in printwriter
      PrintWriter out = new PrintWriter(new BufferedOutputStream(clientSocket.getOutputStream()), true);
  
      // with the below stream we don't need to flush explicitly
      PrintWriter out = new PrintWriter(clientSocket.getOutputStream());
  
      out.println("Repetitive message");
  
      // with the below stream we don't need to flush explicitly
      var out = new DataOutputStream(socket.getOutputStream());
  
      out.writeUTF("Another repetitive message");    
  }
}
```

Reading doesn't have this issue
```
try (Socket socket = new Socket("localhost", 12346)) {

  // Accept incoming connections
  while (true) {
      // BufferedReaderputStream, again, is said to be more efficient when reading lines
      // it makes it easier and also, again, is said to be more performant
      var in = new BufferedReader(new InputStreamReader(clientSocket.getInputStream()));
  
      in.println("A message: " + in.readline());
  
      // with the below stream we don't need to flush explicitly
      var in = new DataInputStream(socket.getInputStream());-
  
      in.writeUTF("Another message received: " + in.readUTF());    
  }
}
```

Another thing to note here that is not mentioned in the documention I have accessed to, is that any read call(depending on the inputstream you choose to use, it could be a call like `read`, `readline`, `readObject`, etc) to the Sockets `InputStream` blocks the thread which is something that doesn't happen when working with files, as for example, when using a BufferedReader's `readLine()` method with the OS's file system files, it doesn't block and if it reaches the end of file it throws an EOF exception, in sockets this exception is never thrown, not even when socket on the other end disconnects, knowing how it behaves was important to get the correct code in our example below, and it was more important in the server side, since we wanted to stop writting messages to connections that don't exists anymore, in our case that means we had to remove the correct `PrintWriter` object, and basically we do that when the execution flow continues after the `while` loop that reads from client's inputstream returns null, which is the behaviour that I just mentioned in which there is no exception thrown, meaning that if we reach that execution point it is because the client's socket its been closed. Later in my development I found out that if the thread is locked with one of the read calls and we call either the socket object returned in the server with ()


server

```
import java.io.*;
import java.net.ServerSocket;
import java.net.Socket;
import java.net.SocketException;
import java.util.*;
import java.util.concurrent.ExecutorService;
import java.util.concurrent.Executors;

public class server {
    private static final List<PrintWriter> writters = new ArrayList<>();
    private static final ExecutorService executor = Executors.newVirtualThreadPerTaskExecutor();
    private static final Deque<String> messagesToClients = new ArrayDeque<>();

    static void main(String[] args) throws IOException {
        try (var server = new ServerSocket( 12346)) {

            executor.execute(() -> {
                var scanner = new Scanner(System.in);

                while (!server.isClosed()) {
                    System.out.print("> ");

                    var userInput = scanner.nextLine();
                    messagesToClients.offer(userInput);

                    executor.execute(() -> {
                        broadcastMessages();
                    });
                }
                System.out.println("server is closed");
            });

            while (!server.isClosed()) {
                Socket client = server.accept();

                executor.submit(() -> {
                    try {
                        var out = new PrintWriter(new BufferedOutputStream(client.getOutputStream()), true);
                        writters.add(out);

                        var in = new BufferedReader(new InputStreamReader(client.getInputStream()));

                        var message = "";

//                        System.out.println("Client connected");

                        executor.execute(() -> {
                            broadcastMessages();
                        });

                        while ((message = in.readLine()) != null) {
//                            System.out.println("Message received from client: " + message);
                            System.out.println("\n- " + message);
                            System.out.print("> ");
                        }

//                        System.out.println("Client disconnected");
                        writters.remove(out);
                    } catch (IOException e) {
                        throw new RuntimeException(e);
                    }
                });
            }
        }
    }

    private static void broadcastMessages() {
        while(!messagesToClients.isEmpty() && !writters.isEmpty()) {
//            System.out.println(messagesToClients);
            var message = messagesToClients.poll();
//            System.out.println("polling message " + message);

            for (var out : writters) {
                out.println(message);
//                System.out.println("Message sent to client ");
            }
        }
    }
}
```

clients
```
import java.io.*;
import java.net.InetSocketAddress;
import java.net.Socket;
import java.util.Scanner;
import java.util.concurrent.ExecutorService;
import java.util.concurrent.Executors;

public class client {
    static OutputStream os;

    static void main(String[] args) throws IOException {

        try (Socket socket = new Socket("localhost", 12346)) {

            // Setting up input and output streams
            var out = new PrintWriter(new BufferedOutputStream(socket.getOutputStream()), true);
            var in = new BufferedReader(new InputStreamReader(socket.getInputStream()));

            // Start a thread to handle incoming messages
            Thread.startVirtualThread(() -> {
                try {
                    var message = "";
                    while ((message = in.readLine()) != null) {
                        System.out.println("\n- " + message);
                        System.out.print("> ");
                    }
                } catch (IOException e) {
                    throw new RuntimeException(e);
                }
            });

            // Read messages from the console and send to the server
            Scanner scanner = new Scanner(System.in);
            String userInput = "";
            while (true) {
//                System.out.print("Waiting for client input: ");
                System.out.print("> ");

                userInput = scanner.nextLine();

                out.println(userInput);

//                System.out.println("Input sent to server: " + userInput);
            }
        }
    }
}
```
