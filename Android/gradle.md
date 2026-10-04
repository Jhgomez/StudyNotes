* [Understanding the difference between libraries and applications](https://pan93412.github.io/gradle-docs-preview/userguide/library_vs_application.html)
* [Gradle Build Overview/ what is a build](https://developer.android.com/build/gradle-build-overview#is-build?), you can have android-application, android-library, java-library,
  kotlin-library modules. Android-application modules compile to APK or bundles, Android-libraries modules compile to AAR, java-library and kotlin-library
  modules compile to JARs. An android-application and android-library modules can consume any of the previously mentioned generated artifacts(AAR and JAR).
  the difference from and APK & AAR vs JAR is that the former types can inclue Android resources and configuration manifests while JAR files can't, this means
  a kotlin and java module can't have a dependency on an android module.
* [Create an Android Library](https://developer.android.com/studio/projects/android-library) **step to configure an android library module**
* coachmark, reveal effect, spotlight, tour guide, Product Tour,

* **Manage Your Build:** If you need to refresh the Gradle configurations of the "Android Gradle Plugin" for your Android's project app module you can search for
"Android Configure your build" or "Configure the Android Build System", you can also find the "Configure build variants" documenation there.
In a nutshell, the build types tells how the app is built/packaged, if it needs to be debugable, if it needs to optimized(obfuscated), and
signing configurations if needed, while the flavors helps you define what is the content of the app, this is because once you define flavors 
you're expected to then create the source sets you may need, and in those source sets you can define specific resource files, such as strings,
drawables, layouts, manifests, source files. Other important thing to know is, how those resources are then resolved at compile time, for example,
can we have the same class defined across source sets?, btw a source set can be specific to the build type, build flavor, and build variant(a 
combination of a build type combined with all possible combinations of all the flavor dimensions, I explain dimensions below),
and you also need to take into account the default main source set which should be used to define code that is common to all of the other
source sets, now, back to how the files are resolved, that is, from lowest to highest priority, main source set, flavor source set, 
build type source set, build variant source set, according to the documentation a class should not be defined in the same resolution track,
that means a class defined in main source set should not have another definition in the following source sets, and if you need different
implementation of a class in each source set, then you should define it at a level where it will not conflict with another definition in the 
same resolution track, however resources and manifest work differently as they actually can have different definitions in the same resolution
track, and lower priority level resources are overwritten by higher priority level source set, if there is no conflict they are just merged
instead of overwriting resources. There is one more "conflict" resolution that I haven't mentioned yet, flavors can have different dimensions,
for example I can have a dimension for "free" and "premium", but also a dimension for "api", those dimensions are declared to the AGP (`flavorDimensions`),
and then specified in the DSL of each declared flavor(`dimension` property), and in this case if you declare the same resource, for example same xml layout,
in two specific build flavors source set, then the priority is given by the order of the dimensions declared in `flavorDimensions`. You can
also add dependencies specific to a build variant as [stated here](https://developer.android.com/build/dependencies#configure_dependencies_for_a_specific_build_variant)

* **Creating Custom Android Gradle Plugins:** If you want to create a customs gradle plugin for Android most likely you will need to extend AGP,
[here](https://developer.android.com/build/extend-agp) is a guide to extend your build and write gradle plugins for Android that extend the,
this is used when creating convention plugins

* **[Varian API:](https://youtu.be/AZBW5StgF8o)** What is a variant? as you know we can define build types and product flavors, these are called
variant dimmensions, we define those in the AGP DSL(we can define them in a a custom convention gradle plugin). AGP uses variant
dimensions(combine them) to create several variant objects and an APK or Bundle will be built for each variant. Basically these variants provide
to the tasks that produces their end results(artifacts, like class files, the merged manifest, APK/AAB files, Android Resources) this API is used
to be able to customize the android build process, usually you'd get a task name, create a task that depends on its outputs, you can see a little
more on this [gradle task ordering documentation](https://docs.gradle.org/current/userguide/task_configuration_avoidance.html#sec:how_do_i_order_tasks)
which lives inside a documentation that talks about "Avoiding Unnecessary Task Configuration with Task configuration avoidance API". AGP doesn't
allows us to use those APIs because they consider the underliying task involved in the build process an "implementation detail", so they give us
this abstraction to modify the artifacts produced by each build variant. Basically it lets you execute a custom task inside the build pipeline.
The tasks that build the artifacts don't use the DSL values, what they actually use is the variant objects produced from the DSL, so what the
variant API is doing is letting us modify the variant objects that are used as the actual tasks input. Lear about it lifecycle phases which is
the actual interface we use to introduce a custom task that helps us change the artifacts in some way [here](https://developer.android.com/build/extend-agp#variant-api-artifacts-tasks)

* Use lazy gradle APIs as described [here](https://docs.gradle.org/current/userguide/task_configuration_avoidance.html#sec:old_vs_new_configuration_api_overview)

* **Android Gradle plugin in Convention Plugins:** `com.android.tools.build:gradle` (found in the [AGP documentation](https://developer.android.com/build/releases/about-agp#updating-plugin))
this is the whole android plugin as an android library, applying the plugin as a library is considered a legacy way to apply plugin(you can see that in the Gradle
plugins website). `com.android.tools.build:gradle-api` (found in ["Creating Gradle Plugins"](https://developer.android.com/build/extend-agp#why-compile-gradle-api)
android documentation), is also a library, in that documentation they compare the one I mentioned first with this one, the difference lies in that the first is the
whole the AGP(the implementation, build tasks, etc), and this one is just the public interface so it hides implementation details, this is the preferred artifact when
writting custom Gradle plugins that adds functionality to AGP since it is lighter and it provides everything you need(depending on what your plugin aims to do). While
I was trying to configure Kotlin through a custom convention plugin in an included build(build-logic) I was trying to find the `KotlinAndroidProjectExtension` which is
the DSL AGP("application" and "library" plugins of the AGP) provides to us to configure Kotlin, remember that the AGP now embeds Kotlin Gradle plugin, but It seems like
the `gradle-api` artifact doesn't provide this API, so since I know configuring Kotlin would be possible through the Kotlin Android plugin(this is what we used to add
before the AGP automated the process for us just recently) I added the plugin with the legacy approach
`compileOnly("org.jetbrains.kotlin.android:org.jetbrains.kotlin.android.gradle.plugin:2.4.0")`, the version seems to match the kotlin version I'm using in
the `org.jetbrains.kotlin.plugin.compose` so I can keep these two in sync. Another thing you might like to know is that the `android` DSL in an Android library module is
provided by `LibraryExtension`, and in an Android application module it is provided by `ApplicationExtension`. These two classes implements `CommonExtension` so if you
want to create a common Kotlin extension function that can configure both types of modules you can use the common interface.

# Publish Android library
using git bash in windows
1. First of all, you can check the gradle cookbook [here](https://cookbook.gradle.org/integrations/maven-central/publishing/)

2. I choosed Vanniktech plugin, check their docu [here](https://vanniktech.github.io/gradle-maven-publish-plugin/central/)

3. I followed their docu, so I had to create a user in maven central using my email, then create a namespace(which
references my github profile), then I had to configure the plugin DSL in the gradle buildscript and in order to complete that
configuration I created a key using GPG in gitbash(git windows utility with bash commands) with the bellow instructions,
also I had to create a token in maven central, the plugin gradle config is exactly what you see in the plugin docu I referenced,
check my repo for the full example[https://github.com/Jhgomez/Coachmark] in the coachmark module

* All I did is follow documentation [here](https://vanniktech.github.io/gradle-maven-publish-plugin/central/), which
is part of the same documentation that describes the requirements to publish to maven central using the mentioned 
plugin. That documentation indicated to create the key following maven central's documentation [here](https://central.sonatype.org/publish/requirements/gpg/#generating-a-key-pair)
so first do `gpg --gen-key` note that you can find more interactive commands to customize the properties of your key
like the algorithm used to encrypt and the duration/expiration date of the key, etc. You need to enter your name, email,
passhprase(password), each file in this repo will have the info about each key. Also be aware that you have to publish
your public key, the instructions are in the docu

* after creating it you need to create environment variables so that the plugin can find the key you just created and
use it to sign the library articfact, that is going to be generated. The environmet variables will ge generated with
the following bash commands, but first get your key's id with the command `gpg --list-keys`, you can sign diferent
artifacts for different libraries you create with the same key, having a single key for different artifacts has pros
and cons as well as having different keys for each artifact, is up to you. The key id is a very long alpha numeric
value and you'll use it in the following commands, again this will create temporary env variables, so you need
to execute the commands patter below everytime you publish a new version, also be aware you need to execute it from
the same terminal you will use gradle to execute the plugin task that publishes to maven, I will leave the IDs and
passwords in each project folder qui.md file

```
export ORG_GRADLE_PROJECT_signingInMemoryKey="$(gpg --armor --export-secret-keys <key_id>)"
export ORG_GRADLE_PROJECT_signingInMemoryKeyPassword='myPasswordSlachKeyPhrase'
```

note `gpg --export-secret-keys --armor <key id>` prints the content of your secret key

* Now you need to create a token in maven central, follow [this](https://central.sonatype.org/publish/generate-portal-token/)
documentation, once you have it create the following gradle properties in the `gradle.properties` file in your project

```
mavenCentralUsername=yourUserNameAsListedInTheDocuIndicatedInThisStep
mavenCentralPassword=yourTokensPasswordAsInReferencedDocu
```

* There is a few things we might want to know, for example newer version(like the one I used, 2.4.7) of gpg doesn't
generate kbx files for each public key and a folder with the private keys, it should be called similar to `private-keys-v1.d`
but "funny" thing is that this plugin doesn't use those files at the moment so, and it uses a "weird" set up I still
might not understand fully, and instead it asks you to generate keys(actually only private key) with the "old" format,
a format that seems to be the previous default, which is ".gpg" and or ".asc" and it seems that they used to be 
called pubring.gpg and secring.gpg, and that is exactly what the command `gpg --export-secret-keys --armor <key_id>`,
it is similar to exporting the secret key in the old format, so you may want to create and store the value returned
by this command in a file with the names and extensions previously mentioned, however this didn't work for me for
some reason, it looks like the plugin was not being able to find the public key by this private key when I used the
gradle properties indicated in the docu so I changed to env variables approach and it work, but the approach is 
"different" as we now pass the private key in an environmet variable and then the plugin along with gpg finds the
public key that corresponds to that private key to sign the artifact, they call it an in memory environment variable

* After all this is done you can execute the gradle task `./gradlew publishToMavenCentral`, then just check the 
deployments section in your maven central's website, in your account, in the namespace section and in the deployments
option you can confirm the lib is available from there, check [this](./gradlew publishToMavenCentral) link
