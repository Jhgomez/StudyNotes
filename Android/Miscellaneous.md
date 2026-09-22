* [feature modules](https://developer.android.com/guide/playcore/feature-delivery#customize_delivery): This feature has to due with the app size, be aware apps have a size limit in the play store, so how are applications like games published(they are quite big), these types of apps very often use this feature, this means that they publish something like a base module or base version of the app and other parts of it are downloaded on demand using feature modules, this way the app can be both, publish on the play store and get bigger on users demand to extend its functionallity.

* [Multi-window Features](https://developer.android.com/develop/adaptive-apps/guides/support-multi-window-mode): **Split-screen mode** fills the screen with two apps, showing them either side by side or one above the other. Users can drag the divider separating the two apps to make one app larger and the other smaller.**Picture-in-picture mode** enables users to continue video playback while interacting with another app and similar things. **Desktop windowing mode**, in which users can freely resize each activity, can be enabled by manufacturers of large screen devices.

* **Dependency Injection Frameworks:** Dagger, Dagger/Anvil, Dagger/Hilt, Koin, Metro, for KMP Metro seems to be the more performant option

    Android 16 (API level 36) overrides screen orientation, aspect ratio, and resizability restrictions, but this only seems to hold true for large screen devices

