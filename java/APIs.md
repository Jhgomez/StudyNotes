# Java APIs Found in [FXLauncher](https://github.com/edvin/fxlauncher/tree/8d8aa93f1bd1f676f9d72773b30e495e93a346ff)
FxLauncher is a library for JavaFx that lets you upload files to a remote computer(server) using some of the bellow Java APIs and also, it uses the Linux command/utility called secure copy `scp` to copy files to a remote server usings SSH.

## SCP/Secure Copy(Not a Java API)
Is a command in Linux is used to securely copy files and directories between two locations using SSH for authentication and encryption

```
scp [OPTION] [user@]SRC_HOST:]file1 [user@]DEST_HOST:]file2
```

* OPTION - scp options such as cipher, ssh configuration, ssh port, limit, recursive copy …etc.
* `` - .
* `[user@]SRC_HOST:]file1(Path to the source file`. The name of the user on the source machine and the hostname (or the IP address) of the source machine are used when the file is located on a remote machine.
*  `[user@]DEST_HOST:]:file2(Path to the destination file)`. The name of the user on the destination machine and the hostname (or the IP address) of the destination machine are used when the file is located on a remote machine.

### Copy a Local File to a Remote System with the scp Command
To copy a file from a local to a remote system, run the following command:
```
scp file.txt remote_username@10.10.0.2:/remote/directory
```
Where file.txt is the name of the file we want to copy, `remote_username` is the user on the remote server, `10.10.0.2` is the server IP address. The `/remote/directory` is the path to the directory you want to copy the file to. If you don’t specify a remote directory, the file will be copied to the remote user’s home directory.

You will be prompted to enter the user password, and the transfer process will start.
```
remote_username@10.10.0.2's password:
file.txt                             100%    0     0.0KB/s   00:00
```

Omitting the filename from the destination location copies the file with the original name. If you want to save the file under a different name, you need to specify the new file name:
```
scp file.txt remote_username@10.10.0.2:/remote/directory/newfilename.txt
```
If SSH on the remote host is listening on a port other than the default 22, then you can specify the port using the -P argument

## JNDI Java Naming and Diretory Interface
This API is not used in FXLauncher but it was mentioned in a document about an API that is actually used which is `ClassLoaders`

### When is it used?
While JNDI plays less of a role in lightweight, containerized Java applications such as Spring Boot, there are other uses. Three Java technologies that still use JNDI are JDBC, EJB, and JMS. All have a wide array of uses across Java enterprise applications.

Also when used with `ClassLoader`s. However, sometimes when JVM core classes need to dynamically load classes or resources provided by application developers, we might encounter a problem.

For example, in JNDI, the core functionality is implemented by the bootstrap classes in rt.jar. But these JNDI classes may load JNDI providers implemented by independent vendors (deployed in the application classpath). This scenario calls for the bootstrap class loader (parent class loader) to load a class visible to the application loader (child class loader).

J2SE delegation doesn’t work here, and to get around this problem, we need to find alternative ways of class loading. This can be achieved using thread context loaders.

The java.lang.Thread class has a method, getContextClassLoader(), that returns the ContextClassLoader for the particular thread. The ContextClassLoader is provided by the creator of the thread when loading resources and classes. As of Java SE 9, threads in the fork/join common pool always return the system class loader as their thread context class loader.

## Class Loaders
A class loader is an object that is responsible for loading classes. Further, class loaders load Java classes dynamically to the JVM (Java Virtual Machine) during runtime. They’re also part of the JRE (Java Runtime Environment). Therefore, the JVM doesn’t need to know about the underlying files or file systems to run Java programs thanks to class loaders.
e
Furthermore, the JVM doesn’t load these Java classes into memory all at once, but rather when an application requires them. This is where class loaders come into the picture. They’re responsible for loading classes into memory.

In FXLauncher there is a class called `FxlauncherClassCloader` which extends from `URLClassLoader`, when extending from that class or `ClassLoader` the JVM registers it automatically registers it 

### Use Cases
Custom class loaders are helpful for more than just loading the class during runtime. A few use cases might include:

Helping to modify the existing bytecode, e.g. weaving agents
Creating classes dynamically suited to the user’s needs, e.g. in JDBC, switching between different driver implementations is done through dynamic class loading.
Implementing a class versioning mechanism while loading different bytecodes for classes with the same names and packages. This can be done either through a URL class loader (load jars via URLs) or custom class loaders.

## Service Loader
To explain how this API works it is good to know a very important use case for it, basically you could do some Dependency Inversion/Dependency Injection, basically you declare an interface in your codebase, this can be refered to as a "service" in this context, usually you'd declare implementations of an interface and that is it but you'd also have to implement yourself some sort of dependency injection but this is where service loader helps us, you can declare an impelementation of the class and register it in the `resource` directory `META-INF/services` create a file and name it as if you where importing the interface `example.pkg.interface.exampleInterface` add just one line where you declare the package and the class implementation name as if you where just importing it like `example.pkg.implementation.exampleImplementation`, this implemenation can be called a "service provider" in this context, that is it, now you can use the Service Loader API to get the implementation of a class anywhere you need, however this is only applicable if your app is not a java modular application, menaing is not using the java module system introduced in Java 9, they're commonly referred to as "Java 9 modules", when using modules what you need to do, instead of creating a `META-INF` directory, is declaring in any javal module that is going to use a "service"(an interface) the following `uses example.pkg.interface.exampleInterface;`, just like if you where importing the interface, previously this was also the name of the file that was created inside the `services` directory, also, any subporject/module that contains a "service provider"(implementation of the interface) has to declare, inside the java module file, it is providing an implementation with `provides example.pkg.interface.exampleInterface with example.pkg.implementation.exampleImplementation;`, you can even declare several implementations in a single line, just separate them with a comma, with that you can now use the following code to find all implementations
```
ServiceLoader<exampleInterface> serviceLoader = ServiceLoader.load(exampleInterface.class);
for (exampleInterface provider : serviceLoader) {
    provider.anInterfaceMethod();
}
```

