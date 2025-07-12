# Java APIs Found in [FXLauncher](https://github.com/edvin/fxlauncher/tree/8d8aa93f1bd1f676f9d72773b30e495e93a346ff)
FxLauncher is a library for JavaFx that lets you upload files to a remote computer(server) using some of the bellow Java APIs and also, it uses the Linux command/utility called secure copy `scp` to copy files to a remote server usings SSH.

## SCP(Not a Java API)
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
