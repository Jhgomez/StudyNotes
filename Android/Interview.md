{\rtf1\ansi\ansicpg1252\cocoartf2761
\cocoatextscaling0\cocoaplatform0{\fonttbl\f0\fswiss\fcharset0 Helvetica;\f1\fswiss\fcharset0 Helvetica-Bold;\f2\fmodern\fcharset0 Courier;
\f3\fswiss\fcharset0 Helvetica-BoldOblique;\f4\fswiss\fcharset0 ArialMT;\f5\fnil\fcharset0 HelveticaNeue;
\f6\fnil\fcharset0 HelveticaNeue-Light;\f7\fnil\fcharset0 HelveticaNeue-Bold;}
{\colortbl;\red255\green255\blue255;\red24\green25\blue27;\red255\green255\blue255;\red56\green60\blue66;
\red38\green38\blue38;\red228\green229\blue251;\red35\green36\blue47;\red24\green24\blue24;\red224\green226\blue231;
\red242\green244\blue246;\red255\green255\blue255;\red21\green25\blue49;\red250\green250\blue250;\red36\green43\blue141;
\red227\green236\blue254;\red26\green28\blue31;\red191\green191\blue191;\red24\green25\blue26;}
{\*\expandedcolortbl;;\cssrgb\c12549\c12941\c14118;\cssrgb\c100000\c100000\c100000;\cssrgb\c28304\c30269\c32720;
\cssrgb\c20000\c20000\c20000;\cssrgb\c91373\c92157\c98824;\cssrgb\c18039\c18824\c24314;\cssrgb\c12549\c12549\c12549;\cssrgb\c90196\c90980\c92549;
\cssrgb\c96078\c96471\c97255;\cssrgb\c100000\c100000\c100000\c92157;\cssrgb\c10588\c13333\c25098;\cssrgb\c98431\c98431\c98431;\cssrgb\c18824\c24706\c62353;
\cssrgb\c90980\c94118\c99608;\cssrgb\c13725\c14902\c16078;\csgray\c79525;\cssrgb\c12549\c12941\c13333;}
{\*\listtable{\list\listtemplateid1\listhybrid{\listlevel\levelnfc23\levelnfcn23\leveljc0\leveljcn0\levelfollow0\levelstartat1\levelspace360\levelindent0{\*\levelmarker \{disc\}}{\leveltext\leveltemplateid1\'01\uc0\u8226 ;}{\levelnumbers;}\fi-360\li720\lin720 }{\listname ;}\listid1}}
{\*\listoverridetable{\listoverride\listid1\listoverridecount0\ls1}}
\margl1440\margr1440\vieww30040\viewh17760\viewkind0
\pard\tx720\tx1440\tx2160\tx2880\tx3600\tx4320\tx5040\tx5760\tx6480\tx7200\tx7920\tx8640\pardirnatural\partightenfactor0

\f0\fs24 \cf0 x\
\
\pard\tx720\tx1440\tx2160\tx2880\tx3600\tx4320\tx5040\tx5760\tx6480\tx7200\tx7920\tx8640\pardirnatural\partightenfactor0

\fs48 \cf0 *Android components
\fs24 \
\pard\pardeftab720\partightenfactor0

\fs32 \cf2 \cb3 \expnd0\expndtw0\kerning0
entry points through which the system or a user can enter your app, they all have to be declares in the manifest.
\fs24 \cf0 \cb1 \kerning1\expnd0\expndtw0 \
\pard\tx720\tx1440\tx2160\tx2880\tx3600\tx4320\tx5040\tx5760\tx6480\tx7200\tx7920\tx8640\pardirnatural\partightenfactor0
\cf0 \
1. - 
\f1\b Activity 
\f0\b0 i
\fs32 \cf2 \cb3 \expnd0\expndtw0\kerning0
s the entry point for interacting with the user. It represents a single screen with a user interface, the component were we draw our UI\
\
2.-
\f1\b  Services
\f0\b0  They handle background processing associated with an application. It is a component that runs in the background to perform long-running operations or to perform work for remote processes (play music in the background, network connectivity, bluetooth, location(gps), is basically hardware functionalities plus some other \'93special\'94 cases), there is two types:\
\
	2.1.- 
\f1\b Started services
\f0\b0 \'a0tell the system to keep them running until their work\
	is completed. This might be to sync some data in the background or play\
	music  even after the user leaves the app, they aren\'92t too common\
	nowadays since devs used to overuse this component, currently they are\
	more restricted by the android operating system\
\
	there is two types of started services one that runs in the foreground, the\
	user is directly aware of this process and will be informed with a notification\
	that this process is running(location is an expample, downloading files, playing	music). The second runs in the background user is not aware of this and is	fully managed by the system, meaning it could be killed to free RAM/memory 	and restarted later on(examples: synching and storing data)\
\
	2.2 
\f1\b Bound services
\f0\b0 \'a0run because some other app (or the system) has said\
	that it wants to make use of the service.	Meaning B depends on A, so B will\
	be treated the same way as A meaning if user is aware of A, B is treated\
	that way and if managed by the system meaning user is not aware then B is	treated that way\
\
\pard\pardeftab720\partightenfactor0
\cf2 Because of their flexibility, services are useful building blocks for all kinds of higher-level system concepts. Live wallpapers, notification listeners, screen savers, input methods, accessibility services, and many other core system features are all built as services\'a0\
\pard\tx720\tx1440\tx2160\tx2880\tx3600\tx4320\tx5040\tx5760\tx6480\tx7200\tx7920\tx8640\pardirnatural\partightenfactor0
\cf2 \
3.- 
\f1\b Broadcast receivers 
\f0\b0 \'a0component that lets the system deliver events to the app outside of a regular user flow, the app can request a broadcastReceiver in the app to schedule a notification\
\
The system creates different broadcast also, like a broadcast announcing that the screen is turned off, the battery is low, or a picture is captured. Aps can also initiate broadcasts, such as to let other apps know that some data is downloaded to the device and is available for them to use\
\
\pard\pardeftab720\partightenfactor0
\cf2 each broadcast is delivered as an\'a0{\field{\*\fldinst{HYPERLINK "https://developer.android.com/reference/android/content/Intent"}}{\fldrslt 
\f2\fs26 \cf0 \cb1 Intent}}\'a0object\
	\
	Implicit Intent vs Explicit Intent\
\
4.- 
\f1\b Content providers 
\f0\b0 shared set of app data that you can store in any type of persistent storage location(file system, in a SQLite database, on the web) that the app or other apps can access through the content provider, an example, Android system provides a content provider that manages the user's contact information and any app with the proper permissions can access this info.\
\
They are identified by a URI scheme. An app can decide how it wants to map the data it contains to the URI\
\
\pard\pardeftab720\partightenfactor0

\f1\b\fs36 \cf2 Kotlin Objects Expressions and Declarations
\f0\b0\fs32 \
Object classes can not have a constructor\
\
	
\f1\b Expressions
\f0\b0  - Create objects of anonymous classes(Classes not explicitly declared with the class keyword, useful for one-time use), also called anonymous objects. The return type of an anonymous object 	depends of if it is the return type of a function and function is public, it is inferred as \'93Any\'94 so funs and properties can not be called but if it is a private function it would be inferred as \'93anonymous object: Any\'93 	and that gives us access to everything public in this object. They can not have a name. They can be declared inside a method. They are initiated right where they are declared(immediately)\
\
		val helloWorld = object \{ override fun toString() = \'93helloWorld\'94 \}\
		val anonymousChild = object: anInterface \{ \}\
	\
	
\f1\b Declarations
\f0\b0  - They must have a name, they are singletons, can live inside and outside a class on its own, can not have constructors, they can be local meaning they can not be defined/declared inside a		method. They initialized lazily, meaning when they are accessed/called\
\
	We can define \'93data class\'94 and a \'93data object\'94 the differences are data objects since they are singleton don\'92t a \'93copy\'94 method. \
	\
	
\f1\b companion objects
\f0\b0  - the methods, values/properties inside this objects have the same behavior as method and properties with the static modifier in Java, they can not have constructors, they can be 		declared without a name, they can only exist inside a class, a class can only have one\
\

\f1\b\fs36 When (Kotlin) Vs Switch(Java)
\f0\b0\fs32 \
	
\f1\b When(Kotlin)
\f0\b0 \
	It can be used as an expression or statement. If it is used as an expression the value of the first matching condition will be the value of the expression and an \'93else\'94 branch would be required unless the 		compiler can prove all possible cases are covered, for example enums and sealed classes. If used as a statement the values of the conditions are just ignored but \'93else\'94 branch is also required in statements 	if all possible scenarios are not evaluated like when the subject is a Boolean, Enum, sealed class. It can have a subject or not.\
\
	Switch(Java)\
	It can only have a subject of primitives or Enum, String and primitive wrapper classes. The default branch is optional, the break is optional but useful as all branches code is executed after the a matching 		branch is found and a break is not declared.\
\
Sealed Vs Enum\
\
	Java\
	The compiler is informed of possible values(Enums)\
\
		Sealed Class/Interface(available since JDK 17``)\
		Child classes can only exist inside the same file, they can add properties and methods, and they can have its own constructor. Used in case of more complex set of types/values. The child classes has		to have the final modifier or must be declared non-sealed which means this child class/interface can be extended/implemented by other classes.\
		following\
\
			sealed interface/class Shape permits Circle \{\}\
			final class Circle implements/extends Shape \{\}\
		\
		The permits declaration can be omitted if the child classes are defined in the same file, child classes can be defined in the same package or same module but not outside(in a different module)\
	\
		Enum\
		The values are defined as constants, the constructor is the same on all however they can add properties and methods, it can contain \'93normal\'94 methods and abstract methods and both	\
		can be overriden inside an enum possible value, the constructor, if provided, has to have package private(default) or private modifier\
\
\
	Kotlin\
	The compiler is informed of possible types(sealed class) or values(Enums)\
\
		Sealed Class/Interface\
		Child classes can only exist inside the same file, they can add properties and methods, and they can have its own constructor. Used in case of more complex set of types/values\
	\
		Enum\
		The values are defined as objects so they are singletons, the constructor is the same on all however they can add properties and methods, methods inside the enum are final so they can not be\
		overrides 	unless they are declared abstract specifically\
\
Access Modifiers\
	Java\
		Private - Only available in the same 
\f3\i\b class
\f0\i0\b0 \
		Default(no modifier) - Available within the same package(package private)\
		Protected - Available within the same package and child classes(either in the same or different package)\
		Public - Accessible from anywhere\
	\
	Kotlin\
		Private - Only accessible in the same 
\f3\i\b file
\f0\i0\b0 \
		Protected - In contrast to java behaviour this one is not available within same package instead it is only accessible by child classes\
		Internal - Accessible within the same module\
		Public(default access modifier) - Accessible from anywhere\
		\
* 
\fs48 GIT
\fs32 \
\pard\pardeftab720\partightenfactor0

\f4\fs28 \cf4 is a distributed version control system that tracks changes in any set of computer files, usually used for coordinating work among programmers who are collaboratively developing source code during software development\
\
*
\fs48 Kotlin is null safety
\fs28 \
Kotlin is null safety because you have to specify to the compiler whether an object can be null or not but still can throw a NPE when using the not null assertion operator among other cases also when using java code like with date objects, or explicitly throwing this exception\
\
-Kotlin Object class\
\
\

\fs48 *SQLite
\fs28 \
Is a database engine which uses SQL lenguage (structured query lenguage), other engines are mysql, postgresql, SQL server, InnoDB\
\

\fs48 *ROOM
\fs28 \
Is a database layer on top of a SQLite database.\
\

\fs48 *SQLdelight
\fs28 \
Library that generate kotlin APIs from SQL statements. It provides multiple platform-specific implementations of the sqlite driver\
\

\fs48 *DataStore and Shared Preferences
\fs28 \
Local storage which are not stored and accessed with queries, and are more volatile since the user can delete them by deleting the app cache from app settings. One is asynchronous and the other not(check differences). They are not stored/retrieved using queries.\
\pard\tx720\tx1440\tx2160\tx2880\tx3600\tx4320\tx5040\tx5760\tx6480\tx7200\tx7920\tx8640\pardirnatural\partightenfactor0

\f0\fs32 \cf2 \
\pard\tx720\tx1440\tx2160\tx2880\tx3600\tx4320\tx5040\tx5760\tx6480\tx7200\tx7920\tx8640\pardirnatural\partightenfactor0

\fs48 \cf2 *REST API
\fs32 \
Api means Application programming interface, REST means representational state transfer, this means they are a set of rules that defines how application or devices can connect to and communicate with each other following the rest architectural style . This means in rest apis when a client request a resource the server will return the current state of the resource in a standardized representation. In Android we use 
\f1\b Retrofit
\f0\b0  to communicate with a REST api along with 
\f1\b Moshi
\f0\b0  and 
\f1\b OkHttp
\f0\b0 . 
\f5\fs28 \cf5 \cb1 Is a set of rules that defines structured data exchange between a client and a server.
\f0\fs32 \cf2 \cb3 \
\

\fs48 *Retrofit
\fs32 \
\pard\pardeftab720\partightenfactor0
\cf2 Is a Rest api client for java and Android with which you can retrieve an upload Json and is an abstraction built on top of OkHttp.\
\pard\tx720\tx1440\tx2160\tx2880\tx3600\tx4320\tx5040\tx5760\tx6480\tx7200\tx7920\tx8640\pardirnatural\partightenfactor0
\cf2 \
\pard\tx720\tx1440\tx2160\tx2880\tx3600\tx4320\tx5040\tx5760\tx6480\tx7200\tx7920\tx8640\pardirnatural\partightenfactor0

\fs48 \cf2 *Moshi
\fs32 \
\pard\pardeftab720\partightenfactor0
\cf2 Is a library by which we can parse JSON into Java and Kotlin classes and backwards\
\pard\tx720\tx1440\tx2160\tx2880\tx3600\tx4320\tx5040\tx5760\tx6480\tx7200\tx7920\tx8640\pardirnatural\partightenfactor0
\cf2 \
\pard\tx720\tx1440\tx2160\tx2880\tx3600\tx4320\tx5040\tx5760\tx6480\tx7200\tx7920\tx8640\pardirnatural\partightenfactor0

\fs48 \cf2 *Okhttp\
\pard\pardeftab720\partightenfactor0

\f5\fs32 \cf6 \cb7 OkHttp is an HTTP client, you would prefer this library if you would want to have more control over your own network process,
\f0\fs48 \cf2 \cb3 \
\pard\tx720\tx1440\tx2160\tx2880\tx3600\tx4320\tx5040\tx5760\tx6480\tx7200\tx7920\tx8640\pardirnatural\partightenfactor0
\cf2 \
*GraphQL
\fs32 \
GraphQL is a query language for API and a runtime for fulfilling those queries with your existing data. 
\f6\fs36 \cf8 \cb9 \'a0While typical REST APIs require loading from multiple URLs, GraphQL APIs get all the data your app needs in a single request. \cb10 GraphQL APIs are organized in terms of types and fields, not endpoints. Access the full capabilities of your data from a single endpoint. GraphQL uses types to ensure Apps only ask for what\'92s possible and provide clear and helpful errors. Apps can use types to avoid writing manual parsing\'a0code. 
\f7\b Queries
\f6\b0  perform read operations, they operate as GET requests in REST. 
\f7\b Mutations
\f6\b0  create, update or delete objects and fields, they operate similar to POST, PUT, DELETE in REST. 
\f5\fs28 \cf5 \cb1 \'a0is a query language, architecture style, and set of tools to create and manipulate APIs. There is a third type of operation called SUBSCRIPTIONS which are long-lasting operations that can change its result over time.
\f6\fs36 \cf8 \cb9 \
\

\f0\fs48 \cf2 \cb3 *Apollo
\fs32 \
\pard\pardeftab720\partightenfactor0
\cf2 I
\fs36 \cf11 \cb12 GraphQL client that generates Kotlin and Java models from GraphQL queries. 
\fs32 \cf2 \cb3 \
\pard\tx720\tx1440\tx2160\tx2880\tx3600\tx4320\tx5040\tx5760\tx6480\tx7200\tx7920\tx8640\pardirnatural\partightenfactor0
\cf2 \
\pard\tx720\tx1440\tx2160\tx2880\tx3600\tx4320\tx5040\tx5760\tx6480\tx7200\tx7920\tx8640\pardirnatural\partightenfactor0

\fs36 \cf2 *GraphQl Vs. REST API
\fs32 \
\pard\tx720\tx1440\tx2160\tx2880\tx3600\tx4320\tx5040\tx5760\tx6480\tx7200\tx7920\tx8640\pardirnatural\partightenfactor0

\f5\fs28 \cf5 \cb13 Both are HTTP-based as HTTP is the underlying communication protocol. They are basically specifications that describes the behavior of a server, how we can get and send information to a server. REST apis are focused on making new APIs, GraphQL\'92s focus has been on API performance and flexibility\cb1 .\
\
\pard\pardeftab720\sa280\partightenfactor0
\cf5 REST is good for simple data sources where resources are well defined. GraphQL is good for large, complex, and interrelated data sources.\
REST has multiple endpoints in the form of URLs to define resources.   GraphQL has a single URL endpoint.\
\pard\pardeftab720\partightenfactor0
\cf5 REST returns data in a fixed structure defined by the server.  GraphQL returns data in a flexible structure defined by the client.\
\
REST is weakly typed so client has to decide how to interpret the returned resource while GraphQl is strongly typed so clients receives data in a mutually predetermined structure\
\
\pard\pardeftab720\sa280\partightenfactor0
\cf5 Rest clients have to check if returned data is valed to catch and handle errors, while graphql invalid request\
\pard\tx720\tx1440\tx2160\tx2880\tx3600\tx4320\tx5040\tx5760\tx6480\tx7200\tx7920\tx8640\pardirnatural\partightenfactor0

\fs36 \cf5 ANR
\fs28 \
Occurs when the UIthread is blocked for too long\
\

\fs36 Coroutines
\fs28 \
Kotlin solution for asynchronous and non-blocking programming, they are lightweight \'93thread\'94 because multiple coroutines can be created in one thread and suspend the work which will not block the thread so it can continue do other work\
\

\fs36 Dependency Injection
\fs28 \
Is a design pattern where the responsibility of creating an object is moved away from the calling class by creating a second class called injector which will provide the object the former class needs. This practice will make the class reusable, easy to refactor and easy to test\
\
In Android exist constructor injection and field injection for components like fragments and activities for which constructor injection ia not possible since the system itself will instantiate them. In Android there are two types of libraries, reflection solutions which connects dependencies at runtime and the other static solutions which creates code to connect dependencies at compile time\
\
It is bases on Inversion of control, also a design pattern, in which generic code controls the execution of specific code. \
\

\fs36 Hilt
\fs28 \
\pard\pardeftab720\partightenfactor0

\f0 \cf2 \cb3 Hilt is a dependency injection library for Android that reduces the boilerplate of doing manual dependency injection in your project. Is a default implementation of dagger, meaning it\'92s built on top of dagger. 
\fs32 \'a0
\fs28 Provides a standard way to use DI by providing containers for every Android class in your project and managing their lifecycles automatically.\
\
\pard\pardeftab720\partightenfactor0
\cf14 \cb15 At build time, Hilt generates\'a0{\field{\*\fldinst{HYPERLINK "https://developer.android.com/training/dependency-injection/dagger-basics"}}{\fldrslt \cf0 \ul \ulc0 Dagger}}\'a0components for Android classes. Then, Dagger walks through your code and performs the following steps:\cb1 \
\pard\tx220\tx720\pardeftab720\li720\fi-720\sa240\partightenfactor0
\ls1\ilvl0\cf14 \kerning1\expnd0\expndtw0 {\listtext	\uc0\u8226 	}\expnd0\expndtw0\kerning0
Builds and validates dependency graphs, ensuring that there are no unsatisfied dependencies and no dependency cycles.\
\ls1\ilvl0\kerning1\expnd0\expndtw0 {\listtext	\uc0\u8226 	}\expnd0\expndtw0\kerning0
Generates the classes that it uses at runtime to create the actual objects and their dependencies.\
\pard\pardeftab720\partightenfactor0
\cf2 \cb3 Hilt needs us to annotate application class and also android classes(activities, fragments, view models, services, broadcast receivers) that need its dependencies injected. For classes that needs their dependencies injected and that also will be injected to other classes but can not use annotations used for android classes we have modules(they have to be installed in a component) and in here we can tell hilt how to construct those classes(repositories, use cases, etc), in here we use either @binds or @provides annotations which we can use to accomplish same goal(tell hilt how to construct a class) in different ways for example when using @binds you need to use @inject annotation in the class construction while with @provides you don\'92t need that but the later is most useful to build classes we don\'92t own like retrofit. Hilt can provide default qualifiers to be able to inject some default objects such as @ActivityContext @ApplicationContext 
\f2\fs26 \cf0 \cb1 @ActivityContext private val context: Context 
\f0\fs28 \cf2 \cb3 \
\
Hilts has different components, such as SingletonComponent, ViewModelComponent and each of these components has a different lifecycle. There is also bindings scopes which will determine if a dependency/binding will receive a new instance or same instance of a binding. Example a binding with @viewModelScope required by two different bindings but both of  them will be injected in the same viewModel will receive same instance of the former binding, all other view models that requires this binding will receive a new instance\
\
Hilt reduces boilerplate code required to do DI while in dagger we would need to write all that boiler plate code manually.\
\
SOLID\
Popular set of design principles used in object oriented software development, its goal is to reduce dependencies so that engineers can change one area of software without impacting others but also intend to make software easier to understand, maintain, extend, scale and test. They tend to make development a little more difficult but it all worths it due to its long term benefits.\
\
	1. 
\f1\b Single responsibility principle
\f0\b0 : a class should have one and only one reason to change, meaning a class/module should do one\
	    thing only or to say it has to solve only one problem. Also we should consider this means the class/module has to be owned by one and\
             online ultimate business owner. For a class/module used to define schedule hours for drivers to leave and arrive locations has to have a its\
             own implementation of a similar class which uses this hours to calculate payments to drivers\
\
	2. 
\f1\b Open for extension closed for modification or just open close:
\f0\b0  Easy, you can extend the class or module not to only get same functionality\
	     but to add new, so open of extension and at the same time that class is closed for modification by extending it\
\
	3. 
\f1\b Liskov Substition:
\f0\b0  This is pretty much an extension of the previous principle, it states that every derived class should be substitutable for its\
	    parent class, so this ensures that every child class extends the base class without changing the behavior.\
\
	4. 
\f1\b Interface segregation:
\f0\b0  We should create small interfaces so the clients can call an implementation of it instead of having to implement/extend \
	    it themselves, This means we should prefer most of the times composition(has-a relationship) over inheritance(is-a relationship) because it\
	    would make the code less coupled, however inheritance is also needed sometimes.\
\
	5. 
\f1\b Dependency Inversion:
\f0\b0  High level modules should not depend on low level modules and both should depend on abstractions, a popular way\
	      to comply with this principle is with the dependency inversion/dependency injection pattern.\
\
\pard\pardeftab720\partightenfactor0

\fs36 \cf2 MVVM vs MVI
\fs28 \
Both architectural 
\f5\fs30 \cf16 patterns aim to separate concerns and improve code maintainability. Some differences are that MVI adds the concepts of unidirectional flow, which means the view is updated by the updates in the model that are produced by intents and also MVI handles immutable states to update the view from the model.\
\
	MVVM\
	Based on user interactions, no state as in MVI but just actions. The ViewModel is responsible to process user actions and update\
	view. This architecture data binding fits very well however view binding is also a good option. The view and viewModel usually\
	communicates by using the observable pattern by using live data or kotlin flows.\
		Model: Represents the business logic. It is consumed from the ViewModel\
		View: Repesents UI logic and interface(fragment/xml). It communicates to the viewModel\
		ViewModel: Interacts between view and model\
\
	MVI\
	This architecture is similar to MVVM in the sense it separates the view and the model but adds a new component, the intent\
	component. It features unidirectional data flow and states, this means the state, which is immutable, travels from the model to the\
	view only. The state is usually transmitted to the view using the observable pattern.\
		Model: The business logic that will live in the state of the app\
		View: Renders the state/model and triggers intents when user interacts with the app\
		Intent: Represents user interactions/actions that occur in the view and are dispatched to the model.\
\
View Binding Vs Data Binding\
Main difference is view binding can provide the same benefits as data binding with simpler implementation and better performances.\
\
Live Data vs Flows\
They pretty much do the same type of work, which is to let us implement the observable pattern very easily, however they have different features. The main difference is that live data is lifecycle aware while flows are not, this means we should be extra careful when using flows in lifecycle components to avoid doing work that is already been done. With flow we can use different intermediate operators.\
\
Process Death\
\
\

\fs36 Flows
\fs30 \
Flows are cold by nature meaning they don\'92t emit values until they are being collected. Cold Flows are streams of data that are created anew for each subscriber while hot flows are streams of data that are shared between subscribers and can emit new values at any time\
\
	
\fs36 Hot flows\
	
\fs30 Shared flow, state flow, callback flow, channel flow\
		Shared Flow\
		It was designed for event streamline and does not maintain any state. Suitable for emitting repetitive events such as button\
		clicks. New Subscribers can get previous emitted values from the cache\
\
		State Flow\
		Represents a single value that can be observed by multiple subscribers, it has to have an initial value\
\

\f7\b\fs36 Testing(JUnit, Mockito, Robolectric(UITests), Espresso(UITests), UIAutomator)\

\f5\b0\fs30 There is different types of testing but some of them are not treated in android\'92s documentation but we have the following types of tests:\
	-Exploratory: Manual tests in androids case using a cellphone\
	-End-to-end: more info below\
	-Component: This test integrates all the parts of an application that are not slow. Slow parts are external services accessed via I/O operations like a DB or HTTP server\
	-Integration: Tests \
	-Unit\
	\
Benefits are, rapid feedback on failures, early failure detection, safer code refactoring(no need to worry about regressions). There is Different types of test depending on the subject:\
- Functional testing: Does my app do what it\'92s supposed to?\
- Performance testing: Does it do it quickly and efficiently?\
- Accessibility testing: Does it work well with accessibility services?\
- Compatibility testing: Does it work well on every device and API level?\
\
There is scopes, depending on the size or degree of isolation:\
- Unit Tests/Small tests only verify a very small portion of the app, such as method or class. Fragments and activities should not have business logic so unit test these classes have little value\
- End-to-end tests/Big tests verify a larger part of the app at same time, such as whole screen or user flow\
- Medium tests, in between tests they verify integration between two or more units\
\
Tests can run on an Android device or on another computer\
- Instrumented tests: Run on Android devices, either physical or emulator. Usually they are UI tests, like launching app and interacting with it. They include End-to-end tests and integration tests. Activites and fragments can be tested using instrumented tests such as UI tests instead of unit tests.\
- Local tests: Run on your development machine or a server, they\'92re also called host-side effects. Usually small and fast tests. They include Unit tests, Integration Tests, Simulators\
\
However not all Unit Tests are local, and not all end-to-end tests run on a device, for example:\
\
- Big local tests: You can use an Android simulator that runs locally, such as robolectric.\
-Small instrumented test: You can verify your code works well with a framework feature, such as a SQLite database. You might run this test on multiple devices to check the integration with multiple versions of SQLite.
\f0\fs28 \cf2 \
\
Out of scope for android developers but good to know selenium is a very popular tool for automation testing.\
\
There is two directories for testing\
	androidTest - This directory should contain the tests that run on real or virtual devices. Integration tests, end-to-end tests, other tests where JVM alone cannot validate apps functionality\
	test - directory should contain tests that run on local machine. Unit tests, tests that run on a local JVM\
\
\pard\pardeftab720\partightenfactor0

\f1\b \cf2 Unit tests
\f0\b0 \
	Is a best practice to unit test the following classes/components:\
	- ViewModels or presenters\
	- Data layer, especially repositories. Most of data layer should be platform-independent. Database modules and remote data sources should be replaced with test doubles.\
	- Platform-independent layers like domain layer, use cases.\
	- Utility classes such as string manipulation and math\
\
Unit test should test edge cases like \
	-Math operations with negative number or zeros\
	-All possible network connection errors\
	-Corrupted data, such as malformed JSON\
	-Simulating full storage when saving a file\
\
UI tests\
	- Screen UI tests - Check critical user interactions in a single screen. They perform actions like clicking buttons, typing, checking visible states.\
	- User flow tests or Navigation Tests - Cover most common paths. Simulate a user moving through a navigation flow. They\'92re simple tests, useful for checking run-time crashes in initialization.\
\
Other tests\
	It exists more specialized tests such as screenshot tests, performance tests and monkey tests. You can categorize tests by purpose such as regressions, accessibility and compability\
\
Consider three things when planning test\
	1. Scope - How much code does the test touch?\
	2. Speed - How fast does the test run?\
	3. Fidelity - How real-world is the test? Like when a test needs to make a network request, does the test code actually makes the network request or does it fake it? If it actually talks with the network it means it has higher fidelity. 		Trade-off is that it could run slower or result in errors if network is down or could be costly to use.\
\

\f1\b Test Doubles
\f0\b0 \
Are components that another component(class/method/flow) needs to perform a test, there are different types:\
	- Fake : A working implementation of the class, its implementation works for tests but is unsuitable for production. Example: an in-memory DB, Don\'92t require a mocking framework and are lightweight. They are preferred\
	- Mock : Should behave as you program it to behave and has expectation about its interactions. Mocks will fail tests if their interaction don\'92t match the defined requirements. Usually created with a mocking framework. Example: Verify that 	a method in a DB is called exactly once.\
	- Stub : Shout behave as you program it to behave but doesn\'92t have expectations on its interactions. Usually created with a mocking framework. Stub uses state verification while mock uses behavior verification\
	- Dummy :  component that is passed around but not used, such as if you need to provide it as a parameter. Example: Empty functions passed as a click callback\
	- Spy :  A wrapper over a real object which also keeps track of some additional information, similar to mocks. Usually avoided for adding complexity. Fakes and mocks are pr\
	- Shadow\
\
When you execute local unit tests, the AGP includes a library that contains all the APIs of the Android Framework. Correct to the version used in your project. The library has all the public method and classes of those APIs, but the code inside is empty and if the methods are accessed test will throw an exception. So in your local tests you can access classes in the Android framework such as \'93Context\'94\
\
Mocking Android Dependencies\
	Typical problem is to find a class uses a string resource but since \'93Context\'94 class is empty we have to create a Mock or Stub of this class to be able to call the \'93getString()\'94 method but we would always return the same value when it is 	called\
\
\pard\pardeftab720\partightenfactor0

\f1\b\fs36 \cf2 Security
\f0\b0\fs28 \
Android system has built-in security features that reduce the frequency and impact of app security issues.\
	\
	Data Storage\
	There is three ways you can store the information, we list a few best practices with each type:\
		1.- Internal storage: Files in internal storage are only accessible to your app if you want to share your data with other processes use content providers.\
		2.- External storage: You should only store non sensitive data in here\
		3- Content Providers: Offers a structured storage mechanism that can be limited to your own app or exported to allow access by other apps.\
\
	Permissions\
	They have to be declared to access additional capabilities not provided by the sandbox/process/VM, like camera, bluetooth, etc. Do not request a permission if app does not require it, so minimize the app permissions.\
\
	Networking\
	Use HTTP and HTTPS\
\
\

\f1\b\fs36 CI/CD
\f0\b0\fs28 \
Is a set of operating principles and practices that enable development teams reliably deliver frequent code changes, \
\
CI is an engineering practice that allows developers to merge their code changes in a central repo to run automated builds and tests. It depends on automation tools to execute build and testing and its goal is to achieve a software-defined lifecycle that reduces the amount of effort required. All changes that go through the pipeline will be deployed to production automatically.\
\
CD practice that refers to the process of developing, testing, and delivering software code improvements. Its goal is to make deployments routine events that can happen at any time. It does require manual approval before deployment to production.\
\

\f1\b\fs36 DevOps
\f0\b0\fs28 \
Is a Collaborative culture that includes a set of practices, ideas, tools, technologies and processes that help to speed up the product development process.\
\
Operate(Docker, Kubernetes, Ansible, AWS) monitor(Nagios)\
\
Test Difference Between Mock Vs Stub Vs Fake\
\

\f1\b\fs36 Jenkins
\f0\b0\fs28 \
Is a program that runs as an automation server, it helps to automate parts of the software development lifecycle, so it facilitates CI/CD. It can make possible to distribute new updates to the Play Store with a single git push command.\
\
Android Platform Architecture\
The android operating system is multi-user linux system. It has 6 major components\
	1. Linux Kernel: I the foundation of the Android platform. The ART relies on kernel to work with threading and low-level memory management.\
	2. Hardware Abstraction Layer(HAL): Is a collection of modules which contains the interfaces that expose hardware functionalities/capabilities, each module expose a specific hardware component like camera, these capabilities are		provided then to the higher level java API framework\
	3. Android Runtime: It contains instances of the Android Runtime (ART) after Android9 each app runs in its own instance of the ART, runtimes create instances of the VM so each app/process runs in its own VM, ART read Dalvyk		Executable Files(DEX) which is optimized byte code. Ahead of time(AOT) and just-in-time (JIT) compilation and the capability to debug your app using profiler and breakpoints are features of the ART\
	4. Native C/C++ libraries: HAL and ART are built from code that requires native libraries written in C and C++. The functionality of some of these native libraries are expoed using Java Framework APIs that the Android platform provides,	for example OpenGL(native) is accessed through Android framework\'92s Java OpenGL API. You can access some of these libraries directly by using de NDK.\
	5. Java API Framework: The complete feature-set of the Android OS is available through  APIs written in Java Language. Here we have the component we talked about previously:\
		\
		*View System: There include all views, Activities belong here\
\
		*Managers: There are different managers for example we have a manager for each of the following: Activitiy, Location, Package, Notification, Telephony, Resource, Window\
\
		*Content Providers: They enable apps to access data from other apps.\
	6. System Apps: You can use them to leverage their functionality.\
\
Activity Vs Fragment\
Activity is a component of an android app in which we draw UI, fragment can not live by itself it can only live inside an activity and we also draw UI in this class. Fragments don\'92t need to be declared in manifest.xml file while activities do need to.\
	\
	Passing data between Activites\
	We can either use bundle to wrap a key value map of data we want to pass to another activity or add extras to the intent that will launch the other activity, we also have the option of using a viewModel to 	share data\
	\
	Passing Data between Fragments\
	We should use the navigation component and we can define safe-args which are passed in the navigation actoins to pass values, we can still pass bundles through the navController navigations or a shared view model if data is too		much.\
\
\pard\tx720\tx1440\tx2160\tx2880\tx3600\tx4320\tx5040\tx5760\tx6480\tx7200\tx7920\tx8640\pardirnatural\partightenfactor0

\fs24 \cf0 \cb1 \kerning1\expnd0\expndtw0 \'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\
\
Declarative/Reactive(Compose) vs Imperative(XML) Ui\
\
	Comparison\
	\

\itap1\trowd \taflags1 \trgaph108\trleft-108 \trbrdrt\brdrnil \trbrdrl\brdrnil \trbrdrr\brdrnil 
\clvertalc \clshdrawnil \clwWidth3240\clftsWidth3 \clheight291 \clbrdrt\brdrs\brdrw20\brdrcf17 \clbrdrl\brdrs\brdrw20\brdrcf17 \clbrdrb\brdrs\brdrw20\brdrcf17 \clbrdrr\brdrs\brdrw20\brdrcf17 \clpadl100 \clpadr100 \gaph\cellx2880
\clvertalc \clshdrawnil \clwWidth5960\clftsWidth3 \clheight291 \clbrdrt\brdrs\brdrw20\brdrcf17 \clbrdrl\brdrs\brdrw20\brdrcf17 \clbrdrb\brdrs\brdrw20\brdrcf17 \clbrdrr\brdrs\brdrw20\brdrcf17 \clpadl100 \clpadr100 \gaph\cellx5760
\clvertalc \clshdrawnil \clwWidth4460\clftsWidth3 \clheight291 \clbrdrt\brdrs\brdrw20\brdrcf17 \clbrdrl\brdrs\brdrw20\brdrcf17 \clbrdrb\brdrs\brdrw20\brdrcf17 \clbrdrr\brdrs\brdrw20\brdrcf17 \clpadl100 \clpadr100 \gaph\cellx8640
\pard\intbl\itap1\tx720\tx1440\tx2160\tx2880\tx3600\tx4320\tx5040\tx5760\tx6480\tx7200\tx7920\tx8640\pardirnatural\partightenfactor0
\cf0 Aspect\cell 
\pard\intbl\itap1\tx720\tx1440\tx2160\tx2880\tx3600\tx4320\tx5040\tx5760\tx6480\tx7200\tx7920\tx8640\pardirnatural\partightenfactor0
\cf0 Imperative\cell 
\pard\intbl\itap1\tx720\tx1440\tx2160\tx2880\tx3600\tx4320\tx5040\tx5760\tx6480\tx7200\tx7920\tx8640\pardirnatural\partightenfactor0
\cf0 Declarative/Reactive\cell \row

\itap1\trowd \taflags1 \trgaph108\trleft-108 \trbrdrl\brdrnil \trbrdrr\brdrnil 
\clvertalc \clshdrawnil \clwWidth3240\clftsWidth3 \clheight310 \clbrdrt\brdrs\brdrw20\brdrcf17 \clbrdrl\brdrs\brdrw20\brdrcf17 \clbrdrb\brdrs\brdrw20\brdrcf17 \clbrdrr\brdrs\brdrw20\brdrcf17 \clpadl100 \clpadr100 \gaph\cellx2880
\clvertalc \clshdrawnil \clwWidth5960\clftsWidth3 \clheight310 \clbrdrt\brdrs\brdrw20\brdrcf17 \clbrdrl\brdrs\brdrw20\brdrcf17 \clbrdrb\brdrs\brdrw20\brdrcf17 \clbrdrr\brdrs\brdrw20\brdrcf17 \clpadl100 \clpadr100 \gaph\cellx5760
\clvertalc \clshdrawnil \clwWidth4460\clftsWidth3 \clheight310 \clbrdrt\brdrs\brdrw20\brdrcf17 \clbrdrl\brdrs\brdrw20\brdrcf17 \clbrdrb\brdrs\brdrw20\brdrcf17 \clbrdrr\brdrs\brdrw20\brdrcf17 \clpadl100 \clpadr100 \gaph\cellx8640
\pard\intbl\itap1\tx720\tx1440\tx2160\tx2880\tx3600\tx4320\tx5040\tx5760\tx6480\tx7200\tx7920\tx8640\pardirnatural\partightenfactor0
\cf0 Programming Style\cell 
\pard\intbl\itap1\tx720\tx1440\tx2160\tx2880\tx3600\tx4320\tx5040\tx5760\tx6480\tx7200\tx7920\tx8640\pardirnatural\partightenfactor0
\cf0 Step-by-step instructions\cell 
\pard\intbl\itap1\tx720\tx1440\tx2160\tx2880\tx3600\tx4320\tx5040\tx5760\tx6480\tx7200\tx7920\tx8640\pardirnatural\partightenfactor0
\cf0 High-level descriptions \cell \row

\itap1\trowd \taflags1 \trgaph108\trleft-108 \trbrdrl\brdrnil \trbrdrr\brdrnil 
\clvertalc \clshdrawnil \clwWidth3240\clftsWidth3 \clbrdrt\brdrs\brdrw20\brdrcf17 \clbrdrl\brdrs\brdrw20\brdrcf17 \clbrdrb\brdrs\brdrw20\brdrcf17 \clbrdrr\brdrs\brdrw20\brdrcf17 \clpadl100 \clpadr100 \gaph\cellx2880
\clvertalc \clshdrawnil \clwWidth5960\clftsWidth3 \clbrdrt\brdrs\brdrw20\brdrcf17 \clbrdrl\brdrs\brdrw20\brdrcf17 \clbrdrb\brdrs\brdrw20\brdrcf17 \clbrdrr\brdrs\brdrw20\brdrcf17 \clpadl100 \clpadr100 \gaph\cellx5760
\clvertalc \clshdrawnil \clwWidth4460\clftsWidth3 \clbrdrt\brdrs\brdrw20\brdrcf17 \clbrdrl\brdrs\brdrw20\brdrcf17 \clbrdrb\brdrs\brdrw20\brdrcf17 \clbrdrr\brdrs\brdrw20\brdrcf17 \clpadl100 \clpadr100 \gaph\cellx8640
\pard\intbl\itap1\tx720\tx1440\tx2160\tx2880\tx3600\tx4320\tx5040\tx5760\tx6480\tx7200\tx7920\tx8640\pardirnatural\partightenfactor0
\cf0 UI definition\cell 
\pard\intbl\itap1\tx720\tx1440\tx2160\tx2880\tx3600\tx4320\tx5040\tx5760\tx6480\tx7200\tx7920\tx8640\pardirnatural\partightenfactor0
\cf0 Explicitly create and manage UI elements\cell 
\pard\intbl\itap1\tx720\tx1440\tx2160\tx2880\tx3600\tx4320\tx5040\tx5760\tx6480\tx7200\tx7920\tx8640\pardirnatural\partightenfactor0
\cf0 Describe UI structure and interactions\cell \row

\itap1\trowd \taflags1 \trgaph108\trleft-108 \trbrdrl\brdrnil \trbrdrr\brdrnil 
\clvertalc \clshdrawnil \clwWidth3240\clftsWidth3 \clbrdrt\brdrs\brdrw20\brdrcf17 \clbrdrl\brdrs\brdrw20\brdrcf17 \clbrdrb\brdrs\brdrw20\brdrcf17 \clbrdrr\brdrs\brdrw20\brdrcf17 \clpadl100 \clpadr100 \gaph\cellx2880
\clvertalc \clshdrawnil \clwWidth5960\clftsWidth3 \clbrdrt\brdrs\brdrw20\brdrcf17 \clbrdrl\brdrs\brdrw20\brdrcf17 \clbrdrb\brdrs\brdrw20\brdrcf17 \clbrdrr\brdrs\brdrw20\brdrcf17 \clpadl100 \clpadr100 \gaph\cellx5760
\clvertalc \clshdrawnil \clwWidth4460\clftsWidth3 \clbrdrt\brdrs\brdrw20\brdrcf17 \clbrdrl\brdrs\brdrw20\brdrcf17 \clbrdrb\brdrs\brdrw20\brdrcf17 \clbrdrr\brdrs\brdrw20\brdrcf17 \clpadl100 \clpadr100 \gaph\cellx8640
\pard\intbl\itap1\tx720\tx1440\tx2160\tx2880\tx3600\tx4320\tx5040\tx5760\tx6480\tx7200\tx7920\tx8640\pardirnatural\partightenfactor0
\cf0 Updates\cell 
\pard\intbl\itap1\tx720\tx1440\tx2160\tx2880\tx3600\tx4320\tx5040\tx5760\tx6480\tx7200\tx7920\tx8640\pardirnatural\partightenfactor0
\cf0 Manual management of Updates\cell 
\pard\intbl\itap1\tx720\tx1440\tx2160\tx2880\tx3600\tx4320\tx5040\tx5760\tx6480\tx7200\tx7920\tx8640\pardirnatural\partightenfactor0
\cf0 Automatic reconciliation of UI changes\cell \row

\itap1\trowd \taflags1 \trgaph108\trleft-108 \trbrdrl\brdrnil \trbrdrt\brdrnil \trbrdrr\brdrnil 
\clvertalc \clshdrawnil \clwWidth3240\clftsWidth3 \clbrdrt\brdrs\brdrw20\brdrcf17 \clbrdrl\brdrs\brdrw20\brdrcf17 \clbrdrb\brdrs\brdrw20\brdrcf17 \clbrdrr\brdrs\brdrw20\brdrcf17 \clpadl100 \clpadr100 \gaph\cellx2880
\clvertalc \clshdrawnil \clwWidth5960\clftsWidth3 \clbrdrt\brdrs\brdrw20\brdrcf17 \clbrdrl\brdrs\brdrw20\brdrcf17 \clbrdrb\brdrs\brdrw20\brdrcf17 \clbrdrr\brdrs\brdrw20\brdrcf17 \clpadl100 \clpadr100 \gaph\cellx5760
\clvertalc \clshdrawnil \clwWidth4460\clftsWidth3 \clbrdrt\brdrs\brdrw20\brdrcf17 \clbrdrl\brdrs\brdrw20\brdrcf17 \clbrdrb\brdrs\brdrw20\brdrcf17 \clbrdrr\brdrs\brdrw20\brdrcf17 \clpadl100 \clpadr100 \gaph\cellx8640
\pard\intbl\itap1\tx720\tx1440\tx2160\tx2880\tx3600\tx4320\tx5040\tx5760\tx6480\tx7200\tx7920\tx8640\pardirnatural\partightenfactor0
\cf0 Dataflow\cell 
\pard\intbl\itap1\tx720\tx1440\tx2160\tx2880\tx3600\tx4320\tx5040\tx5760\tx6480\tx7200\tx7920\tx8640\pardirnatural\partightenfactor0
\cf0 Often complex bidirectional \cell 
\pard\intbl\itap1\tx720\tx1440\tx2160\tx2880\tx3600\tx4320\tx5040\tx5760\tx6480\tx7200\tx7920\tx8640\pardirnatural\partightenfactor0
\cf0 Unidirectional: Data/Model changes triggers UI updates\cell \lastrow\row
\pard\tx720\tx1440\tx2160\tx2880\tx3600\tx4320\tx5040\tx5760\tx6480\tx7200\tx7920\tx8640\pardirnatural\partightenfactor0
\cf0 \
	Compose\
		Pros\
		- Far less boilerplate\
		- Much easier to write custom component\
		- Much easier to animate component\
		- Better tooling(Previews, live edit, etc)\
		- Events-up state-down design feels more modern\
		- Shader support is \'93easier\'94 (AGSL)\
		- Easy to integrate to existing apps\
		- Because it is a library backwards compatibility is easy to accomplish in contrast with XML which has a lot of properties you can\'92t use depending on your minimum API\
		- Easier to test, very similar to do Unit testing as opposite of testing XML for which you had to instantiate the whole app with mocks just to test a view\
		\
		Cons\
		- If no reactive programming experience there is a learning curve\
		- Side effects may be difficult to handle or avoid\
		- Reactive programming could make debugging tricky, like, \'93why is my app recomposing every second?\'94\'92\
\
\
\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97
\fs28 \cf2 \cb3 \expnd0\expndtw0\kerning0
\
\pard\pardeftab720\partightenfactor0
\cf2 \
Lifecycle\
Is the different states an activity and fragments go through as the user navigates through, out of, and back to the app.\
	Activity\
	A very commonly used is onCreate which is the first method in the lifecycle\
		1. onCreate - only happens once, you usually implement start up logic here, we configure the UI here, you can save the sate of the activity which you can then use in this method by overriding	onSaveInstanceState method\
		2. onStart\
		3. onResume - the Ui is visible \
		4. onPause \
		5. onStop - from here the onRestart could be launched and go back to onStart\
		6. onDestroy\
	\
	Fragment\
	Manages lifecycles through implementing LifecycleOwner, you can access a Lifecycle object through getLifecycle() method, this object has an enum called State that represents the current state. It exists 	lifecycle aware components.		Fragments also have a LifecycleOwner which can be accessed via getViewLifecycleOwner method. It has more phases than activity however since they are so many that usually what we care about is more the state than the method		directly. However two important methods of the cycle are the following\
		1. onCreate - view attached to Fragment Manager but an instance of the view does not exist yer\
		2. onCreateView - view instance its returned in these method, that mean the view is created\
	the states are \
		1. Initialized\
		2. Created\
		3. Started\
		4. Resumed\
		5. Resumed\
		6. Destroyed\
\
Fragment Manager\
Is responsible to monitor and move the fragment to the correct lifecycle state but also to attach/detach the fragment to/from the host activity. You can use the findFragmentById() method to find fragment. onAttach() is always called before any lifecycle state changes, onDetach is called when it is removed from manager, Fragment transactions provide more details on these two methods.\
\
\
\pard\pardeftab720\partightenfactor0

\fs36 \cf2 Navigation Controller\
\pard\pardeftab720\partightenfactor0

\fs28 \cf2 We can talk of five different concepts, \
	1.- Navigation graph is an xml file in which we define possible destinations in the app and the connections between them.\
	2.- Navigation Controller: It allows us to navigate between destinations and manage the back stack.Is in charge of adding, replacing and removing fragments as the user navigates through the app.\
	3.- Safe Args: You define the arguments in the graph and a grade plugin generates type-safe classes for passing the arguments.\
	4.- Animation: You can animate fragment transitions\
	5.- Deep Links: This simulates manual navigation, allowing you to navigate from web links or push notifications\
\pard\pardeftab720\partightenfactor0

\fs36 \cf2 \
	Proguard Considerations
\fs28 \
	If you\'92re using code shrinking, you need to prevent your Parcelable, Serializable and Enum class names from being obfuscated as part of the minification process.\
\
Publish App to Playstore\
All the steps listed here can be configured in a CI/CD server to automate them, also you can configure it to publish builds to an internal testing distribution channel as the service offered by Firebase. If app is larger than 150MB you have to publish them using either \'93Play Feature Delivery\'94 or \'93Play Asset Deliver\'94. You have go through the following process to prepare your app for release to play store:\
\
	1. Prepare EULA, get cryptographic keys(upload key, signing key these two are used in play app signing and keystroke), create application icon, end-user license agreement.\
	2. Configure You app for release - Make sure loggin is disable by turning off \'93isDebugable = false\'94 flag, and set the apps version info, \'93versionCode\'94 which is an integer that will increment on every release to store and \'93versionName\'94 		wich is the actual version name the users will see. Also define the \'93minSdk\'94 and \'93targetSdk\'94.\
	3. Build and sign the release version of app\
	4. Test release version of the app - Test it before relsease. Firebase Text lab helps us test code in a variety of devices and configurations.\
	4. Update App resources - Make sure the multimedia files and graphics are the ones you need. Usually you have to make sure the server is staged on the proper production servers\
	6. Prepare Remote Server and devices the depends on - make sure they are secure and production ready\
\
When your app is configured following the previous steps you can then do the following to release it:\
	1. Prepare Promotional Material - Create screenshots, videos, graphics and promotional text to promote your app and leverage Google Play marketing and publicity capabilities\
	2. Configure Options and Upload Assets - Using Google Play Console you can set different configurations like the countries you want to reach, languages you want to use, and price you will charge if so.\
	3. Publish the release version of the app - If everything is configures correctly you just have to choose \'93publish\'94 and wait for it to pass Google Play review process\
\
If an app size is greater than 150MB you can either use \'93Play Asset Delivery\'94 or \'93Play Feature Delivery\'94 to upload it to play store.\
\
	Google App Signing\
	Is a Google Play Store service for developers/publishers that helps you protect your application\'92s signing key. You can have google generate you signing key or you can provide one yourself, be aware after uploading your signing key\
	you can not retrieve a copy. After you configure App Signing you can not retrieve a copy of the app signing key. Depending on your configuration your first upload key may be different from the app signing key, you will use your upload\
	key to sing your app and Google will use this key to verify your identity and sign your app with the App Signing Key, you can request a change/new upload key but not a signing key this is why is you would prefer using this service as if\
	you ever lose your App Signing Key you would not be able to upload updates to your app again. \
\
\
Code Shrinking\
We use this feature to make the app as small as possible as enabling shrinking will shrink code for example by the shrinker can change a class and variables names with shorter names to reduce DEX size this is also known as obfuscation. Besides of using obfuscation to shrink the size of the app another process will also help to shrink the app even more and that is possible by running optimizations as if shrinker/R8 detects code that is never used it will remove it.\
\
Security what wi-Fi OK more is my best friend instructions\
If using WebView to display paid content or if using Javascript interfaces make sure disable debugging with \'93setWebContentsDebugginEnabled(false)\'94 otherwise info can be extracted.\
\

\fs36 Modularization
\fs28 \
Is the process of separating and creating clear boundaries between logical components of code\
\
Project Overview\
In this documentation you can find the role of each package like the res/, src/, etc\
\

\fs36 D8/R8
\fs28 \
D8 is Dexer tool that converts java byte code to DEX code. R8 is a java program shrinking and minification tool that converts java byte code to optimized DEX code. DEX is a type of executable file used by the Dalvik virtual machine in android devices. They contain Dalvik byte code which can be executed by Android\'92s runtime environment and is optimized for mobile devices.\
	\
	R8 compiler consumes class files and can output either DEX for Android apps or class files for java apps(consider this feature when trying to optimize a Java/JavaFx app)\
\

\fs36 Desugaring
\fs28 \
Android and gradle 4 or higher now supports java8 code without  requiring a minimum API level for your app. Its possible through desugaring which are transformations of byte code as part of the D8/R8 compilation of class files into DEX code, this is how the default toolchain implements new language features.
\f5 \cf5 \cb1 \
\pard\tx720\tx1440\tx2160\tx2880\tx3600\tx4320\tx5040\tx5760\tx6480\tx7200\tx7920\tx8640\pardirnatural\partightenfactor0
\cf5 \
\pard\tx720\tx1440\tx2160\tx2880\tx3600\tx4320\tx5040\tx5760\tx6480\tx7200\tx7920\tx8640\pardirnatural\partightenfactor0

\fs36 \cf5 Event-Driven Programming
\fs28 \
Is a type of programming in which the flow of execution is determined by events which are triggered by user actions just like a click, or type keyboard keys. Is commonly used in graphical user interfaces. Android uses some of these features in its development for example clicks and views lifecycle can trigger actions.\
\

\fs36 Software Framework
\fs28 \
Is an abstraction/software used to build and deploy apps that is part of a larger software platform, this software/abstraction provides generic functionality that can be changed by the framework user by overriding the framework default implementation.\
\
\pard\pardeftab720\partightenfactor0

\f0 \cf18 \cb3 frameworks may include support programs, compilers, code libraries, toolsets, and APIs that bring together all components to enable development of project or system\
\pard\pardeftab720\partightenfactor0

\f5 \cf5 \cb1 \
\pard\pardeftab720\partightenfactor0

\fs36 \cf5 Loose Coupling/High Cohesive
\fs28 \
Loose coupling is a feature or practice in which components of software are weakly associated, meaning changes in a component least affect the other component existence or performance and High cohesive is the measure of relationship between the methods and properties/data of a class.\
\pard\tx720\tx1440\tx2160\tx2880\tx3600\tx4320\tx5040\tx5760\tx6480\tx7200\tx7920\tx8640\pardirnatural\partightenfactor0
\cf5 \
Activity Rotation\
When an activity rotates it is destroyed and a new instance is created in the new orientation and the activity lifecycle repeats from the \'93onRestart\'94\
\
Dialog vs DialogFragment\
Dialogs depend entirely on activities. If the screen is rotated, dialog is dismissed while dialog fragments take care of orientation and config changes as well\
\
Data Structures\
\
\
\
\
\
\
\
\
\
\
\
}