FXLauncher is using this API to load a custom UI, but they are not using Java 9 modules, this means they need a way to include in the Jar file(fxlauncher's artifact) a file with the name of an implementation following the patterns previously described in this document, this means that somehow we need to create a `META-INF` directory inside that Jar, I will explain how that is done but first we need to know that there is a `UiProvider` interface which will be the "service" and we will extend this interface to create a "service provider", once we have done that we need to modify the "fxlauncher.jar" file, and this is accomplished differently depending on your build system, for example in Maven after declaring a dependency you can run `./mvnw install` or `./mvnw dependency:resolve` or even `./mvnw compile` among others, or if you have Maven in you `PATH` environment variable you can call `mvn` instead of the wrapper command, while in Gradle you just sync your project, after you do this in Maven, it will first resolve the artifact’s/dependency POM(the artifact metadata) and then downloads the binary JAR(the compiled classes and resources), note that It does not download the library’s Java source files unless you explicitly ask for them explictly in the dependency declaration with `<classifier>sources</classifier>`. In Gradle it downloads the Jar and the sources by default. The directory where these files are stored is, in Maven, in the user's root directory `~/.m2/repository` and then follow the artifact package naming, in Gradle, in the `~/.gradle/caches/modules` this is where the Jar is downloaded the source files are somewhere but if you're using IntelliJ you can see them in the `External Libraries` section. To modify an artifact(a library's Jar file), in Maven, you need the `org.codehaus.mojo:exec-maven-plugin` plugin, let me explain a litle more about how maven works in the following paragraph

Maven has three lifecycles, `default`, `clean` and `site`, each lifecycle is composed by a sequence of "phases", a Maven phase represents a stage of one of the three lifecycles. Each phase is responsible for a specific task, for example `package`, `install`, `deploy` are task/phases we can execute, at the same time a phase is composed by a sequence of "goals", when you run a phase, all goals bound to the phase are executed in order, for example the `jar:jar` and `war:war` goals are bound to the package phase, you can list all goals bound to a phase with `mvn help:describe -Dcmd=<PHASENAME>`. A Maven plugin is a group of goals, they can be bound to different phases each, you can get a plugin's goals with `mvn <PLUGIN>:help`, you can execute a goal without executing the entire phase(and preceding phases) with `mvn <PLUGIN>:<GOAL>`. the codehaus `exec-maven-plugin` plugin can help us execute commands by adding goals to a phase using its `exec` goal or executing a java class in the current VM with the enclosing project's dependencies as classpath using its `java` goal, what could we do with thsese goals? simple, with the `exec` we can basically use it to run any command as if we where executing a command in a terminal, we have to say what command(executable) we will use, we can say the directory we want to run it from, and then pass it arguments. with the `java` command we can basically declared any number of java programs that we can have this plugin execute, we just have to declare its main class and pass it arguments if we need to, what you can do with this is really up to you and how much you know about different Java tools, APIs, libraries. In the examples using this library, it was used to run a Java class/program that exists inside LauncherFx's artifact that creates a manifest and also for modifying the artifact(jar), this is possible again with the knowledge we have about the Jar files and the JDK tools, Jar files are basically zip files usually, the files contained in the archive/zip/jar are a combination of compiled Java classes and resource files such as images. In addition, there is a standard location within the JAR archive for metadata — the META-INF folder which can contain many files with different formats, while MANIFEST.MF file is the most important file. JAR files provide either a single library or a portion of the functionality of an application. Therefore, constructing Java applications requires combining many JAR files. If you want to browse a Jar file contentn you can run `unzip <path_to_jar>.jar` in a terminal, to modify a jar you need the `jar` command from the JDK, this utility lives inside the "bin" folder of your JDK, if you have added this directory to your PATH environment variable, you can just run it with the command if not you either have to provide the full path or move/change your current directory in the terminal to run this command, in the confiugration of the `exec` the example is indicating a `workingDirectory` but it is really not making much sense here since after that we are basically chaning directory in the `jav` command option and arguments, note it accepts arguments, in this case we pass `uf`, `u` is indicating we are updating an existing Jar, `f` to pass a file name, in this case the file name is "fxlauncher.jar", note that maven knows where this jar is, and I already explained where these files live, and in the path indicated which is `<argument>${project.basedir}/../fxlauncher-custom-ui/target/classes</argument>`, it could have been writtent like `<argument>${project.basedir}/target/classes</argument>`, it is important to note that with the property declared `app.dir` since we passed it to the `org.apache.maven.plugins` either using the plugin `maven-compiler-plugin` or `maven-jar-plugin` we passed it in the configuration `<outputDirectory>${app.dir}</outputDirectory>` this helps us separate the class files generated from the packaging process so we can just copy the `META-INF/services` content to the jar, this is how we can achive modifyin the jar so that it can find the implementation using the service loader.

How can we do this in Gradle?, we will leave this as a TODO, but basically investigate how `tasks` and/or "Atrifact Transforms" work in Gradle
