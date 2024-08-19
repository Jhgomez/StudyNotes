{\rtf1\ansi\ansicpg1252\cocoartf2761
\cocoatextscaling0\cocoaplatform0{\fonttbl\f0\fswiss\fcharset0 Helvetica;\f1\fnil\fcharset0 HelveticaNeue;\f2\fmodern\fcharset0 Courier;
\f3\fswiss\fcharset0 Helvetica-Bold;\f4\fnil\fcharset0 HelveticaNeue-Medium;\f5\froman\fcharset0 Times-Roman;
}
{\colortbl;\red255\green255\blue255;\red11\green12\blue12;\red255\green255\blue255;\red88\green118\blue71;
\red32\green32\blue32;\red5\green36\blue44;\red23\green56\blue124;\red0\green0\blue0;\red191\green191\blue191;
}
{\*\expandedcolortbl;;\cssrgb\c4706\c5098\c5490;\cssrgb\c100000\c100000\c100000;\csgenericrgb\c34510\c46275\c27843;
\csgenericrgb\c12549\c12549\c12549;\cssrgb\c784\c18824\c22745;\cssrgb\c11373\c29412\c56078;\cssrgb\c0\c0\c0\c80000;\csgray\c79525;
}
{\*\listtable{\list\listtemplateid1\listhybrid{\listlevel\levelnfc23\levelnfcn23\leveljc0\leveljcn0\levelfollow0\levelstartat1\levelspace360\levelindent0{\*\levelmarker \{hyphen\}}{\leveltext\leveltemplateid1\'01\uc0\u8259 ;}{\levelnumbers;}\fi-360\li720\lin720 }{\listname ;}\listid1}}
{\*\listoverridetable{\listoverride\listid1\listoverridecount0\ls1}}
\margl1440\margr1440\vieww30040\viewh17760\viewkind0
\pard\tx720\tx1440\tx2160\tx2880\tx3600\tx4320\tx5040\tx5760\tx6480\tx7200\tx7920\tx8640\pardirnatural\partightenfactor0

\f0\fs24 \cf0 \
Software Development Life Cycle(SDLC)\
Is a methodology that outlines the various stages involve in Android application development. By understating each phases\'92s requirement and activities, \
developers can ensure that the app meets end user\'92s needs, performs as intended and is released on time and within budget. We can talk about 7 \
:phases\
	\
	1. Planning: Here goals and objectives are defined, eg: create a simple new user friendly chat app that can handle millions of messages while 	having high performance. The should evaluate the feasibility of the project in terms of budget, resources and time.\
\
	2. Analysis: The team should gather information about app requirements from different stakeholders, like users. Like what type of interface or 	features the user would like to have. The goal is to understand needs of end-users, business requirements and technical specifications\
\
	3. Design: Team should ensure the app will meet the requirements gathered in the analysis phase. Includes several activities like creating the user	interface, designing the app\'92s architecture, defining the data model etc.\
\
	4. Implementation: The team develops the app. Includes activities like coding, testing and debugging.\
	\
	5. Testing: The team test the app to find any bugs, there is different types of testing like unit test, integration test, system testing and acceptance	testing.\
\
	6. Deployment: App is deployed and made available to end users. It involves activities like publishing app to Google Play Store, configure app for	different devices and platforms, documenting app. The team could write a user manual or help documentation to guide end-users on how to use it\
\
	7. Maintenance: The team maintain the app by providing updates, fixing bugs and addressing issues that may arise. It includes activities like app	performance monitoring, gather user feedback and releasing new versions. \
\
\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\
\
Gradle Enterprise = Develocity\
\
\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\
\
Perfetto\
Tool used for doing System profiling, App tracing and tracing analysis for Linux and Android. These tools helps you find where CPU cycles and memory are spent at the end time of inspection\
\
\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\
\
Speed Scope App\
Is an app we can use for profiling IOS apps, it can import instruments(Xcode profiler tool) profiles and show them as a frame graph \
\
\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\
\
Resource Qualifiers\
\
Allows us to define different resource packages/folders that will be used to store/retrieve resources for a specific  in to display the right resource in \
different situations such as in screen size or screen orientation, etc\
\
\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\
\
Fastlane\
Is a suite of app automation tools, it can be used to do CI(continuous integration) more specifically to sign and push apps apps to the playstore, it can also be used to create a \
private apps, automate screenshots and manage beta deployments\
\
\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\
\
StrictMode\
Is a developer tool which detects things you might be doing by accident and brings them to your attention so you can fix them\
\
\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\
\
Input method editor(IME)\
Is a user control that lets user enter text, like the keyboard on the screen\
		\
\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\
\
Recomposition\
\
Is the process of calling your composables again when inputs change. The composables will go through the three phases: composition, layout and drawing\
\
\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\
\
Saved State Module\
\
System initiated process death is when the OS kills the process due to resource constraints or configuration change.\
\
Allows to use SavedStateHandle API as backup of system-initiated process death, meaning you can persist info using it and this API is basically a key-value\
map which you can use to write/read values. There is different APIs in this module which we use depending on what it needs to be persisted as if you want\
to persist state used in business logic, hold it in a ViewModel and save it using SavedStateHandle and for state used in UI logic, use \
onSaveInstanceState/onRestoreInstanceState or rememberSaveable in Compose.\
\
Data stored in saved instance state is transient state that depends on user input or navigation such as scroll position of a list, the ID of the item the user wants\
more detail about, the in-progress selection of user preferences or input in text fields\
\
You can accept a SavedStateHandle as a constructor argument to your ViewModel\
\
	Supported Types\
	Data stored in DaveStateHandle is saved and restored as a \'93Bundle\'94, along with the rest of the \'93savedInstanceState\'94 for the activity or fragment. You \
	store/retrieve the same data types as a \'93Bundle\'94, which are basically all Number class child(double, int, etc) string, charsequence, etc and all	Parcelable and Serializable child classes meaning you can implement this interfaces by adding @Parcelize Kotlin annotation or implementing 	Parcelable directly to be able to store a child class\
\
\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\
\
A/B testing\
\
Is a way to improve an application by testing new features on a subset group of users, this helps us avoid code regression.\
\
	Firebase Remote Config\
\
	Allows us define a local variable with a default value that we can change remotely to change app appearance and behavior without reinstalling a 	new build. This tool will let you do quick roll-outs, provide variations on app\'92s user experience by app version, and do A/B testing\
\
	Firebase A/B Testing\
	\
	It lets us start an \'93experiment\'94, we can experiment with either notifications, remote config or in-app messaging. After choosing the type of test you have	to provide a description, define the subset of users by version, build number, languages and other options, You can select the experiment to track other	metrics in the objectives section. \
\
\
\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\
\
Location\
\pard\pardeftab720\partightenfactor0

\f1\fs26 \cf2 \expnd0\expndtw0\kerning0
\
\pard\pardeftab720\sa330\partightenfactor0

\fs30 \cf2 \cb3 Deciding between\'a0LocationManager\'a0or\'a0FusedLocationClient\'a0in Android is pretty easy, just go for FusedLocationClient, since it will save power and it is recommended as a best practice.\

\f0\fs24 \cf0 \cb1 \kerning1\expnd0\expndtw0 \
\pard\tx720\tx1440\tx2160\tx2880\tx3600\tx4320\tx5040\tx5760\tx6480\tx7200\tx7920\tx8640\pardirnatural\partightenfactor0
\cf0 \
\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\
\
System Services\
\
Helps us expose the lower level hardware functionalities to the higher level Java API framework. We access system services through managers such as \
Notifiaction manager, alarm manager, we can create different instances of each manager as needed and from different apps, activities or fragments but \
the system will handle all request made by all of those managers instances using only one instance of a service, each service run on a system server and\
there is different types of them, for example the display service which handles surface fingers interactions run on the system server however the camera\
service run on the media server.\
\
	Creating a Custom Service\
	it is possible by using the AOSP, since sometimes android could be installed in a different device other than a computer this is useful because it lets us \
	provide new hardware functionality to developers, the following steps doesn\'92t cover installing drivers to Android Linux Kernel which would also be 	required before adding the following code:\
\
	1.- Create an Android Interface Definition Language(AIDL) You have to define an interface which will have the contract of what a client can do with/in	this service, it uses java syntax, it has to have an \'93.aidl\'94 file extension, and has to be placed in the \'93android.os\'94 package (framework/base/core/java/android/os)\
\
	2.- Create an implementation of the interface, it has to be \'93.java\'94 file but it will be implementing an interface with the same name as named in the	prev step but with \'93.stub\'94 added to it so \'93exampleInterface.stub\'94 would be the name of the interface, define this in the \'93com.android.server\'94 package	(framework/base/services/core/java/com/android/server). Note: Since it exists different server we could run it in a custom or just different server but 	how to do this is something we will have to find out if we ever need to do it\
\
	3. Add AIDL in Android MK, open frameworks/base/Android.mk file and add the AIDL file path of the service you just created 	like the following path: core/java/android/os/iCustomeService.aidl\
\
	4. Add/register your service in the server it will run in(at this moment I only know how to this only using the system server and not a custom server or 	just a different server other than the system server), the following code has to be added to the \'93SystemServer.java\'94 file(frameworks/base/services/java/com	/android/server):\
	\
		try \{\
			Slog.i(TAG, \'93My custom service\'94)\
			ServiceManager.addService(\'93Test\'94, new CustomService())\
		\} catch (Throwable e) \{\
			Slog.e(TAG, \'93Failure starting service\'94,e)\
		\}\
\
	5.- Register service in \'93Context.java\'94 file, the file path is the following: \'93frameworks/base/core/java/android/content\'94, just add the following line of code:\
	\
		public static final CUSTOM_SERVICE = \'93service-name\'94;\
\
	6.- Register service in \'93SystemServerRegistry.java\'94 file. As previously mentioned the application doesn\'92t have direct access to the service instead this is	possible through a manager or several instances of the manager which will delegate all requests to a single/same instance of the custom service. This file	path is: \'93framework/base/core/java/android/app\'94. Just add the following code:\
		\
		registerService(\
			Context.CUSTOM_SERVICE,\
			CustomServiceMgr.class,\
			new CacheServiceFetcher<CustomServiceMgr> \{\
				@Override\
				public CustomServiceMgr(ContextImpl ctx) \{\
					return new CustomServiceMgr();\
				\}\
			\}\
		) \
\
	7.- Create the manager class for service, the file/class can be named however but it is a \'93.java\'94 file, so it is a class, the path would be \'93framework/base/core/java/android/os\'94.\
	\
		public class CustomServiceMgr \{\
			\
			ICustomService mService = null;\
			 \
			private CustomServiceMgr getService() \{\
				if (mService != null) return service\
				try \{\
					IBinder binder = ServiceManager.getService(Context.CUSTOM_SERVICE):\
					mService = ICustomService.Stub.asInterface(binder);\
					\
				\} catch(Exception e) \{ \}\
				\
				return mService;\
			\}\
\
			public String getServiceName() \{\
				// here you can see all functionality is actually delegated to the service and is not processed in the manager itself\
				return getService().getServiceName();\
			\}\
			\
\
			public int add(int a, int b) \{\
				return getService().add(a, b); \
				// just an example function available in the example service, we just want to demonstrate the manager delegates all computations to the service\
			\}\
			\
		\}\
\
	8.- Use service in your app, \
\
		val manager = getSystemService(Context.CUSTOM_SERVICE) as CustomServiceMgr\
		val name = manager.getServiceName()\
		val sum = manager.add(1, 4)\
		\
		Log.i(TAG, sum)\
		Log.i(TAG, name)\
\
\
\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\
\
reference: https://www.youtube.com/watch?v=egVnhfuVJYg&t=11s\
\
Use Compose Runtime to create a custom client library\
\
The process is when compiling composable functions the compose compiler injects a \'93Composer\'94 to each function, the composer then adds the composables info to a \'93Slot Table\'94\
this table contain two things, the \'93slots\'94 which contain actual composables data and the \'93Groups\'94 which contain composables metadata, then the composer which is also recording\
composables changes will pass all this info to the applier which creates the composables node tree, the nodes are created by the composables, this means the each composable \
function emits a node, there are two types of nodes in Android Compose, one is \'93ComposeNode\'94 and the other is \'93ReusableComposeNode, and then the client integration which in\
Compose is what you would know as the \'93setContent\'94 function will create a Recomposer which is in charge of monitoring state variables changes and inform the functions observing \
that state of changes, the client integration also is in charge of getting the composables, create a frame clock, create initial composition, refresh the frame\
\
In the example provided Apache POI was used to enable custom Nodes to write/create a power point file/slide from a custom composable. The following are the steps that we \
need to follow in order to be able to accomplish the described task:\
	\
	1.- create custom nodes, by creating a contract/interface, we could just define a method called render, and a val property called children which would be a mutable list of	type of itself interface. Then we create the custom nodes by implementing this interface and we can add different properties to each node\
	\
	2.-  Create a custom applier by implementing from the  \'93AbstractApplier<T>(root: T)\'94 class that exists somewhere in the Jetpack Compose library and this provides a contract\
	to insert, remove, move nodes to the three. The function of an applier is exactly that, inserting, removing, moving nodes in/to/out the tree and this info is received from the	slot table through the composer\
\
	3.- Create composables, the functions that will emit the nodes that we previously created, the following composable would be an example of a composable that is a \'93container\'94\
	\
\
		@Composable\
		fun Slide(content: @Composable () -> Unit) \{\
			ComposeNode<MyCustomNode, MyCustomApplier>(\
				factory = ::MyCustomNode,\
				update = \{\},\
				content = content\
			)\
		\}\
\
	4.- Client Integration: create a function that will be the entry point for our custom composables\
	\
		fun runCustomComposables(content: @Composable () -> Unit) = runBlocking \{\
			val fameClock = BraodcastFrameClock()\
			val recomposer = Recomposer(coroutineContext + framClock)\
			val rootNode = SlideNode() // this Is the root of the compose node tree\
\
			//create initial composition\
			val composition = Composition(\
				applier = MyCustomApplier,\
				parent = recomposer\
			)\
\
			composition.setContent(content)\
			\
			// we would also need to create logic to observe changes, run recomposer, send frame to clock\
\
			rootNode.render()\
		\}\
\
	5.- Use all previous component, just call it anywhere in the app\
\
\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\
\
SDK Extensions\
	\
	Project Treble\
	This project aimed to separate hardware specific code from the OS code,  that means the vendor implementation of an Android version was separated from the core OS framework\
\
	This helped to modularize system components as in the following diagram, each line is a \'93layer\'94\
		\
		Android Apps.  \'97\'97\'97\'97\'97\'97\'97\'97\'97  OEM Apps & Customizations\
		Android OS framework(Modules, which are modularized system components live inside the framework) \'97 this can be updated independently of any OEM implementation		Vendor Implementation + Kernel\
\
Basically we the SDK has extensions which is how the SDK is updated, and by checking the extensions we can access to backwards compatibility to latest Android OS features available\
In the SDK and in the API\
\
https://www.youtube.com/watch?v=OBpjDSA-3Vk&t=926s\
\
\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\
\
@Composable\
\
This annotation more closely resembles a language keyword, it is not an annotation processor. Compose works with the aid of kotlin compiler plugin in the type checking and code generation\
phases of kotlin: there is no annotation processor needed in order to use compose.\
\
\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\
\
Configure your Build\
When updating Android Studio you usually update AGP even though you can still use an old version of the AGP, that isn\'92t ideal and it could cause errors, but this means the Android Studio version\
Could define the AGP version and the AGP version defines the Gradle version and AGP version defines the JDK version, although it should be no problem to use a higher version of the JDK for a\
determined AGP version but not with a lower JDK version since it can throw errors when starting Gradle, since the plugins use different JDK versions it sometimes can be hard to use the right JDK\
either way the idea is to use an equal or higher version of the JDK used on a given plugin\
\
	Build Glossary\
	\
		Build Types\
		They define certain properties that Gradle uses when building and packaging an app. They are typically configured for different stages of the development lifecycle. For example, debug\
		build type enables debug options and signs the app with the debug key, while the release type may shrink, obfuscate and sign the app with a release key for distribution\
\
		Product Flavors	\
		They represent different versions of an app that you can be released to users, such as free and paid versions, you can customize product flavors to use different code and resources while		sharing and reusing the parts that are common to all versions of the app. They are optional and have to be created manually, they contrast with build types which are mandatory, since at 		least one is needed to create a build. \
\
		Build Variants\
		Is the result of convincing build types with product flavors, they define the configuration that Gradle uses to build the app. \
\
		Manifest Entries\
		It is possible to specify values for some properties of the manifest file in the build variant configuration. These build values override the existing values in the manifest file. Defining properties		in the build variant configuration allows us to create variants of the app with different application names, minimum SDK versions, or target an SDK version. When multiple manifest are present		the manifest merger tool merges manifest settings\
\
		Dependencies\
		The build system manages project dependencies, they can be local or from remote repositories. This moves the responsibility of manually searching, downloading, and copy binary packages		of the dependencies into the project directory\
\
		Signing\
		The build system lets you specify signing settings in the build configurations/build scripts and it can sign applications during the build process. The debug and release build types/build configurations		are signed with different keys and certificates, for example the debug build type key and certificate signs the build using known certificates to avoid a password prompt at build time in contrast 		with release builds which require the developer to define a signing configuration so the build tool can sign it, for that you need to create a release key if you don\'92t have one, a signed build		is required to distribute apps in most apps stores\
\
		Code and Resource Shrinking\
		Build system lest us specify different ProGuard rules file for each build variant, the build system applies the appropriate set of rules to shrink the code and resources using tools such as R8 which		live inside the AGP\
\
		Multiple APK Support\
		Build system lets us build different APKs that each contain only the code and resources it needed for example resource/code needed for a specific screen density or Application Binary		Interface(ABI). The recommended approach is to release a single SASB as it offers splitting by language in addition to screen density, while it avoids the need of uploading multiple artifacts to		an app store.\
\
	\
	The following are the different build configuration files\
		\
		- The Gradle Wrapper file(gradle/wrapper/gradle-wrapper.properties)\
		The Gradle wrapper(gradlew) is a small application included with your source code that downloads and launches Gradle itself. The property \'93distributionUrl\'94 describes which version of Gradle is		used to run your build. If you have different projects with different Gradle versions, Gradle creates copies of the Gradle daemon for each Gradle version, in addition to separate copies of each		JDK  used to run Gradle. This increases memory and CPU usage, potentially slowing your builds or impacting other work on the machine.\
\
		- The Gradle settings file\
		The \'93settings.gradle.kts\'94 file (for the Kotlin DSL) or \'93settings.gradle\'94 (Groovy DSL) is in the root project directory. This settings file defines project-level repository settings and informs Gradle which		modules it should include when building your app. It can also conta\\in a \'93pluginManagement.repositories\'94 block which configures the repos Gradle uses to search or download the gradle plugins and		repos such as JCenter, Maven Central and Ivy. You can also use local repositories or define your own remote repos. They are the repos Gradle should use to look for its dependencies. It can also		contain \'93dependencyResolutionManagement.respositories\'94 block which configures the repos and dependencies used by all modules in your project, such as libraries that you are using to create 		your app. However, you should configure module-specific dependencies in each module-level build.gradle file. For new projects, Android Studio includes Google\'92s Maven and Maven Central by default.\
\
		- Top-level build file(project level)\
		The top-level \'93build.gradle.kts\'94 is located in the root project directory. It typically defines the common version of plugins used by modules in your project such as the \'93com.android.application\'94 plugin		which is also known as the AGP or \'93com.android.library\'94 and \'93org.jetbrains.kotlin.android\'94, you can define a version and use \'93apply false\'94 in the project level plugin block when defining a plugin 		and this will add the plugin as a build dependency but not apply it to the current(root) project, don\'92t use this in sub-projects, for more info search \'93Applying external plugins with same version to 		subprojects\'94 in gradle documentation. If using buildsrc or build logic you have to define \'93com.android.application\'94 in project config file you can define it with version or without a version but include 		\'93apply false\'94, and also in the application config file use it but without applying a version if you\'92re using buildSrc or build-logic then you usually define an application plugin and in here you define 		the app plugin and the use this custom plugin only in the app build config, at the same time you have to define in buildsrc or build logic config file the agp dependency 		\'93com.android.tools.build:gradle:version\'94 inside either a \'93compileOnly\'94 or \'93implementation\'94 this is in KTS.
\f2\fs26 \cf4 \cb5 \

\f0\fs24 \cf0 \cb1 \
		\
		- Module-level build file\
		The module-level \'93build.gradle.kts\'94 is located in each project module, individual module custom configuarionts/settings. In the app module build config we define build types and product flavors, here 		we can also override settings in the top-level(project) build script or in the \'93main/\'93 app manifest. Using the \'93defaultConfig\'94 block we can override some attributes defined in main/manifest, build types		are defined in the \'93buildTypes\'94 block using the function getByName(\'93release\'94) function, product flavors are defined in the \'93productFlavors\'94 block and using the create(\'93flavorName\'94) function inside it.\
		If you need to override the source and target  java compatibility version you can it in the \'93compileOptions\'94 block and \'93kotlinOptions\'94 block. Also all modules should define a \'a8compileSDK\'a8 version in		this script level\
\
		- Gradle Properties File\
		There is two properties files;\
			\
			- gradle.properties: this is where you can configure project-wide gradle settings such as the gradle daemon\'92s maximum heap size which depends on the Build Environment, you can search for			\'93Configuring the Build Environment\'94 in the gradle documentation to understand it better\
\
			- local.properties: Is reserved for properties specific to the AGP. Putting your own values in this file can cause problems, if you need to define your own local properties create a separate			 properties file and manually load it. This file Configures local environment properties for the build system, including:\
					\
				- ndk.dir: Path to NDK. This is deprecated. Any downloaded version of the NDK are installed in the \'93ndk\'94 directory within Android SDK directory\
				- sdk.dir: Path to Android SDK\
				- make.dir - path to CMake\
				- ndk.symlinkdir: From Android Studio 3.5, creates a symlink to the NDK that can be shorter than the installed NDK path\
				\
\
	Source Sets\
		Android Studio logically groups source code and resources for each module into source sets. When you create a new module, AS creates a \'93main/\'93 source set within the module. A module\'92s \'93main/\'93 		source set includes the code and resources used by all its build variants/versions.\
\
		Additional source set directories are optional, if you have declared build variants you need to create the source sets, if you need specific code or resources for a product flavor or buildtype, manually. 		This will help inform Gradle to use specific code and resources when building a specific variant. The following are possible source set you can create to specify code and resources to build a variant\
		\
			src/buildType/ - Source set that includes code and resources only for a specific build type\
		\
			src/productFlavor/ - Source set that includes code and resources only for a specific product flavor. You can configure your build to combine multiple product flavors and for this you can create 			a source set like the following for each combination: src/productFlavor1ProductFlavor2\
		\
			src/productFlavorBuildType/ - Source set that includes code and resources only for a specific build variant. When you build the \'93fullDebug\'94(name is just an example of a flavor with build type)			version of your app, the build system merges code, settings, and resources from the following resource sets: \'93src/fullDebug/\'93(build variant source set), \'93src/debug/\'93(build type source set), 			\'93src/full/\'93(product flavor source set) and \'93src/main/\'93(common source set)\
\
			if different source sets contain different versions of the same file, Gradle uses the following priority priority order when deciding which file to use. The source  set on the left override tiles and 			settings he ones on the right:\
		\
			build variant > build type > product flavor > main source set > library dependency\
\
		When merging multiple manifests, gradle uses the same priority order so each build variant can define different components or permissions in the final manifest.\
\
	Version Catalogs\
\pard\tx220\tx720\tx1440\tx2160\tx2880\tx3600\tx4320\tx5040\tx5760\tx6480\tx7200\tx7920\tx8640\li720\fi-720\pardirnatural\partightenfactor0
\ls1\ilvl0\cf0 {\listtext	\uc0\u8259 	}Use them to specify common versions when you have multiple modules or multiple independent projects with common dependencies, search in grade documentation \'93Sharing dependency versions 		between projects\'94\
\pard\tx720\tx1440\tx2160\tx2880\tx3600\tx4320\tx5040\tx5760\tx6480\tx7200\tx7920\tx8640\pardirnatural\partightenfactor0
\cf0 	\
	\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\
	\
	Java Versions in Android Builds\
		\
		Glossary\
			Java Development Kit - This contains tools such as a compiler, profiler, and archive creator which are used behind the scenes during your build to create your app. Libraries contacting APIs			 that you can call from your Kotlin or Java source code, note that not all functions are available on Android. The JVM, an interpreter that executes Java apps, this is used to run Android Studio 			IDE and the Gradle tool, the JVM is not used on Android devices or emulators.\
\
			JetBrains Runtime(JBR) - Is an enhanced JDK, distributed with Android Studio. It includes several optimizations for use in Studio and other JB products.\
\
\
		Change JDK to run AS\
			Even though is possible to change the JDK from the JBR, which is the default, to something else by changing the environment variable \'93STUDIO_JDK\'94 its not recommended\
\
		Choose which JDK runs the Gradle builds\
			There are different ways but if you run Gradle using the buttons in AS, the JDK used is set in the AS settings. If you run Gradle in a terminal, either inside or outside AS, the JAVA_HOME			 enviroment variable(if set) determines which JDK Gralde uses to build it scripts and if variable is not set, uses the \'93java\'94 command on your PATH environment variable. For consistent result			 make sure JAVA_HOME and JDK version set in settings uses same JDK since if you run gradle from any button in Android Studio the version it will use will be the one in the IDE gradle settings\
		\
			When running a build, Gradle creates a process called a daemon to perform the actual build. This process can be reused, as long as the build are using the same JDK and Gradle version and 			this reduces the time to start a new JVM and initialize the build system. Starting different daemons consumes more CPU and memory\
\
		Which Java APIs can I use in my Java or Kotlin source code?\
			An Android application can use some of the APIs defined in a JDK, but not all of them. The Android SDK defines implementations of many Java library functions as part of its available APIs. The			\'93compileSdk\'94 property specifies which Android SDK version to use when compiling your Kotlin or Java source code.\
\
			Basically the Android SDK is the same as the Android API and each version of Android can represent a version of the API/SDK and same way backwards, the API/SDK version represents a version of 			Android, for example: Android 14 represents API/SDK version 34. For each SDK/API(or Android version) version there is a compatible JDK version used to build the project, for example for			API 34/Android 14 you should use JDK 17. Desugaring is the process that will allows us to use a Java API that is available in the \'93compileSDK\'94 but is not available in the \'93minSDK\'94 			version, you might still be able to use the Java API you want to use through this feature called desugaring.\
\
		Which JDK compiles with my Java source code?\
			The Java toolchain JDK contains the Java compiler, used to build Java source code. This JDK also runs the Kotlin compiler(which runs on a JVM), javadoc(tool to generate java documentaiont), and			tests run during the build. The JDK used to compile Java code and to run Gradle should be the same as the toolchain by default uses the same JDK as used to run Gradle(if inside AS it will be			 the JDK defined in settings and if running \'93manually\'94 from any terminal the JDK will depend on the \'93JAVA_HOME\'94 environment variable)  \
\
			This all means even thought the JDK used to run Gradle and the Toolchain JDK used to compile Java code can be the same they serve different purposes. This setting should be defined in			in each module build script and it can be change depending on if your code is pure Java or a combination of Kotlin and Java, for the first scenario use the \'93toolchain\'94 block inside a \'93java\'94 block			and use \'93languageVersin.set(JavaLanguageVersion.of(17))\'94, for the second scenario use the \'93kotlin\'94 block and use the function \'93jvmToolchain(17)\'94\
\
		Which Java language source features can I use in my Java source code?\
			The \'93sourceCompatibility\'94 property determines which Java language features are available during compilation. It does not affect Kotlin source code. If not specified it defaults to the Java 			toolchain or JDK used to run Gradle. Is recommended to specify toolchain or \'93sourceCompatibility\'94. \
		\
		Which Java Binary/Bytecode features can be used when I compile my Kotlin or Java source?\
			Specifying \'93targetCompatibility\'94 and \'93jvmTarget\'94 determines the Java class-format version used when generating bytecode from Java and Kotlin source. Some Kotlin features existed before 			Java equivalent features were added. With later \'93jvmTarget\'94 levels, the Kotlin compiler directly use the Java feature instead of create Kotlin\'92s compiler own way to represent these features, 			and this will result in better performance. \'93targetCompatibility\'94 defaults to the same value as \'93sourceCompatibility\'94, but if specified, must be greater than or equal to \'93sourceCompatibility\'94. 			\'93jvmTarget\'94 defaults to the toolchain version. You can take advantage of additional Java features by increasing \'93targetCompatibility\'94 and \'93jvmTarget\'94(they should have same version) but this			might force you to also increase your minimum Android SDK version to ensure the feature is available.\
\
	\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\
	\
	Configure the app module\
	\
	The application ID is declared in this modules build script and this can be different for each build configuration/build variant. We also declare the namespace independent of the application ID\
\
		Set Application ID\
		This ID looks like a Java or Kotlin package name, such as \'93com.example.myapp\'94. This ID uniquely identifies the app on the device and in the Google Play Store. Once app is published, you should		not change this ID if you do the Play Store treats the apps as a new different app. In some APIs this can be referred to as the package name as it used to be directly tied to the package name in 		the past. If using a web view consider using your package name as a prefix in your app ID as you might encounter problems if you don\'92t do so.\
\
		The rules for naming this setting, even though it looks very similar to a Kotlin or Java package name, are a bit more restrictive:\
			- Has to have at least two segments(one or more dots)\
			-Each segment must start with a letter\
			-Can have alphanumeric characters or underscore\
\
		When setting this property is recommended to:\
			-Keep the ID the same as the namespace. The distinction between these two properties can be a bit confusing but if you keep it the same you don\'92t have to worry about any of that\
			-As mentioned don\'92t change ID after it has been published\
			-If an app ID is not defined it automatically sets it to the same as the namespace, so be careful not to change the namespace as this could mean changing the app ID as well\
\
		Change the application ID for testing\
			By default the build tools apply an application ID to your instrumentation test APK using the app ID for the given build variant appended with \'93.test\'94. You should not need to change this but if			you require to do so you can change it using the property \'93testApplicationId\'94\
\
		Set the Namespace\
			Every Android module has a \'93namespace\'94, which is used as the kotlin or Java package name for its generated \'93R\'94(resources) and \'93BuildConfig\'94 classes. This property is set to the same value as 			package name you choose when you create the project. In newer versions of AGP this property replaces the \'93packageName\'94 property in the manifest\
		\
		Change the Namespace\
			If you are in the need to change this property\'92s default value, even though not recommended to avoid dealing with complexities, it is possible, you have to make sure the appId  is explicitly 			defined, so that changing namespace likewise change the app ID. \
\
			If you have set different values for \'93namespace\'94 and \'93applicationId\'94, the build tools copy the app ID into your app\'92s final manifest file at the end of the build. If you inspect the \'93AndroidManifest.xml\'94			file after a build, the \'93package\'94 attribute is set to the app ID. The merged manifest\'92s \'93package\'94 attribute is where Google Play Store and Android platform actually look to identify your app.\
\
		Change namespace for Testing\
			The default namespace for the \'93androidTest\'94 and \'93test\'94 source sets is the main namespace, with \'93.test\'94 added at the end. If you need to change this for any reason you can set the 			\'93testNamespace\'94 property. You should not explicitly define the \'93nameSpace\'94 and the \'93testNamespace\'94 to the same value otherwise namespace collisions will occur.\
\
		Change The Test BuildType\
			You can change \'93testBuildType\'94 by passing the build type you want your instrumented test to run on. By default all test run against debug build type\
		\
	\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\
	(Special Topic not \'93directly\'94 related in configuring the build script but its necessary to know what an Android Library is, you can search \'93Create an Android Library\'94)\
	Android Library\
		Is structurally the same as an Android app module. It includes everything needed to build an app, including source code, resource files and an Android manifest. However instead of compiling into 		an APK(android package), it compiles into an Android Archive(AAR) file that you can use as a dependency for an Android app module. Unlike a JAR, AARf files offer the following functionality for		Android apps:\
			-AAR files can contain Android resources and manifest file, this lets you bundle in/include shared resources like layouts and drawables in addition to Kotlin or Java classes and methods\
			-Can contain C/C++ libraries for use by the app module\'92s C/C++ code\
\
	\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\
	\
	Add build dependencies\
		\
		Dependency types\
			Local library module dependency\
				Declared as follows:                  implementation(project(\'93:myModule\'94)\
			\
			Local Binary dependency\
				Gradle declares dependencies on JAR files inside your project\'92s \'93module_name/libs/\'93 directory. However you can declare individual files:\
					implemtation(fileTree(mapOf(\'93dir\'94 to \'93libs\'94, \'93include\'94 to listOf(\'93*jar\'94))))\
								or\
					implementation(files(\'93libs/foo.jar\'94, \'93libs/bar.jar\'94))   \'97\'97 declaring individual files\
\
			Remote Binary dependency\
				Declared as follows:			\
					implementation(\'93com.example.android:app-magic:12.3\'94) which is the shorthand for implemation(group = \'93com.example.android\'94, name = \'93app-magic\'94, version = \'9312.3\'94)\
				\
				These dependencies requires you to declare an appropriate remote repo, where Gradle will look for the library. \
\
		Native Dependencies\
			Depending on an AAR that exposes native libraries will automatically make them available to the build system used by \'93externalNativeBuild\'94.\
\
		Dependency configurations\
			The following list contains all the functions we can use to declare dependencies in the \'93dependencies\'94 block:\
			\
				- implementation : Gradle adds the dependency to the compile class path and packages the dependency to the build output. However this tells Gradle you don\'92t want this dependency				to leak to other modules at compile time. The means the dependency is available to other modules only at runtime. Using this configuration instead of \'93api\'94 can result in significant 				build time improvements because it reduces the number of modules that the build system needs to recompile\
\
				- api : Is basically the same as \'93implementation\'94 with the difference that Gradle knows that the module wants to transitively export the dependency to other modules. So that it is 				available to them at both runtime and compile time. If the dependency changes its external API, Gradle recompiles all modules that have access to that dependency at compile time.\
\
				- compileOnly : adds dependency to compile classpath time but not runtime, meaning it is not included in the build output, this doesn\'92t work with AAR dependencies\
\
				- runtimeOnly : adds dependency to runtime(build output) which means it is not added to the compile classpath\
\
				- annotationProcessor : Adds dependency to annotation processor classpath. This will separate the compile and annotation processor classpath which  will improve performance\
\
				- lintChecks : This will run lint checks you want Gradle to run when building the project. This checks are not packed in your Android library project\
\
				- lintPublish : it must be called from an Android library. It packs/compiles lint checks into a \'93Lint.jar\'94 file and publish it to your Android library\
\
\pard\tx720\tx1440\tx2160\tx2880\tx3600\tx4320\tx5040\tx5760\tx6480\tx7200\tx7920\tx8640\pardirnatural\partightenfactor0

\f3\b \cf0 				Adding Dependencies To An Specific Build Variant or Test
\f0\b0 \
				put the variant name in front/before the configuration which has to have its first letter capitalized example: flavornameImplementation, flavornameCompileOnly, flavornameAnnotationProcessor\
\
				It is also possible to add a dependency that applies only to an specific product flavor and a build type with the following syntax\
\
					val flavorNameBuildTypeApi by configuration.creating\
					val flavorNameBuildTypeRuntimeOnly by configuration.creating\
\
					dependencies \{\
						flavorNameBuildTypeApi(\'93some:articat:1\'94)\
						flavorNameBuildTypeRuntimeOnly(\'93some:articat:2\'94)\
					\}\
				\
				Adding a dependency that applies only to local test or instrumented test looks like the following respectively\
					\
					dependencies \{\
						testImplementation(\'93some:articat:1\'94)\
						androidInstrumentedTestImplementation(\'93some:articat:2\'94)\
					\}		\
			\
				It is possible to pass arguments to annotation processors by extending the interface \'93CommandLineArgumentProvider\'94\
				\
				If using \'93Kept\'94 you can avoid compiling \'93KAPT\'94 again when rebuilding project by setting this flag in \'93gradle.properties\'94  \'93kept.include.compile.classpath=true\'94 from either the kapt block or				keptExtension adding this line \'93includeCompileClasspath = false\'94 (https://kotlinlang.org/docs/kapt.html#compile-avoidance-for-kapt)\
\
				
\f3\b Exclude Transitive Dependencies
\f0\b0 \
				Transitive dependencies are the dependencies your dependencies depend on and you can exclude them with the following syntax\
					implementation(\'93some-dependencie-artifact\'94) \{\
						exclude(group = \'93com.example.imgTools\'94, module = \'93native\'94)\
					\}\
\
				You can exclude this type of dependencies in your test by using the \'93TestedExtension\'94 with the following syntax\
					android.testVariants.all \{\
						compileConfiguration.exclude(group = \'93com.example.one\'94, module = \'93one\'94)\
						runtimeConfiguration.exclude(group = \'93com.example.two\'94, module = \'93two\'94)\
					\}\
\
				You can declare repositories URL and you can declare different URL\'92s in the same repositories.\
				\
				You can find all the info about handling dependencies to local and remote binaries, libraries, local and remote repos in the gradle \'93dependency Management\'94. In here we can also find info 				on a Glossary that defines the following vocabulary (artifact, module, Component Metadata, etc)\
\
	\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\
	Configure Build Variants\
\
		Configure Build Types\
			AS automatically creates a debug and release build type, you usually add more configurations to release type like \'93isMinifyEnable = true\'94 or \'93isResourceShrinking = true\'94, 			you can use \'93getByName\'94 function to add/modify existing build type or \'93create\'94 function to create one and \'93initWith\'94 function to copy configurations from other buildtype\
		\
		Configure Product Flavors\
			You can use the same functions as in build types, \'93create\'94, \'93getByName\'94, \'93initWith\'94, inside this block. You have different options inside build types vs product flavors blocks and			there are quite a few different configurations you can set in each of those blocks but at least the \'93versionName\'94 and \'93versionCode\'94 can only be customized in this block\
			In order to be able to create a product flavor you have to define a flavor dimension which is basically a String value that you have to add to the \'93flavorDimensions\'94 property, 			if you only define one dimension inside a module\'92s build script all product flavors will be added to this dimension, you can define more than one but then you have to explicitly			define/declare which dimension a flavor belongs to when declaring/creating it in the buildscript. \
\
			Gradle applies the build type after the product flavor, if we add app id suffix in both build type and product flavor the product flavor suffix will be added first and then the build type			suffix.\
\
		Variant API	\
			You can use the Variant API and/or Artifact API to call some extensions that will let you change things like the \'93versionCode\'94 in each build variant by using the block			 \'93androidComponents\'94(only available to build scripts applying the application or library plugin) this block is available in Gradle Kotlin \'93.kts\'94 files but if you\'92re using Groovy			 you access it by calling \'93android.applicationVariants.all\{ \}\'94 in here you have access to the variant API\
		\
	\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\
	Optimize Your build\
		\
		You can optimize your build by limiting what string and screen-density resources you use in your build type/product flavor use \'93resourceConfiguration(\'93en\'94, \'93xxhdpi\'94)\'94\
		\
		Convert images to WebP, this can reduce your images size and therefore can speed up your builds since images don\'92t need to be compressed at build-time to reduce its size, its benefits		are more sensible if your app uses a lot of images, however there is a small increase in CPU usage while decompressing WebP images\
	\
		Gradle automatically disables \'93isCrunchPngs = false\'94 in debug builds this improves build times since images won\'92t be compressed, if you are building a release version of the app		you should explicitly set this to true.\
\
		Try using the JVM parallel garbage collector, by adding this to the \'93jvmargs\'94 in the properties files, remember every argument you add to this field must with \'93-\'93, just add the following to enable		this feature \'93-XX:+UseParallelGC\'94 Setting arguments to this property can lead to a \'93Daemon disappeared\'94 failure, in order to fix this you have to add \'93-XX:MaxMetaspaceSize=256m\'94 and 		\'93-XX:+HeapDumpOnOutOfMemoryError\'94\
\
		You can change the memory limit if builds are too slow add jvmargs \'93-Xmx6g\'94 if you change the default limit you also have to add \'93-XX:MaxMetaspaceSize=1g\'94\
\
		You can try speeding up rebuilds by caching configuration phase results with \'93org.gradle.configuration-cache=true\'94 and in case a plugin is not capable of using this feature print warnings\
		\'93org.gradle.configuration-cache.problems=warn\'94. Activating the configuration-cache flag will let the build retrieve cache values of files like buildscripts, gradle properties and environment\
		variables, which will speed up the build time, this type of caching will help Gradle speed up the configuration phase. There is another type of cache which can speed up the execution		phase and is done by retrieving the cache tasks outputs if the taks inputs has not changed\
\
		Any project using KAPT can leverage the optimization described in the following link https://kotlinlang.org/docs/kapt.html#compile-avoidance-for-kapt\
\
	\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\
	Profile Your Build(Generate Build Time Report)\
		You can profile your build, first run your app so all downloadable dependencies are cached, second perform a clean build to avoid skipping tasks which input have not change this way we will		be able to catch/profile the whole build, run the following command \'93./gradlew - -profile - -offline - -rerun-tasks assembleFlavorDebug\'94. Breaking it down \'93profile\'94 enables profiling. \'93offline\'94 disables		gradle from fetching online dependencies, as mentioned above you should have built app at least once to have your dependencies cached already. \'93rerun tasks\'94 forces Gradle to rerun all tasks		and ignore any task optimization. You can check the report in the project-root/build/reports/profile/ directory it is an \'93html\'94 file you can open in the browser\
\
	\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\
\
	Plugins\
	You have two ways of declaring a plugin, one with a version and the other is without a version. The first way is useful when your you have a multi-project build and you want to apply the plugin to some or	all subprojects in your build, but not the root project, you can do this by using \'93apply false\'94 and this will also enable us to use the second way in subprojects which is using the \'93plugins\'94 block without the 	version in subprojects build script.(info found in Gradle documentation \'93{\field{\*\fldinst{HYPERLINK "https://docs.gradle.org/current/userguide/plugins.html#sec:subprojects_plugins_dsl"}}{\fldrslt 
\f4\fs25\fsmilli12750 \cf6 \cb3 \expnd0\expndtw0\kerning0
Applying external plugins with same version to subprojects}}\'94)\
	\
		\'93org.jetbrains.kotlin.jvm\'94 or kotlin(\'93jvm\'94) - I found this plugin in a custom plugin called \'93JvmLibraryConventionPlugin\'94 and also in another called \'93KotlinLibraryPlugin\'94 both custom plugins implementation/setup was 		almost identical. The result of applying this plugin is a \'93pure\'94 Kotlin module, meaning without any Android SDk.\
		\
		\'93org.jetbrains.kotlin.android\'94 or \'93kotlin-android\'94 or kotlin(\'93android\'94) - they are basically the same since they both link to plugin \'93org.jetbrains.kotlin.gradle.plugin.KotlinAndroidPluginWrapper\'94, these plugins are used to		be able to build modules with Android SDK code written in kotlin, plugin provides processes and settings the builder tools needs to perform a build. I have seen either or plugin applied to custom		plugins such as a custom application plugin, an Android library custom plugin, custom feature plugins and a Test custom plugin. Usually any module or custom plugin applying this plugin will define		a \'93targetSdk\'94 and \'93minSdk\'94, we use the follwowing dependency to resolve plugin. This plugin is resolved with this dependency \'93org.jetbrains.kotlin:kotlin-gradle-plugin:$\{version\}\'94 or \'93kotlin(gradle-plugin), $\{version\}\'94		inside a implementation function inside the dependencies block. I\'92ve always seen this plugin applied whenever the \'93android.application\'94 or \'93android.library\'94 is applied to the project buildscript\
			\
		The following two plugins version are resolved with the dependency of AGP \'93com.android.tools.build:gradle:8.1.2\'94\
		\
		\'93com.android.application\'94 - this is pretty much the AGP and as mentioned above in the gradle configuration files info it can be used in different custom plugins, it even can be repeated in some 		custom plugins applied to the application module build script, and I have seen it applied to the project build script which would make this plugin applied to all build scripts, so this means its 		declaration is repeated, but in the project build script it is applied with the \'93apply false\'94 modifier. This plugin will make the code in this module into a AAR instead of a JAR, this will allow us to \
		call the library module as a dependency from another module in the project\
\
\pard\tx720\tx1440\tx2160\tx2880\tx3600\tx4320\tx5040\tx5760\tx6480\tx7200\tx7920\tx8640\tx20844\pardirnatural\partightenfactor0
\cf0 		\'93com.android.library\'94 - This plugin turns your module into a library so you can reuse it(this is the info I found about it but its real use in some of the context I saw it is still not clear), I saw it declared in		project build script without a version and with \'93apply false\'94, also in custom plugins for the presentation layer custom plugins either a custom plugin for the old view system or for compose, and in an		Android library custom plugin. You can create Kotlin and Java library modules however you can only add resources and manifest files to an Android module. In some projects basically all modules 		apply this plugin. This is also part of the AGP\
\pard\tx720\tx1440\tx2160\tx2880\tx3600\tx4320\tx5040\tx5760\tx6480\tx7200\tx7920\tx8640\pardirnatural\partightenfactor0
\cf0 \
			
\f3\b Extension
\f0\b0 \
			All Plugins has extension, this is how we can configure them and usually we access to those extension using a DSL however, when using an AGP plugin we access the plugin extensions via the \'93android\'94, \
			\'93java\'94 or \'93kotlin\'94 block and depending on any other block we might have other blocks but inside these functions blocks we can call the plugin extensions, for example the AGP has two extensions(at least			that I know) the first \'93ApplicationAndroidComponentsExtenstion\'94, this extension gives us the opportunity to customize the process of building build type and product flavors, the second \'93ApplicationExtension\'94			this one gives us access to functions like \'93defaultConfig\'94 etc. For the \'93com.android.library\'94 we have an extension of \'93LibraryExtension\'94 which allows to have access to functions such as 			\'93defaultConfig\'94/\'93targetSDK\'94, we can call this extension from our custom plugins to be able to configure them with the following syntax in the custom plugin \'93target.extension.configure<ThePluginExension>\'94,\
			there is a \'93BaseExtension\'94 that we can use to configure basically any plugin from a custom/local/convention plugin but it is not recommended to use it, so we are going to need to know the plugin 			extension if we need to configure/customize the build further\
\
			You can call extensions from a custom plugin with the following syntax\
				project.extensions.configure<ExtensionTypeClass> \{ // you have access to blocks like: defaultConfig \{ \} which belongs to application and library plugin etc \}\
\
				// or\
\
				val extensions = project.extensions.getByType<ExtensionTypeClass>()\
				\
				extensions.apply \{ // you have access to blocks like: defaultConfig \{ \} which belongs to application and library plugin etc \}\
		\
			The following are the most common Android extensions we might need to use, but each plugin most likely will let us access new/different extensions\
\
				CommonExtensions\
				LibraryExtension and ApplicationExtension are Childs of this interface, this gives us access to block such as \'93defaultConfig\'94, \'93compileOptions\'94, \'93buildTypes\'94, \'93productFlavors\'94 and 				configurations like \'93compileSdk\'94				\
\
				LibraryExtension\
				You have to apply the Android Library plugin to be able to consume these extensions, gives you access to configurations/blocks as the above extensions with the addition of at least				another configuration which will be available in the \'93defaultConfig\'94 block called \'93targetSdk\'94\
\
				ApplicationExtension\
				You have to apply the Application plugin to be able to consume these extensions, gives you access to configurations/blocks as the above extensions with the addition of at least				another configuration which will be available in the \'93defaultConfig\'94 block called \'93targetSdk\'94\
\
				ApplicationAndroidComponentsExtension (https://medium.com/androiddevelopers/new-apis-in-the-android-gradle-plugin-f5325742e614)\
				this extension gives you access to the Variant Api which lets you call functions like \'93onVariants\'94, \'93beforeVariants\'94, \'93onFinalizeDsl\'94, this API help us customize build further\
			\
	\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\
\
	Configurations Glossary\
		\
		minSdk - defines the minimum version of the Android platform on which the app will run, is identified by the platform API level identifier.\
\
		targetSdk - API level on which the app is designed to run. In some cases, this allows the app to use manifest elements or behaviors defined in the target API level\
		\
		versionCode - is a positive integer that the Android system uses to avoid an application to install an old version, meaning an app can only be upgraded but not downgraded. Make sure to always 		change this to a greater value as the Play Store won\'92t let you upload an APK you already used for previous version. This version is not displayed to the user. I have seen this and version name 		always defined together and have seen them declared inside a \'93Android.kt\'94 file in buildsrc or buildLogic module, this means it could be defined in different modules but have also found a case 		where the it is declared only once in the app level build source and no place else. (info found in \'93Publish your app/Version your app\'94)\
	\
		versionName - String used as a version number shown to the users. Can be a raw string or a reference to a string resource. This string should describe the app version as \
		\'93<major>.<minor>.<point/patchLevel>\'94 or any other absolute or relative version identifier.\
\
		compileSdk - specifies which Android SDK/API version to use when compiling your kotlin or Java source code(the SDK contains some java libraries implementations)\
\
		jvmTarget - determines the Java class-format version used when generating bytecode for compiled Java and Kotlin source. When using a later version the Kotlin compiler can use features that		were added in Java after they existed in Kotlin resulting in a performance gain. It defaults to toolchain version, and remember toolchain version defaults to JDK used to run Gradle if that version is		not compatible then you should be prepared and have defined a toolchain resolver. \
	\
		sourceCompatibility - This defines what java features your app supports at runtime. This should be lower or equal than the JDK used to run Gradle but not greater, \
\
		targetCompatibility - By default it has the same value as sourceCompatibility(if set). This defines what version of Java the output(the bytecode) will have, this means the java version the class files needs to run		on a JVM so the Java version that the program is executed on has to be equal or higher that this but not lower other wise it will throw an exception at runtime. This value defines the minimum Java version 		the consumer of the project will need to run it. This is just a restriction to whoever is building the app from using the wrong Java version to build the app and it can be different from source compatibility\
\
		toolchain - this feature will make sure we\'92re using the right JDK version and download it if necessary. Also when using this flag ti will automatically set source and target compatibility.  It also provides		with java and kotlin compiler, basically it provides compilers capabilities\
		\
		compileSdk - determines the Java API/SDK framework that will be used to compile Java and Kotlin source\
\
	\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\
	Tips\
		- You can define common configuration of modules in the Root project/module, however the root project would have to apply \'93kotlin-android\'94 plugin, and then you have different options you can do		it directly in the root project script or from a function in a \'93buildsrc\'94 that takes an instance of an object of type Project and then use the block\
			project.anroid \{ // android configurations \}\
\
		- {\field{\*\fldinst{HYPERLINK "https://developer.android.com/build/gradle-tips"}}{\fldrslt https://developer.android.com/build/gradle-tips}} read it for source set, gradle test options configurations and signing configs tips, add buildconfigfields to the buildconfig class and also add		resources directly from the buildscript. \
		\
		- You can configure gradle test options for local unit tests only, inside the \'93unitTests\'94 block inside a \'93testOptions\'94 block inside an \'93android\'94 block \
			\
	\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\
	TestKit\
	A Gradle tool that help us test the build logic, some people have wrote their test using Spock which is a testing framework\
\
	\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\
	Composite builds Vs Buildsrc(both are build logic)\
	One of the main disadvantages of \'93buildsrc\'94 is that any change in \'93buildsrc\'94 would invalidate the cached configuration of every module/project in the build, because this changes the classpath of the entire	build but this can be solved with composite builds, basically all you need to do is separate the build logic from the rest of the build via the \'93included build facility\'94 however there is a cost in using composite	builds and that is when an included build provides plugins used by the main build, Gradle needs to do which is unfortunately single-threaded. For every plugin request, Gradle needs to check the included 	builds for plugins that might be substituted in, however some people have opted to publish their plugins to their Artifactory instance so that they can be resolved as a Binary plugin/third party plugin, 	resolving a binary plugin is much faster than compiling(or pulling from the build cache) a plugin that lives in \'93buildsrc\'94/included build, on the other hand there is also a cost in using buildsrc and that is	any change in it will invalidate cache in this approach any build script changes only invalidates some tasks and not the that script cache.\
	\
	Normal dependency management is used when creating convention plugins(local plugins) which usually apply chore and community 
\f3\b plugins without a version
\f0\b0 , creating convention plugins is something	that is usually done in either or, composite builds or buildsrc, no matter your implementation for handling build logic there are different ways to be able to declare those plugins without a version, \
	we are going to use the \'93org.jetbrains.kotlin.android\'94/\'93kotlin-android\'94 plugin just as an example, so inside a convention plugin, living either in the module of buildSrc or an included module in a composite	build module(usually called build-logic), we apply the mentioned plugin without a version and if we try apply this convention plugin in a script and build the entire project without making any configuration	the build will fail, so our first option is making some configurations in the \'93buildsrc\'94 or included module in the composite build root build script, first this script needs to apply at least the chore plugin of	\'91kotlin-dsl\'92 which will give us access to blocks like \'93dependencies\'94, it looks like the purpose of this plugin is to let us add configurations/dependencies to the build\'92s classpath in a more declarative way	but the idea is adding a dependency that will help us resolve the plugin version so we can define it either with a  \'93implemention(org.jetbrains.kotlin:kotlin-gradle-plugin:1.8.20\'94 or a 	\'93implementation(kotlin(\'93gradle-plugin\'94, \'931.8.20\'94),)\'94 inside a \'93dependency block\'94 if the \'93kotlin-dsl\'94 plugin is declared, other wise we can discard the \'93kotlin-dsl\'94 plugin and open a \'93buildscript\'94 block with a 	\'93dependencies\'94 block inside and a \'93classpath\'94 function inside and that substitutes the \'93implementation\'94 keyword in the previous approach but with the same values it had inside it. The second option is if 	we are not using buiildSrc or composite build then we can just go to the root project build script and basically either do the same as in the previous approach or instead declare the plugin with the version we 	want inside the plugins block with an \'93apply false\'94 and then declare the plugin without a version in the plugins block of any module/project needing it, this will cause Gradle to get the version from 	the root project build script declaration, this is usually done when build logic is not abstracted to a different module. There is one difference with \'93buildSrc\'94 and composite build, that is when declaring the used	plugins in the root module build script if we are using \'93buildSrc\'94 with the dependencies or classpath of the artifacts that will help us resolve the version we don\'92t to declare its version anywhere, however	if using composite builds we would declare those plugins in dependencies or in the classpath, for example the dependency \'93com.android.tools.build:gralde:8.1.2\'94 can resolve the version of	 \'93com.android.application\'94, \'93com.android.library\'94 and \'93com.androi.test\'94 plugins however if using composite build and declaring them in the root module build script we have to declare them with a version\
	but this is not required in any other place we declare the plugins, meaning we should/could/would have two declarations of the plugins in the version catalog, one with a version to use it in this build script	and one without a version to use it any other place, and the version is the same for the dependency and for the plugins always.
\f2\fs26 \cf4 \cb5 \

\f0\fs24 \cf0 \cb1 )\
\
	\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\
	Random data\
	- According to some info I found, there is/was a concept called \'93project isolation\'94 which aimed to isolate each project since at some point in time build caching was applied to the build as a hole, meaning if 	any script changed anything the entire cache result is discarded and the entire sync is executed again.\
\
	If you need to configure multiple APK so they are distributed by the same app listing you can look for two documents \
		1.- \'93Multiple APK support\'94/\'93How multiple APKs work\'94 \
		2.- \'93Build multiple APKs\'94/ \'93Configure your build for multiple APKs\'94\
\
	\
	\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\
	Sharing Dependency versions between projects\
	We have two options to manage this, first version catalog, second using a platform\
		\
		Version Catalog\
		you can declare [libraries], [plugins] and [versions], in the versions you have the option to declare them as a \'93required version\'94 which is just a string and the other option is to declare them as 		{\field{\*\fldinst{HYPERLINK "https://docs.gradle.org/current/userguide/rich_versions.html#rich-version-constraints"}}{\fldrslt 
\f1 \cf7 \cb3 \expnd0\expndtw0\kerning0
\ul \ulc7 rich versions}} in which we can declare different parameters like \'93strictly\'94, \'93prefer\'92, etc\
\
		Platform\
		refer to: 
\f5 \cf8 \expnd0\expndtw0\kerning0
 {\field{\*\fldinst{HYPERLINK "https://docs.gradle.org/current/userguide/platforms.html#sub:using-platform-to-control-transitive-deps"}}{\fldrslt 
\f4 \cf6 \cb3 Using a platform to control transitive versions}}
\f4\fs36 \cf6 \cb3 \
\pard\pardeftab720\partightenfactor0

\f1\fs32 \cf6 \cb1 \
\pard\tx720\tx1440\tx2160\tx2880\tx3600\tx4320\tx5040\tx5760\tx6480\tx7200\tx7920\tx8640\pardirnatural\partightenfactor0

\f0\fs24 \cf0 \kerning1\expnd0\expndtw0 	\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\
\pard\pardeftab720\partightenfactor0
\cf0 \
\pard\tx720\tx1440\tx2160\tx2880\tx3600\tx4320\tx5040\tx5760\tx6480\tx7200\tx7920\tx8640\pardirnatural\partightenfactor0
\cf0 \'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\
About App Manifests\
This file describes essential information about your app to the Android build tools, the Android operating system and Google play. It is required to declare. For more info about manifest references, which \
are the tags used in the manifest, see look for the \'93About app manifests/App manifest overview\'94 documentation\
\
-Components of the app(activities, services, broadcast receivers and content providers)\
-The permissions that the app needs to access protected info or functionality(hardware)\
-The hardware and software features the app requires, which determines which devices can install the app from google play.\
\
	\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\
\
	
\f3\b Intent Filters(find this info in the \'93About App Manifests\'94)
\f0\b0 \
	App activit\'e9s, services, and broadcast receivers are activated by intents. An intent is a message defined by an \'93Intent\'94 object that describes an action to perform, including data to be acted on, the category\
	of component(activity, service, broadcast reciever) that is expected to perform the action, and other instructions\
\
	When an app issues an intent to the system, the system locates an app component that can handle the intent based on intent filter declarations in each app\'92s manifest file. The system launches an instance\
	of the matching component and passes the Intent object to it. If more than one app can handle the intent, then the user can select which app to use.\
\
	An app component can have any number of intent filters(defined with the <intent-filter> element). If you want to allow other apps start an activity in your application see \'93Let other apps start your activity\'94 	documentation\
\
	\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\
	Icons and Labels\
	Any app component can define an \'93icon\'94 and \'93label\'94 attribute for displaying a small icon and text label. The values for these attributes that are set in a parent element become the default value for all child	elements. For example the values declared in <application> element are the default values for each app\'92s component, such as all activities. You can declare specific values inside an <intent-filter> element\
	this will be used to display to users whenever that component is presented as an option to fulfill an intent.\
\
	\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\
	Permissions\
	An app must request permission to access sensitive user data, such as contacts and SMS, or certain system features, such as camera and internet access. They are declared inside an \'93<uses-permission>\'94\
	element and it has to declare a \'93name\'94 property, each permission has its own name, SMS permission, for example, is \'93android.permission.SEND_SMS\'94\
	\
	You can protect your apps components with permissions, it can use the permissions defined by Android in android.Manifest.permission, or a permission declared in another app or your app can also define	its own permissions. A new permission is declared with <permission> element. For more info check \'93Permissions on Android\'94\
\
	\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\
	Device Compatibility\
	You define what types of hardware or software features your app requires so Google Play Store can determine which users can install your app. You use elements like <uses-feature> inside here you can 	define with the attirbute \'93required\'94 you can define \'93true\'94 or \'93false\'94, <uses-sdk> with attribute \'93minSdkVersion\'94 but most likely you will define this in your Gradle build script. \
\
	\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\
	Merge Multiple Manifests FIles(\'93From optimize your build\'94 documentation)\
	In this document they explain the priority order when merging manifest files that are available in source sets\
	\
\
\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\
Proguard Rules\
Is a file that includes rules that modify R8 compiler behavior, the R8 compiler is in charge to shrink code, shrink resources, obfuscate code and optimize code. R8 compiler converts your project\'92s java bytecode\
into the DEX format that run on the Android platform. You can generate a report of all the rules that R8 applies when building your module by including the following code in your modules \'93proguard-rules.pro\'94 file\
\
	// You can specify any path and filename\
	\'93-printconfiguration ~/tmp/full-r8-config.txt\'94\
\
Report of removed code\
	\'93-printusage ~/tmp/usage.txt\'94\
\
Report of entry points\
	\'93-printseeds ~/tmp/seeds.txt\'94\
\
For apps with minSdk lower or equal to 21 you should enable multi dex, look for \'93enable multidex\'94 documentation\
\
\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\
Check the commit the tag points and compare it with the \'93main\'94 branch HEAD(in attach mode it is the current checked-out branch\'92s latest commit) to get the correct tag name\
\
	Check tags with the commit they point to\
	git show-ref - -tags\
	\
	Check main branch head latest commit it points to\
	git checkout main\
	1\
\
With these information we can create objects, do transformations and determine what is the latest tag which we can use to set the application \'93versionName\'94 from the repository\
\
\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\
\
\
Version Catalogs\
\
\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\
\
Kotlin Flows\
They are located in the Kotlin Coroutine library and represent a stream of values computed asynchronously. Both types of flows, cold and hot, emits/generate the stream values \
in the context of a coroutine, meaning they run processes to emit/generate values asynchronously.\
\
	Cold Flows\
	At first only cold flows existed, meaning flows are cold by nature. Cold flows are stateless streams which are created on demand, they are created every time an observer starts 	collecting its values, Each observer gets it\'92s own sequences of values, they are not shared.\
\
	Hot Flows\
	They can share the same stream values to all the subscribers, meaning they are stateful streams.\
		SharedFlow\
		Broadcast same values to all observers. They can manage an optional replay cache and/or a buffer\
		\
		StateFlow\
		Specialized and optimized subclass of SharedFlow which stores and replays last value only. You basically are enforced to catch exceptions early since any uncaught 		exception in a hot flow ends the stream with no possibility to restart it, even when using the \'93catch()\'94 operator\
		\
		The implementation, MutableStateFlow, needs to have an initial value. You can emulate a MutableStateFlow with now initial value with a MutableSharedFlow declared		like: \'93MutableSharedFlow(replay = 1)\'94, but this would be less efficient thatn \
\
		It filters out repetitions of the same value, it does it by using \'93Any.equals()\'94 to do comparisons, MutableSharedFlow does the same\
\
		Each time a coroutine collects a hot flow, the flow provides the latest value which means if we have code that will run whenever the lifecycle state is \'93STARTED\'94, since		we will go though that state on every configuration change, if we register an observer in this lifecycle state this observer will be provided the same last value several times		which may hit performance since it will duplicate work.\
\
		A flow is not lifecycle aware, because of this the responsability of syncing with the lifecycle aware component is moved up to the coroutine collecting the flow\
\
	Collecting a Flow inside a Component With a Lifecycle\
	The components with a lifecycle could be a a fragment, an activity\
		\
		Collecting Cold Flows\
		You can efficiently collect cold flows which are not backed by a channel nor buffer inside a component with a lifecycle with the following code\
			\
			viewLifecycleOwner.lifecycleScope.launchWhenStarted \{\
				viewmodel.result.collect \{ data ->\
					displayResutl(data)\
				\}\
			\}\
\
		This will suspend when the flow when lifecycle state is \'93STOPPED\'94 as the coroutine collecting it will suspend. \
\
		The problem with hot flows is that the flow will dispatch stream values to all observers, including suspended observers(observers running on suspended coroutines)\
\
		Channel-based or Callback-based flows only stop when the collection is cancelled(not sure what that means but sounds like is when the coroutine is cancelled)\
\
		Note: Flows are usually destroyed/cancelled if the job that reference to the coroutine is cancelled but you can also cancel the flow collection with operators like firts(() that under \
		the hood are calling other functions like \'93collectWhile\'94\
\
		Collecting Flows Efficiently\
		We should aim to\
			1. Cache: Cache Data that has been loaded, and not loaded a second time if the first value is still valid, like when just rotating screen(config change)\
			2. Avoid Background Work: When activity or fragment becomes goes to \'93STOPPED\'94 state ongoing work should be paused or cancelled in order to save resources\
			3. No Work Interruption During Configuration Changes: This is an exception to goal #2 since during config changes an Activity/Fragment gets replaced by a new 			instance of it while preserving its state, so canceling on going work when the old instance is destroyed to immediately restart it when the new instance is created would			be counter-productive\
\
		So the solution with hot flows is using either or the following APIs(run either or functions inside a \'93onCreate\'94 in an activity or \'93onViewCreated\'94 in a fragment)\
			viewLifecycleOwner.lifecycleScope.launch \{\
				viewLifecycleOwner.repeatOnLifecycle(LifecycleState.STARTED) \{\
					viewModel.result.collect \{ result ->\
						displayData(result)\
					\}\
				\}\
\
				or\
			\
				viewModel.result.flowWithLifecycle(viewLifecycleOwner.lifecycle, LifecycleState.STARTED).collect \{ result ->\
					displayData(result)\
				\}\
			\}\
		\
\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\
\
Material 3 Components\
Components are interactive building blocks for creating user interface. They can be organized into categories based on their purpose: Action, conatainment, communication, navigation,\
selection and text input\
\
	Actions\
	Common Buttons, Extended FAB(FABs with texts), Floating actions buttons(just the icon) (for primary actions), Icon Buttons(for minor actions), Segmented Button(like buttons group)\
\
	Communication\
	Badges(They show notification, counts, or status info on nav items and icons like how many unread emails there is or how many notifications there are), progress indicators(show status\
	of a process in real time), snackerbar(updates about app processes at the bottom of the screen), tooltips(display brief labels or messages)\
\
	Containment\
	They include other components. Here we have Bottom Sheets, cards, carousel, dialogs, divider(Thin lines that group content in lists or other containers), list, side sheets(components \
	anchored to the side of the screen)\
 \
	Navigation\
	Bottom app bar, Navigation Bar, Navigation Drawer, navigation rail, search, tabs and top app bar\
\
	Selection\
	Checkbox, Chips, date pickers, menus, radio button, sliders, switch(es) and time pickers\
	\
	Text Inputs\
	Text fields\
\
\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\
\
Jetpack Compose Architecture\
\
	Compose UI - Most low level part, compose deals with layout, drawing, input. Compose UI that defines basic blocks for UI construction\
	Compose Foundation - Built on top of compose UI, it provides basic layouts like Column, box, lazy column etc\
	Compose Animation - Built on top of foundation\
	Material and Material 3 - Design systems that provides common widgets \
\
		Compose Compiler - It is needed since the whole concept of composable functions is actually an extension of kotlin language that needs compiler support.\
		Compose Runtime - Manages all the system  \
 \
Android uses \'93Skia Graphics\'94 engine for rendering things, it\'92s written in c++ call\
\
\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\
\
Phases in Compose vs Phases in View System\
\
	View System\
	Measure, Layout and drawing\
\
	Compose\
	Composition, it creates a tree of composables. Layout, it measures and defines where they are going to be placed(measure, placement). Drawing\
		\
\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\
\
Kotlin Multiplatform\
Kotlin/Native compiler and runtime(Runtime has a GC ) is used for rendering compose for IOS, while Kotlin/JVM compiler and runtime is used for rendering compose for Android\
\
\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\
\
Graphics Modifiers\
	\
	Drawing Modifiers\
	All drawing commands are done with drawing modifiers.\
	\
		Modifier.drawWithContent - Make sure to call \'93drawContent()\'94 somewhere inside to render actual content of composable,\
		basically you can choose drawing order with this modifier. This the drawing modifiers base modifier\
	\
		Modifier.drawBehind - Just draw behind a composable, just that simple. Actually this modifier is wrapped around drawWithContent\
\
		Modifier.drawWithCache - It will cache your draw objects. You either call \'93onDrawBehind\'94 or \'93onDrawWithConent\'94 inside of it\
		\
\
	Graphics Modifiers\
		\
		Modifier.graphicsLayer - Makes the content of a composable to draw into a draw layer. You can apply transformations\
		to composables. Transformations in this modifier can be applied without having to re-excute the drawing lambda, all these\
		transformations only affect the draw phase it does not affect the composition nor layout phases\
\
\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\
\
Process\
\
	All applications run in it own process. Android system starts a new Linux process for the application with single thread of execution when an application component(activity, \
	broadcast receiver, content provider, service) starts and no other components of the app are in a running state. By default, all components of the same app, run in the same	process and main thread. However is possible to start a new/different process for each app component we require, it is possible by declaring a \'93android:process\'94:processName\'94\'94\
	property in the manifest when declaring the tag of the component you want to run in a different process. You can communicate between different process using	interprocess communication(IPC)\
\
\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\
\
Task(basically what we call backstack when talking about navigation in fragments)\
\
	A task can be defined as a stack of activities. By default there will be only one task for an application unless defined the other way by different launch modes. To make an	activity launch in a different task define the \'91android:launchMode=\'93singleInstance\'94\'92 inside the activity tag in the manifest. If you create many tasks to run at the same time, some of 	them might be sent to the background and in time they might be destroyed by the system causing state to be lost.\
\
	Activity launch modes\
	\
		1.- Standard: It creates a new instance of an activity in the task(stack) from which it was started. Multiple instances of the activity can be created and multiple instances can\
		be added to the same or different task(s)\
		2- SingleTop: The same as standard except if there is a previous instance of the activity that exists in the top of the stack then it will not create a new instance, but only if it is at \
		the top of the stack/task, if it is not at the top it will then create a new instance to avoid this you can use the below mode\
		3.- SingleTask: If no instance of activity exists it will be created but if it does exist no matter where in the stack, the same existing instance will be used and if there is\
		other activities on top of the requested activity the ones on the top will be destroyed and the one requested will be active, this happens similar to a callback\
		4.- SingleInstance: Same as single task but system does not launch any activities in the same task.\
\
\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\
\
ActivityTaskManager and FragmentManager(Pretty much they are equivalent, activity manager deals with activity backstack while fragment manager deals with fragment backstack)\
	\
	ActivityTaskManager\
	Class that interacts with activities, their containers(tasks which is the activities stack) and can give information about them\
\
	FragmentManager\
	This class handles the application fragment stack, that means we can manage the fragment stack with this class, we can add, remove and replace the fragments in/to the stack\
	If using the Navigation Library most likely you will not need to use this class as that library works with this manager directly.\
\
\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\
\
Optimizing RecyclerView\
\
https://amitshekhar.me/blog/recyclerview-optimization?source=post_page-----40e38b2531b--------------------------------\
\
\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\
\
APK(Android Package) vs. AAB(Android App Bundle)\
\
They both are ways to pack an Android application for distribution. APK is the \'93traditional\'94 format while AAB is a more modern and efficient format introduced by Google. APK is more \
\'93Compatible\'94 since it can be distributed across different platforms/App stores while the purpose of AAB is to be optimized by Google Play Store these optimizations make your app \
smaller. Using AABs along with Google Play App Signing allows you to use \'93feature modules\'94/\'93dynamic feature modules\'94/\'93Modules on Demand\'94\
\
	 Dynamic Delivery and Feature Modules/Dynamic Feature Modules/Modules on Demand\
		Dynamic delivery means if you\'92re uploading a AAB enables Play Store to build/generate/install an optimized APKs with only the code and resources that the user\'92s \
		specific device configurations needs to run the app, meaning the APK/app size is smaller.\
\
		Dynamic feature modules/modules on demand are a feature that allow you to specify modules that contain features and resources your app doesn\'92t require at install\
		time and the user can download on demand at a later time. I don\'92t know the details to implement this feature yet. Dynamic feature modules can only exist inside an AAB.\
		If you need to know more about this feature check the \'93On Demand Modules\'94 Android codelab\
\
\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\
\
(Related to AOSP)\
\
\pard\tx720\tx1440\tx2160\tx2880\tx3600\tx4320\tx5040\tx5760\tx6480\tx7200\tx7920\tx8640\pardirnatural\partightenfactor0

\f3\b \cf0 SE LInux
\f0\b0  (Security Enhanced Linux)[https://www.youtube.com/watch?v=uI9nk1VDCpY]\
\
This is Linux Kernel module that provides a mechanism for supporting access control security policies. Rules express admin policies, there is two types of policies/rules a.- Mandatory\
Access control(MAC) b.- Discretionary Access Control(DAC), all accesses have to go through these policies/rules to get access controls. The former type of policy should be the same on\
all Android devices and is called system policy, this policies are private and mandatory meaning they can not be modified, can not be replaced nor disabled, however there is one \
way to ignore all those policies and thing that would \\violate those policies and that is when working on a userdebug device and running the shel in a permissive domain by using \'93adb root\'94\
be aware when this mode is used all fails of SE Linux calls/denials are suppressed and also SE comp is disable, SE comp filters which system calls an app can make, in this cases SE comp\
will be in charge to log all these failures/denials. The later can be provided by the vendor and are called vendor policy\
\
This mechanism labels all processes(domains), files, sockets, apps, properties, services, objects. These labels are automatically assigned but can be overridden. Labels have the \
following structure: <use>]:<role>:<type>:<categories> but in Android most of the time you only use the \'93type\'94 field to write a policy.\
\
Everything is forbidden unless explicitly allowed. The following is how you\'92d write an allow statement in the policy: allow <source Type> <target type>: <target class> <permission>\
This means you allow a domain of \'93X\'94 source type to access an object of \'93Y\'94 target class labeled with \'93Z\'94 target type to use the specified permission(access vector)\
\
Rules verbs can be \'93allow\'94, \'93dontaudit\'94(deny permission and don\'92t audit/log it) and \'93neverallow\'94. All access denials are register as an AVC denial to the Audit log an event log. You can remove\
rate limiting with \'93auditctl -r 0\'94 so you can see all denials.\
\
	Uses\
\
	All processes should only have the access it needs.\
\
	This mechanisms makes user and app Isolation possible, each different app is a different different user to the OS and a user shouldn\'92t/won\'92t have access to other user\'92s \
	info. \
\
	Categories defined in the labels help accomplish this security as the User Id and the App Id is encrypted in the category of a label and the label of the source type must\
	have all the categories of the target type in its declaration or won\'92t have access\
\
	System and Vendor \
\
	Project Treble\
	Aim to allow updating the system(Android framework) without have to update the vendor code. System code and vendor code must only communicate via stable APIs and for that we\
	use HAL wich contains all the interfaces that communicate to drivers and that we can use to communicate with the hardware, the system can\'92t talk to drivers directly. SE linux enforces\
	use of HALs interfaces, limits access to these interfaces to only the processes that need it, limit access to drivers to interfaces inside HAL, and blocks other channels between the vendor\
	and core/drivers\
\
	Policies\
	Keep in mind that updating system usually means updating system policy as well. Vendor policies is allowed to reference some rules in the system policy and system policy is \
	split in 3 directories:\
	\
		Public: Everything here can be accessed but vendor policy. Hard to change\
		Private: Nothing here can be accessed by vendor policy. Careful changes are OK.\
		Vendor: This is only intended for use by vendor policy(purpose is not very clear but it looks like it is policies intended to be accessed by vendor only)\
\
\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\
Talk form embedded open source summit [https://www.youtube.com/watch?v=hQZz2PRNdxI&t=1367s]\
\

\f3\b The AOSP Build System
\f0\b0 (Info based on Android 13 and will probably all change in Android 14 as part of migration to Bazel)\
\
Is similar to others(OpenEmbedded, Buildroot), it only build the AOSP OS meaning it doesn\'92t build a kernel nor a bootloader and this means is developer\'92s or original equipment \
Manufacturer\'92s responsibility to bundle together the AOSP build system and their own build system on top of that and which is going to build the kernel and the bootloader,  if trying to\
deliver an alternative Android version using AOSP, which is said to be result in some truly weird stuff and is not entirely ideal but is how it is done. AOSP is a huge project, it \
contains at least >50 MLOC which are C++(mostly), Java(big chunk) and a bit of Rust and Kotlin\
\

\f3\b 	How to build a AOSP target product
\f0\b0 \
		\
		1.- Getting AOSP\
		AOPS is a collection of git repositories(> 1100). To run AOSP you first need to get a manifest listing the git tress to clone, optionally specifying a version tag with -b using the\
		following command: \'93repo init -u https://android.googlesource.com/platform/manifest -b <version tag>\'94. Then clone git trees, you will get them all in one go(150GB) as \
		opposite of downloading on demand, as in OpenEmbedded in which you have to download one by one, using the following command \'93repo sync\'94, which essentially is a \'93git clone\'94 \
		you will get download all the repos but this means you could get stuff you don\'92t need and that is why all the project is so large(150GB,s)\
\
		2.- Select and build a target product\
			- Set up the shell environment with the following command \'93source build/envsetup.sh\'94, this will include a bunch of shell functions\
			- Select the target using lunch(a shell function defined in envsetup.sh) \'93lunch aosp_cf_x86_84_phone-userdebug\'94\
			- Each target is defined by an AndroidProduct.mk file, example: \'93aosp_cf_x86_84_phone-userdebug\'94 which comes from location: \'93device/google/cuttlefish/AndroidProduct.mk\'94\
			  and it would contain a field with the following info: \'93COMMON_LUNCH_CHOICES := aosp_cf_x86_84_phone-userdebug\'94\
\pard\tx720\tx1440\tx2160\tx2880\tx3600\tx4320\tx5040\tx5760\tx6480\tx7200\tx7920\tx8640\tx16661\pardirnatural\partightenfactor0
\cf0 			- Start the build with the following command: \'93m\'94 (just a letter \'93m\'94), with powerful hardware it will take about one hour, normal hardware 4-6 hours\
\
		3.- Outputs\
		The android packages/modules that get build are all bound together into this \'93.mk\'94(make) file variable called \'93PRODUCT_PACKAGES\'94 which lists all modules it builds. You can get\
		all product packages that exists in your product with the following command \'93get_build_var PRODUCT_PACKAGES\'94(not easy to read since it is basically on long line with all that info)\
		all files are stored in the \'93out/target/product/<device name>\'94 directory and here you will find a \'93system.img\'94 system image file, you use a fastboot to flash that image into a device\
\pard\tx720\tx1440\tx2160\tx2880\tx3600\tx4320\tx5040\tx5760\tx6480\tx7200\tx7920\tx8640\pardirnatural\partightenfactor0
\cf0 \
\pard\tx720\tx1440\tx2160\tx2880\tx3600\tx4320\tx5040\tx5760\tx6480\tx7200\tx7920\tx8640\pardirnatural\partightenfactor0

\f3\b \cf0 	How Android modules are organized?
\f0\b0 \
		\
		
\f3\b Recipes
\f0\b0 \
		Android modules are defined in recipes in one of two formats\
			a.- Android.bp\
				Written in blueprint which is a language specific to AOSP as a way of defining a module. This is equivalent to BB files in Yocto. Yocto is a Linux Foundation collaborative\
				open source project whose goal is to produce tools and processes that enable the creation of Linux distributions for embedded and internet of things(IoT) software that\
				are independent of the architecture of the embedded hardware, BB is the extension of the the recipe files in Yocto project\
			b.- Android.mk\
				Legacy format to store recipes, this type of files are deprecated but still hanging around\
\
		When you do the build it will iterate over all \'93bp\'94/\'93mk\'94 files it will build whatever it is you specified in the \'93PRODUCT_PACKAGES\'94 \
\
	So now that we now how do you pull AOSP and how you build it we can see the details of the build tools which this section is all about\
\

\f3\b 	The Build Tools/Components
\f0\b0 \
		\
		There are three main tools:\
			\
			* 
\f3\b Soong
\f0\b0 : Parses Android.bp files and generates ninja manifests(and some makefile fragments and then passes it to kati), this tool was intended to replace \
			   Kati and Makefiles but it has not fully replaced them and its has progressed slowly that is why the makefiles where mentioned. The blueprint language is JSON-like, and\
			   also similar to Basel BUILD files, it is declarative(no build logic) and that means all you get inside these files only contains a bunch of name value assignments. The build \
			   logic is implemented in Song modules written in go. The generated code/manifests will be stored in the <AOSP directory URL in your machine>/buid/soong and the\
			   soong documentation is stored in <AOSP directory URL in your machine>/build/soong/README.md\
			* 
\f3\b Kati
\f0\b0 : Parses Android.mk and all the other makefile fragments and generates more ninja manifests\
			* 
\f3\b Ninja
\f0\b0 : Parses the ninja manifests, generates the dependency tree for the target to built and schedules jobs\
			\
		New tool:\
		\
			* Bazel: Is intended to solve a problem with the software architecture by adding another layer \
\

\f3\b 	Build System\
		Soong Modules
\f0\b0 \
		Check the following video on the title for an example of a \'93.bp\'94 file it will explain the structure. BP files are going to be passed to the cross compiler which is going to build it, it\
		will bring some implicit dependencies such as libraries and other explicit defined in the \'93required\'94 block inside the BP file, all dependencies will be installed into the staging area \
		before the module is built. There is different type of modules a recipe can contain like the following list\
		\

\itap1\trowd \taflags1 \trgaph108\trleft-108 \trbrdrt\brdrnil \trbrdrl\brdrnil \trbrdrr\brdrnil 
\clvertalc \clshdrawnil \clwWidth2880\clftsWidth3 \clheight20 \clbrdrt\brdrs\brdrw20\brdrcf9 \clbrdrl\brdrs\brdrw20\brdrcf9 \clbrdrb\brdrs\brdrw20\brdrcf9 \clbrdrr\brdrs\brdrw20\brdrcf9 \clpadl100 \clpadr100 \gaph\cellx4320
\clvertalc \clshdrawnil \clwWidth2920\clftsWidth3 \clheight20 \clbrdrt\brdrs\brdrw20\brdrcf9 \clbrdrl\brdrs\brdrw20\brdrcf9 \clbrdrb\brdrs\brdrw20\brdrcf9 \clbrdrr\brdrs\brdrw20\brdrcf9 \clpadl100 \clpadr100 \gaph\cellx8640
\pard\intbl\itap1\tx720\tx1440\tx2160\tx2880\tx3600\tx4320\tx5040\tx5760\tx6480\tx7200\tx7920\tx8640\pardirnatural\qc\partightenfactor0
\cf0 cc_binary\cell 
\pard\intbl\itap1\tx720\tx1440\tx2160\tx2880\tx3600\tx4320\tx5040\tx5760\tx6480\tx7200\tx7920\tx8640\pardirnatural\qc\partightenfactor0
\cf0 Native binary\cell \row

\itap1\trowd \taflags1 \trgaph108\trleft-108 \trbrdrl\brdrnil \trbrdrr\brdrnil 
\clvertalc \clshdrawnil \clwWidth2880\clftsWidth3 \clbrdrt\brdrs\brdrw20\brdrcf9 \clbrdrl\brdrs\brdrw20\brdrcf9 \clbrdrb\brdrs\brdrw20\brdrcf9 \clbrdrr\brdrs\brdrw20\brdrcf9 \clpadl100 \clpadr100 \gaph\cellx4320
\clvertalc \clshdrawnil \clwWidth2920\clftsWidth3 \clbrdrt\brdrs\brdrw20\brdrcf9 \clbrdrl\brdrs\brdrw20\brdrcf9 \clbrdrb\brdrs\brdrw20\brdrcf9 \clbrdrr\brdrs\brdrw20\brdrcf9 \clpadl100 \clpadr100 \gaph\cellx8640
\pard\intbl\itap1\tx720\tx1440\tx2160\tx2880\tx3600\tx4320\tx5040\tx5760\tx6480\tx7200\tx7920\tx8640\pardirnatural\qc\partightenfactor0
\cf0 cc_library_shared\cell 
\pard\intbl\itap1\tx720\tx1440\tx2160\tx2880\tx3600\tx4320\tx5040\tx5760\tx6480\tx7200\tx7920\tx8640\pardirnatural\qc\partightenfactor0
\cf0 Shared library\cell \row

\itap1\trowd \taflags1 \trgaph108\trleft-108 \trbrdrl\brdrnil \trbrdrr\brdrnil 
\clvertalc \clshdrawnil \clwWidth2880\clftsWidth3 \clbrdrt\brdrs\brdrw20\brdrcf9 \clbrdrl\brdrs\brdrw20\brdrcf9 \clbrdrb\brdrs\brdrw20\brdrcf9 \clbrdrr\brdrs\brdrw20\brdrcf9 \clpadl100 \clpadr100 \gaph\cellx4320
\clvertalc \clshdrawnil \clwWidth2920\clftsWidth3 \clbrdrt\brdrs\brdrw20\brdrcf9 \clbrdrl\brdrs\brdrw20\brdrcf9 \clbrdrb\brdrs\brdrw20\brdrcf9 \clbrdrr\brdrs\brdrw20\brdrcf9 \clpadl100 \clpadr100 \gaph\cellx8640
\pard\intbl\itap1\tx720\tx1440\tx2160\tx2880\tx3600\tx4320\tx5040\tx5760\tx6480\tx7200\tx7920\tx8640\pardirnatural\qc\partightenfactor0
\cf0 cc_library_static\cell 
\pard\intbl\itap1\tx720\tx1440\tx2160\tx2880\tx3600\tx4320\tx5040\tx5760\tx6480\tx7200\tx7920\tx8640\pardirnatural\qc\partightenfactor0
\cf0 Static library\cell \row

\itap1\trowd \taflags1 \trgaph108\trleft-108 \trbrdrl\brdrnil \trbrdrr\brdrnil 
\clvertalc \clshdrawnil \clwWidth2880\clftsWidth3 \clbrdrt\brdrs\brdrw20\brdrcf9 \clbrdrl\brdrs\brdrw20\brdrcf9 \clbrdrb\brdrs\brdrw20\brdrcf9 \clbrdrr\brdrs\brdrw20\brdrcf9 \clpadl100 \clpadr100 \gaph\cellx4320
\clvertalc \clshdrawnil \clwWidth2920\clftsWidth3 \clbrdrt\brdrs\brdrw20\brdrcf9 \clbrdrl\brdrs\brdrw20\brdrcf9 \clbrdrb\brdrs\brdrw20\brdrcf9 \clbrdrr\brdrs\brdrw20\brdrcf9 \clpadl100 \clpadr100 \gaph\cellx8640
\pard\intbl\itap1\tx720\tx1440\tx2160\tx2880\tx3600\tx4320\tx5040\tx5760\tx6480\tx7200\tx7920\tx8640\pardirnatural\qc\partightenfactor0
\cf0 cc_binary_host\cell 
\pard\intbl\itap1\tx720\tx1440\tx2160\tx2880\tx3600\tx4320\tx5040\tx5760\tx6480\tx7200\tx7920\tx8640\pardirnatural\qc\partightenfactor0
\cf0 Host binary\cell \row

\itap1\trowd \taflags1 \trgaph108\trleft-108 \trbrdrl\brdrnil \trbrdrr\brdrnil 
\clvertalc \clshdrawnil \clwWidth2880\clftsWidth3 \clbrdrt\brdrs\brdrw20\brdrcf9 \clbrdrl\brdrs\brdrw20\brdrcf9 \clbrdrb\brdrs\brdrw20\brdrcf9 \clbrdrr\brdrs\brdrw20\brdrcf9 \clpadl100 \clpadr100 \gaph\cellx4320
\clvertalc \clshdrawnil \clwWidth2920\clftsWidth3 \clbrdrt\brdrs\brdrw20\brdrcf9 \clbrdrl\brdrs\brdrw20\brdrcf9 \clbrdrb\brdrs\brdrw20\brdrcf9 \clbrdrr\brdrs\brdrw20\brdrcf9 \clpadl100 \clpadr100 \gaph\cellx8640
\pard\intbl\itap1\tx720\tx1440\tx2160\tx2880\tx3600\tx4320\tx5040\tx5760\tx6480\tx7200\tx7920\tx8640\pardirnatural\qc\partightenfactor0
\cf0 cc_library_host_shared\cell 
\pard\intbl\itap1\tx720\tx1440\tx2160\tx2880\tx3600\tx4320\tx5040\tx5760\tx6480\tx7200\tx7920\tx8640\pardirnatural\qc\partightenfactor0
\cf0 Host shared library\cell \row

\itap1\trowd \taflags1 \trgaph108\trleft-108 \trbrdrl\brdrnil \trbrdrr\brdrnil 
\clvertalc \clshdrawnil \clwWidth2880\clftsWidth3 \clbrdrt\brdrs\brdrw20\brdrcf9 \clbrdrl\brdrs\brdrw20\brdrcf9 \clbrdrb\brdrs\brdrw20\brdrcf9 \clbrdrr\brdrs\brdrw20\brdrcf9 \clpadl100 \clpadr100 \gaph\cellx4320
\clvertalc \clshdrawnil \clwWidth2920\clftsWidth3 \clbrdrt\brdrs\brdrw20\brdrcf9 \clbrdrl\brdrs\brdrw20\brdrcf9 \clbrdrb\brdrs\brdrw20\brdrcf9 \clbrdrr\brdrs\brdrw20\brdrcf9 \clpadl100 \clpadr100 \gaph\cellx8640
\pard\intbl\itap1\tx720\tx1440\tx2160\tx2880\tx3600\tx4320\tx5040\tx5760\tx6480\tx7200\tx7920\tx8640\pardirnatural\qc\partightenfactor0
\cf0 cc_library_host_static\cell 
\pard\intbl\itap1\tx720\tx1440\tx2160\tx2880\tx3600\tx4320\tx5040\tx5760\tx6480\tx7200\tx7920\tx8640\pardirnatural\qc\partightenfactor0
\cf0 Host static library\cell \row

\itap1\trowd \taflags1 \trgaph108\trleft-108 \trbrdrl\brdrnil \trbrdrr\brdrnil 
\clvertalc \clshdrawnil \clwWidth2880\clftsWidth3 \clbrdrt\brdrs\brdrw20\brdrcf9 \clbrdrl\brdrs\brdrw20\brdrcf9 \clbrdrb\brdrs\brdrw20\brdrcf9 \clbrdrr\brdrs\brdrw20\brdrcf9 \clpadl100 \clpadr100 \gaph\cellx4320
\clvertalc \clshdrawnil \clwWidth2920\clftsWidth3 \clbrdrt\brdrs\brdrw20\brdrcf9 \clbrdrl\brdrs\brdrw20\brdrcf9 \clbrdrb\brdrs\brdrw20\brdrcf9 \clbrdrr\brdrs\brdrw20\brdrcf9 \clpadl100 \clpadr100 \gaph\cellx8640
\pard\intbl\itap1\tx720\tx1440\tx2160\tx2880\tx3600\tx4320\tx5040\tx5760\tx6480\tx7200\tx7920\tx8640\pardirnatural\qc\partightenfactor0
\cf0 java_library(since android 10)\cell 
\pard\intbl\itap1\tx720\tx1440\tx2160\tx2880\tx3600\tx4320\tx5040\tx5760\tx6480\tx7200\tx7920\tx8640\pardirnatural\qc\partightenfactor0
\cf0 Java Library\cell \row

\itap1\trowd \taflags1 \trgaph108\trleft-108 \trbrdrl\brdrnil \trbrdrr\brdrnil 
\clvertalc \clshdrawnil \clwWidth2880\clftsWidth3 \clbrdrt\brdrs\brdrw20\brdrcf9 \clbrdrl\brdrs\brdrw20\brdrcf9 \clbrdrb\brdrs\brdrw20\brdrcf9 \clbrdrr\brdrs\brdrw20\brdrcf9 \clpadl100 \clpadr100 \gaph\cellx4320
\clvertalc \clshdrawnil \clwWidth2920\clftsWidth3 \clbrdrt\brdrs\brdrw20\brdrcf9 \clbrdrl\brdrs\brdrw20\brdrcf9 \clbrdrb\brdrs\brdrw20\brdrcf9 \clbrdrr\brdrs\brdrw20\brdrcf9 \clpadl100 \clpadr100 \gaph\cellx8640
\pard\intbl\itap1\tx720\tx1440\tx2160\tx2880\tx3600\tx4320\tx5040\tx5760\tx6480\tx7200\tx7920\tx8640\pardirnatural\qc\partightenfactor0
\cf0 android_app(since 10)\cell 
\pard\intbl\itap1\tx720\tx1440\tx2160\tx2880\tx3600\tx4320\tx5040\tx5760\tx6480\tx7200\tx7920\tx8640\pardirnatural\qc\partightenfactor0
\cf0 Android app\cell \row

\itap1\trowd \taflags1 \trgaph108\trleft-108 \trbrdrl\brdrnil \trbrdrr\brdrnil 
\clvertalc \clshdrawnil \clwWidth2880\clftsWidth3 \clbrdrt\brdrs\brdrw20\brdrcf9 \clbrdrl\brdrs\brdrw20\brdrcf9 \clbrdrb\brdrs\brdrw20\brdrcf9 \clbrdrr\brdrs\brdrw20\brdrcf9 \clpadl100 \clpadr100 \gaph\cellx4320
\clvertalc \clshdrawnil \clwWidth2920\clftsWidth3 \clbrdrt\brdrs\brdrw20\brdrcf9 \clbrdrl\brdrs\brdrw20\brdrcf9 \clbrdrb\brdrs\brdrw20\brdrcf9 \clbrdrr\brdrs\brdrw20\brdrcf9 \clpadl100 \clpadr100 \gaph\cellx8640
\pard\intbl\itap1\tx720\tx1440\tx2160\tx2880\tx3600\tx4320\tx5040\tx5760\tx6480\tx7200\tx7920\tx8640\pardirnatural\qc\partightenfactor0
\cf0 prebuilt_etc(since 10)\cell 
\pard\intbl\itap1\tx720\tx1440\tx2160\tx2880\tx3600\tx4320\tx5040\tx5760\tx6480\tx7200\tx7920\tx8640\pardirnatural\qc\partightenfactor0
\cf0 Prebuilt installed into etc\cell \row

\itap1\trowd \taflags1 \trgaph108\trleft-108 \trbrdrl\brdrnil \trbrdrt\brdrnil \trbrdrr\brdrnil 
\clvertalc \clshdrawnil \clwWidth2880\clftsWidth3 \clbrdrt\brdrs\brdrw20\brdrcf9 \clbrdrl\brdrs\brdrw20\brdrcf9 \clbrdrb\brdrs\brdrw20\brdrcf9 \clbrdrr\brdrs\brdrw20\brdrcf9 \clpadl100 \clpadr100 \gaph\cellx4320
\clvertalc \clshdrawnil \clwWidth2920\clftsWidth3 \clbrdrt\brdrs\brdrw20\brdrcf9 \clbrdrl\brdrs\brdrw20\brdrcf9 \clbrdrb\brdrs\brdrw20\brdrcf9 \clbrdrr\brdrs\brdrw20\brdrcf9 \clpadl100 \clpadr100 \gaph\cellx8640
\pard\intbl\itap1\tx720\tx1440\tx2160\tx2880\tx3600\tx4320\tx5040\tx5760\tx6480\tx7200\tx7920\tx8640\pardirnatural\qc\partightenfactor0
\cf0 cc_prebuilt_binary\cell 
\pard\intbl\itap1\tx720\tx1440\tx2160\tx2880\tx3600\tx4320\tx5040\tx5760\tx6480\tx7200\tx7920\tx8640\pardirnatural\qc\partightenfactor0
\cf0 Prebuilt installed into bin\cell \lastrow\row
\pard\tx720\tx1440\tx2160\tx2880\tx3600\tx4320\tx5040\tx5760\tx6480\tx7200\tx7920\tx8640\pardirnatural\partightenfactor0
\cf0 	\
		You can compile the documentation with \'93m soong_docs\'94 it will be generated and stored in \'93out/soong/docs/soong_build.html\'94 in here you will see all info about modules and\
		attributes, remember build logic of soong modules is written in Go. In android 13 there is 300 types of modules approx. \
\
\pard\tx720\tx1440\tx2160\tx2880\tx3600\tx4320\tx5040\tx5760\tx6480\tx7200\tx7920\tx8640\pardirnatural\partightenfactor0

\f3\b \cf0 		Soon outputs
\f0\b0 \
		The manifests which can be called build rules will be stored in \'93out/soong/build.ninja\'94 directory. If you change a single recipe/Android.bp file the build.ninja file will have to be\
		regenerated again. Soon does not know what the target is so it parses all Android.bp files, even if your target does not depend on that module/recipe, it also writes install\
		rules to \'93out/soong/Android-[product name].mk\'94 in Android.mk format which is processed by kati later, also writes dependencies to \'93out/soong/late-[product name].mk\'94\
		\

\f3\b 		Kati Modules
\f0\b0 \
		An Android.mk file cannot have a dependency on a module defined in an Android.bp, however it is possible the other way around.\
\

\f3\b 		Ninja Outputs
\f0\b0 \
		Ninja generates a ninja manifest named \'93out/build-[device name].ninja\'94 which contains the build rules to generate the Android modules listed in the \'93.mk\'94 files\
		example: \'93out/build-aosp_cf_x86_64_phone.ninja\'94, it also generates a manifest with dependencies or packaging in \'93out/build-aosp_cf_x86_64_pohne-package.ninja\'94\
\

\f3\b 		NINJA
\f0\b0 \
		It basically stitches all these stuff together, it read manifests generated by Soon and Kati, calculates dependencies for given target and schedules jobs needed to reach the \
		target. Ninja 1.9.0 is bundled in AOSP 13 in \'93prebuilts/build-tools/linux-x86/bin/ninja\'94. Basically is its own a build system, and build rules/build logic is not intended to be written\
		by humans\
\
		Bazel\
		It\'92s intended to replace all other tools, Soong, Kati and Ninja and should start in Android 14. Bazel works using the following components:\
	\
			*WORKSPACE: Defines the top level of a project. For AOSP we have <AOSP directory URL>/WORKSPACE -> build/bazel/bazel.WORKSPACE. Contains global configuration\
			*BUILD: Each module is defined in a BUILD file(similar to Android.bp or Android.mk), similar to recipes\
			*Bazel Rules(.bzl): Build logic lives here\
			*Starlark: BUILD and .bzl files are written in a which is a Phyton-like called Starlark.(Properly known as the \'93Build Language\'94)\
\
		Notes: In Android 13 the official way of building the Kernel is with \'93build.sh\'94 script but you an also do that with bazel(investigate more). The \'93build.sh\'94 script will disappear in \
		Android 14 and Bazel will be the only way of building the Kernel.\
\
\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\
\

\f3\b Coroutines\
\
	Scope\
\pard\tx720\tx1440\tx2160\tx2880\tx3600\tx4320\tx5040\tx5760\tx6480\tx7200\tx7920\tx8640\pardirnatural\partightenfactor0

\f0\b0 \cf0 	You can only create coroutines inside a scope and that is know as structured concurrency\
\
		
\f3\b Context\
		
\f0\b0 The scope context defines \
	\
	
\f3\b Coroutine Job(Mostly known as Job) and Supervisor Job\
	
\f0\b0 , coroutines can create other coroutines. A scope defines the context where the child coroutines are going \
	to be created, however you can assign each coroutine its own context.\
		\
		Context\
\
		
\f3\b Job
\f0\b0 \
		Represents a cancellable piece of work being performed by a coroutine, every coroutine builder(Launch and Async) will return these type of object. You can use a Job to\
		cancel a coroutine, await its completion(join) or even combine it with another Jobs.\
\
		
\f3\b Supervisor Job
\f0\b0 \
		This is a special kind of Job that is designed to supervise child coroutines \
\
\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\
\
\pard\pardeftab720\partightenfactor0
\cf0 Jetpack Glance\
\
	Is a framework built on top of the Jetpack Compose runtime that lets you develop and design app widgets using Kotlin APIs. App widgets miniature application views the can be embedded in other applications and receive periodic updates\
\pard\tx720\tx1440\tx2160\tx2880\tx3600\tx4320\tx5040\tx5760\tx6480\tx7200\tx7920\tx8640\pardirnatural\partightenfactor0
\cf0 \
\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\
\
Compose Good Practices\
\
	1. Make two versions of a composable. First version is a stateful version and second is a stateless version. First version basically is a wrapper of the second, the first wraps the second and it provides the state to it. Basically/usucally you\'92d use the stateful version in production code receiving business logic state or just hoisting state locally to render it correctly and the second version, stateless version, would be used to create a preview\
\
\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\
\
Graphics\
All of the following are GPU renderers\
\
	Skia\
	Graphics engine, is an open source 2D graphics library written in C++. Flutter used to use this as its GPU renderer but it moved away to use its own solution. It used to be Android\'92s only solution for rendering graphics but it is not clear to me whether it is still using it or not, it looks like they actually combining the usage of OpenGl and skip\
\
		OpenGl(Skia)\
		Skia has a OpenGL implementation of its GPU backend, they can be built alongside the Vulkan(Skia) implementation of its GPU backend\
\
		Vulkan(Skia)\
		Skia has a Vulcan implementation of its GPU backend, they can be built alongside the OpenGl(Skia) implementation of its GPU backend\
\
	OpenGl(android default)\
	Cross-language, cross-platform API for rendering 2D and 3D vector graphics. This API is typically used to interact with a graphics processing unit, to achieve hardware-accelerated rendering(this feature made google switch from SKIA to OPENGL as skin is not hardware-accelerated)\
\
\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\
\
Android ROM\
\
Stands for Read Only Memory but it refers to the system that an Android phone has installed from factory setup. This can be \'93replaced\'94 by a custom implementation of Android OS(Android is based on Linux), remember Android is open source so you can download the software and modify it as you need, it also can be created from scratch according to some information\
\
\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\
\
AppCompatActivity vs ComponentActivity\
\
You can check the details later but basically ComponentActivity is all you need to extend from your MainActivity when using compose in your app and if you\'92re using fragments with views(xml) you would rather extend AppCompatActivity as it extends from FragmentActivity and ComponentActivity\
\
\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\
\
Serializable vs Parcelable\
\
\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\
\
Modifier.Then\
\
\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\
\
Software Architecture\
\
An app\'92s/software\'92s architecture provides a set other guidelines to help you allocate the app responsibilities between the classes/modules. A well designed app helps you scale your app and extend it with additional features.\
\
\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\
\
4 OOP basic concepts\
\
	Inheritance\
	Is the technique/mechanism of basing a class or object upon another object or class, retaining a similar implementation. this enables us to create a hierarchy between these classes.\
\
	Polymorphism \
	Is the capability of a class/object/symbol to represent different types at different times.\
\
	Abstraction\
	Is the technique of hiding complex implementation details and showing only the necessary functionality\
	\
	Encapsulation\
	Is the concept of containing data creation and the methods to operate on the data(access, modification inside a single unit/class to meet determined requirements\
	\
\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\
\
Compose Unidirectional Data Flow\
\
Lets us decouple composables that display state in the UI from the application components/parts that store and change state\
\
\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\
\
Automated Test\
\
Is a structured method of checking your software to make to make sure that it works as expected, automated testing is code that checks to ensure that another pice of code that you wrote works correctly.\
\
Testing provides a way to continuously check the existing code as changes are introduced. It can help to the team\'92s productivity since it doesn\'92t require a person to run the test because they are run by a computer or device which can execute them much faster\
\
	Local Testing\
	They test small pieces of code to ensure that it functions properly. You can test functions, classes, and properties, all of those are also called Unit Test. They are executed in your workstation, which means they run in a development environment without the need for a device or emulator(fancy way of saying they run on your computer)\
\
	Instrumented test\
	In android an instrumentation test is a UI tests. Lets you test parts of your app that depend on Android API, and its platform and services. Unlike local testing, they lunch and app or part of an app, simulate user interactions, and check whether the app reacted appropriately. They run on a physical device or emulator.\
\
	In android these tests are actually built into its own Android Application Package(APK) like a regular Android App. The test APK is installed on the device or emulator along with the regular app APK and the former run its tests against the former\
\
\
\
	TEST STRATEGIES\
	Creating test scenarios around these categories can serve as guidelines for your test plan \
\
	Success Path: Focus on testing functionality for a positive flow. Create a list of scenarios for success paths should be easy since they focus on intended behavior for your app\
\
	Error Path: Focuses on testing functionality for a negative flow. It is quite challenging to determine all the possible error flows because there are lots of possible outcomes when intended behavior is not achieved\
	\
	Boundary case: Focuses on testing boundary conditions in the app.\
\
\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\
\
Convert from DP to Pixel\
\
Type \'93Android DP\'94 and find \'93support different pixel densities\'94 in that document you will find a reference to documentation function \'93TypedValue.applyDimension()\'94 Doucmentaiton will explain how\
\
	Pixel to DP\
	in the same documentation you will find a method called \'93deriveDimension(int, float, android.util.DisplayMetrics)\'94 to help us with this\
\
\
\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\
\
App Architecture\
\
	-Data Layer\
	In this layer contains most of the business logic. If we wanted to create an offline-first app we would start in the data layer\
		\
		Offline-First App\
		Read and Write are the two main operations we perform on app data. At minimum an online-first app should be able to perform reads without network access\
		\
		There should be a local data source, this one is the canonical source of truth, and a network data source, this one is the actual state of the application. \
		\
		The following would be the structure of the data layer	\
			\
			data/\
			    local/\
			        entities/\
			        dao/\
			        AppDatabase(class)\
			    network/\
			        AppNetwork(class)\
			        models/(DTOs)\
			    model/(exposed to other layers, they should live in the domain layer if it exists)\
			    repository/(you should expose the interface only, if a domain layer exists the interface should live there and the implementation lives in the data layer)\
		\
			Reads\
			The recommended way to read data in an offline-first app is using observable types, both strategies below would use work manager.\
				Read Strategies\
				Basically the only read strategy here is: error handling\
				\
					Error Handling\
					It depends on the data source. \
				\
					Local data source errors should be rare so you can just protect callers(those are other layers consuming the repository implementation) for example if you\'92re getting the info using a flow you can use the \'93catch\'94 function. \
\
					Network data source errors is more \'93complex\'94 and you have basically two options 1. Exponential Backoff or 2. Network Connectivity Monitoring, both uses WorkManager, the former tries to fetch data in intervals and increasing time on every attempt until it succeeds and you need to define a criteria to evaluate if the app should keep backing off like 1. The kind of error, meaning only retrying when error indicate lack of connectivity but not unauthorized HTTP calls because proper credential are not available 2. Maximum allowable retries. The later, Network Connectivity Monitoring, all request are queued until the system is sure the app can connect to the network data source and they are dequeued when the connection is established  \
\
			Writes\
			The recommended way to write data in offline-first app is using asynchronous APIs such as suspend functions. This avoids block the UI thread\
	\
				Write Strategies\
					Online-only writes\
					If successful you should update local data source but if it fails we throw an exception and let caller respond appropriately\
					\
					Queued writes\
					Insert into a queue writes requests then drain the queue with exponential backoff when app gets back online this is accomplished by creating persistent work usually delegated to WorkManager\
\
					Lazy writes\
					The local data store is updated first and then the write request are queued. This can create conflict between local data source and network data source\
\
			Synchronization and Conflict resolution\
			When an offline-first app restores connectivity it needs to reconcile the data in its local data source with that in the network data source. This process is called synchronization. There two main ways to do this, 1. Pull-based synch and 2. Push-based synch but there is some other\
\
				Pull-based Synch\
				The app reaches out the network data source to read the latest application data on demand. It is usually navigation-based, meaning it will only fetch the data it needs right before it\'92s presented to the user when it navigates to a screen. A downside of this approach is that if prone to heavy data use, this is because repeated visits to a navigation destination triggers unnecessary refetching of unchanged info. This can be mitigated through proper caching, in the UI layer with \'93cachedIn\'94(paging library) operator on in the network layer(data layer) with an HTTP cache. In case there is no network connectivity, the repository may request data from the local data source alone.\
\
				Push-based Synch\
				The local data source tries to mimic a replica set of the network data source to the best of its ability. It proactively fetches an appropriate amount of data on first-start to set a baseline, after which it relies on notifications from the server to alert it when that data is stale(no longer fresh) and then the app reacts to the notifications by fetching the data. With this approach we can have both read and writes when offline because it is assumed that the app has the latest info from the network data source locally. Check advantages and disadvantages in the documentation.\
\
				Hybrid Synch\
				Uses both\
\
			Conflict Resolution\
			If an app writes data locally when offline(lazy writes) that is misaligned with the network data source, a conflict has occurred that you must resolve before synch can take place.\
			\
			Conflict resolution often requires versioning. The app will need to do some bookkeeping to keep track of when changes occurred. This enables it to pass the metadata to the network data source. The network data source then has the responsibility of providing the absolute source of truth. There are a wide range of strategies to consider for conflict resolution depending on the app needs. A common approach in mobile apps is \'93last write wins\'94\
\
				Last write wins\
				Devices attach timestamp metadata to the data they write to the network. When the network data source receives them, It discards any data older than its current state while accepting those newer than its current state\
	\
			Work Manager in offline-first apps\
			in both read and writes strategies covered above, there were two common utilities:\
\
				Queues\
					Reads: Used to defer/postpone reads until network connectivity is available\
					Writes: Used to defer/postpone writes until network connectivity is available and to requeue writes for retries\
				\
				Network connectivity monitors\
					Reads: Used as a signal to drain the read queue when the app is connected and for synch\
					Writes: Used as a signal to drain the write queue when the app is connected and for synch\
\
			Both cases are examples of the persisten work that WorkManager excels at. Basically WorkManager first queues work request and then it drains the queue with exponential backoff. Basically this is possible thanks to the \'93doWork(): Result\'94 method in CoroutineWorker which automatically retries with exponential backoff if the result of the current execution is \'93Result.retry()\'a0\'94\
				\
	\
	-UI Layer\
		From this layer a very interesting note is about pagination\
	\
			Paging/Pagination 
\f5 \expnd0\expndtw0\kerning0
(https://developer.android.com/topic/architecture/ui-layer?authuser=1#paging)
\f0 \kerning1\expnd0\expndtw0 \
\
			Paging is consumed in the UI with type called PagingData. PagingData is a mutable object so it should not be represented/included in an immutable UI state. Instead, you should expose it from the ViewModel independently in its own stream\
\
		Logic\
			Business Logic: Is the implementation of product requirements for app data.\
			UI Logic: Is refers to how to display the UI state on the screen\
\
		UI State\
			UI State or state is basically app data or the property that describes the UI\
\
			There is two types of app data/state/UI state, Screen UI state and UI element state, the former is produced by the application of business logic to local state changes events/inputs that provides access to UIlogic that derives in Screen UI state changes and/or external inputs/events such as the application itself of business logic(repositories) to UIlogic triggered by those local inputs(sources of state change) that access UI logic that has access to business logic such as a click that refetches a screen content(inputs produce state changes and can be local(also called events, they can be user events like entering text to a filed, or clicking a checkbox, this inputs derive in UI element state changes when applying UI logic or local inputs can also be user events that provide access to UI logic that derives in Screen UI state changes, those type of UI state changes are the result of applying business logic to these type of event/inputs) or inputs can be external(external inputs are basically sources/inputs/events of state change that are processed by the domain or data layer) inputs can also be a mixture of local and external inputs/events) and the later is produced by application of UI logic to local state changes inputs\
\
		State Holder\
			They are types that apply business logic and UI logic to sources of state change and process user events to produce UI state  \
\
		UI State Production Pipeline\
\
			-Inputs: the sources of state change. They may be:\
				*Local to UI layer:  These could be user events like entering a text to a field or APIs provides access to UILogic that derives in UI state changes. Example: Button that refresh/fetch screen content\
				*External to UI layer: These are sources of UI state change coming from the domain or data layer. Example: A list of object coming from the repository in the data layer\
				*A mixture of all the above\
\
			-State Holders: as defined above\
			-Output: UI state the app can render to provide users the info they need\
	\
		State Production APIs\
			Inputs dictate what kind of processing is applied to the pipeline that is why the choice of asynchronous API for input has greater influence on the nature of the state production pipeline than the choice of observable API for output.\
				-Inputs: Use asynchronous APIs to perform work off the UI thread to keep the UI jank free however they can be synchronous as well however they both would be one shot operations or can be a Stream API. Coroutines or Flows in Kotlin and RxJava or callbacks in Java. One-Shot APIs can be MutableStateFlow, compose \'93mutableStateOf\'94, both APIs offer methods that allow safe atomic updates to the values they host whether or not the updates are synchronous or asynchronous\
				-Output: Use observable data holder APIs to invalidate and render the UI when state changes. Like StateFlow, Compose State, or LiveData\
\
		State Production Pipeline Assembly\
			-Lifecycle aware: in case the UI is not visible/not in focus or  not active, the pipeline should not consume any resource unless explicitly required, It is fine to perform any asynchronous operations in the Viewmodel with coroutines using the viewModelScope which means the task is executed even if the UI is not visible, however you should only do this for requests that less than or equal to 5 seconds but if it lasts more than that you should enqueue them as deferred or long running work with workmanager\
			-Easy to consume: UI should be able to easily render the produced UI state. \
\
		One-shot APIs as sources of state change\
			Use MutableStateFlow API as an observable, mutable container of state. In compose consider using mutableStateOf specially when working with Compose text APIs. Both APIs offer methods that allow safe atomic updates to the values they host whether or not the updates are synchronous or asynchronous. For MutableStateFlow use the update method\
\
		Mutating the UI state from asynchronous calls\
			For state changes that require an asynchronous result first launch a coroutine to run a suspend function and then use the state holder to write the result of the suspend function call into to observable API used to expose UI state			\
		Mutating the UI state from background threads\
			It is preferable to launch coroutines from main dispatcher for production of UI state, however it is possible to update UI state from a background context using the following APIs: \
				-When using coroutines in a viewmodel for example, you can use \'93withContext\'94\
				-When using MutableStateFlow use the \'93update\'94 method as usual\
				-When using compose state use \'93Snapshot.withMutableSnapshot\'94 to guarantee atomic updates to state in concurrent context\
\
		Stream APIs as sources of state change\
			For sources of state change that produce different values over time in a stream. Aggregating the outputs of all sources into a cohesive whole is a straightforward approach to state production. When using flows use the \'93combine\'94 function and then you can use the \'93stateIn\'94 operator to create a StateFlow which is an observable stream API. This operator gives the UI finer grained control over the activity of the state production pipeline as it may need to only be active when the UI is visible. This operator lets you use \'93SharingStarted.WhileSubscribed()\'94 if the pipeline should only be active when the UI is visible while collecting the flow in a lifecycle-aware manner. Use \'93SharingStated.Lazily\'94 if the pipeline should be active as long as the user may return to the UI, that is UI is on the back stack, or in another tab offscreen\
\
		State production pipeline initialization\
			Involves setting the initial conditions for the pipeline to run, that means providing initial input values critical for it to run. Initialize the pipeline lazily to conserve system resources, you can achieve this if using flows with the \'93started\'94 argument in the \'93stateIn" method. In the cases where this is inapplicable, define an idempotent \'93initialize()\'94 function to explicitly start the state production pipeline.\
			\
			Avoid launching asynchronous operations in the init block or constructor of a viewmodel. Asynch operations should not be a side effect of creating an object because those operations may read or write to the object before it is fully initialized. This is also referred to as leaking the object.  \
		\
	-Architecture Recommendations\
	From \'93guide to App Architecture\'94 we can find a document about \'93Architecture Recommendations\'94  in which we can find information about best practices when working with \'93Lifecycle\'94\
\
		LifeCycle (
\f5 \expnd0\expndtw0\kerning0
https://developer.android.com/topic/architecture/recommendations#lifecycle)
\f0 \kerning1\expnd0\expndtw0 \
		Do not override lifecycle methods in activities or Fragments use LifecycleObserver instead, if the app needs to perform work when the lifecycle reaches a certain a Lifecycle.State use the repeatOnLifecycle API\
\
		The reason to do this is explained in this other file https://developer.android.com/topic/libraries/architecture/lifecycle\
	\
		In this documentation you can find also best practices and concepts about the three layers in clean architecture, data layer, domain layer(optional), UI layer\
\
	\
\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\
\
HttpUrlConnection\
\
Is an alternative to using Retrofit or OkHttp\
\
\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\
\
Difference between Canvas, Windows and Activity\
\
These three concept play a different role in creating and managing user interface.\
\
	Activity\
	Is a core component of the Android framework that represents a single screen. It provides the user a way to interact with the app.\
\
	Window\
	Is higher-level abstraction that represents a single UI window or container for displaying the content of an Activity. Provides a framework for managing the presentation of UI, handling user interactions, and managing appearance of the screen. A Window can include various UI elements such as View, dialogs, and other widgets. The system provides default windows for activities, and you can customize the window\'92s appearance and behavior through themes, styles and layout XML. Elements like Activity, Dialog, StatusBar have their own window. Each window has its own \'93Surface\'94 on which to render\
\
	Canvas\
	Is a low-level drawing surface that allows you to draw graphics, shapes, text, and images directly onto it. Provides a way to create custom graphics and visuals within a view or a drawable. Provides methods for drawing, paths, shapes, text, bitmaps and other graphical elements. It\'92s often used for creating custom UI components, animations and special effects.\
\
	Now let\'92s see these three concepts in detail and introduce other concepts. When we create an Activity the \'93attach\'94 function is called before onCreate. The \'93attach\'94 method has a parameter of type \'93Window\'94 among others, this method is called by the Android Framework. The Activity class has a private property called \'93mWindow\'94 which is instantiated in the \'93attach\'94 method by creating a \'93PhoneWindow\'94 object, this means each activity created creates its own window.\
\
	PhoneWindow(Window)\
	This is basically a window, every activity creates one in the \'93attach\'94 method, This implementation of window has two important properties, \'93DecorView mDecor\'94 and \'93ViewGroup mContentParent\'94. In the constructor we actually copy the \'93DecorView\'94 of the window that was passed from the attach method parameter, this means the \'93DecorView\'94 is actually provided by the system because \'93attach\'94 method in activity is called by the framework itself. The mContentParent property is designed to hold other view elements\
\
	DecorView\
	Is the actual root container in the View hierarchy for an Activity, DecorView extends Framelayout, this means this is a view. The layout of this view is created based apps theme\
	\
\
When you create an activity the system calls \'93attach\'94 method, this method receives a Window object instance from the Android Framework, then every activity creates its own Window(PhoneWindow) using the provided instance from the SDK, this window that we\'92re provided contains a DecorView, the DecorView has a reference to the Window that created it and it holds that reference until the developer calls the Actiivity\'92s method called \'93setContentView\'94(usually called from onCreate). This acitivity\'92s method then calls the Window(PhoneWindow) method with the same name(setContentView) on the window instance it created, at this point this method calls other methods which do a lot of things but what we want to highlight right now is that it calls \'93setWindow\'94 on \'93DecorationView mDecor\'93 object to change the window the decorVIew contains and then it inflates the activity\'92s xml which is then draw on the window which is then draw by the DecorView since it has a reference to that window. Basically that means the activity contains a reference to a Window object and the window object contains a reference of a DecorView object which has a reference to the window that contains it and it is in charge of drawing to the window\
\
\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\
\
Context\
\
\pard\tx720\tx1440\tx2160\tx2880\tx3600\tx4320\tx5040\tx5760\tx6480\tx7200\tx7920\tx8640\pardirnatural\partightenfactor0
\cf0 \'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\
\
Termux\
\
Is a free and open-source terminal emulator for Android which allows for running a Linux environment on an Android device. \
\pard\tx720\tx1440\tx2160\tx2880\tx3600\tx4320\tx5040\tx5760\tx6480\tx7200\tx7920\tx8640\pardirnatural\partightenfactor0
\cf0 \
}