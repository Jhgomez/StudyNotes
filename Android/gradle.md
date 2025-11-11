* [Understanding the difference between libraries and applications](https://pan93412.github.io/gradle-docs-preview/userguide/library_vs_application.html)
* [Gradle Build Overview/ what is a build](https://developer.android.com/build/gradle-build-overview#is-build?), you can have android-application, android-library, java-library,
  kotlin-library modules. Android-application modules compile to APK or bundles, Android-libraries modules compile to AAR, java-library and kotlin-library
  modules compile to JARs. An android-application and android-library modules can consume any of the previously mentioned generated artifacts(AAR and JAR).
  the difference from and APK & AAR vs JAR is that the former types can inclue Android resources and configuration manifests while JAR files can't, this means
  a kotlin and java module can't have a dependency on an android module.
* [Create an Android Library](https://developer.android.com/studio/projects/android-library)
* coachmark, reveal effect, spotlight, tour guide
