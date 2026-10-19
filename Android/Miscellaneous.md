* [feature modules](https://developer.android.com/guide/playcore/feature-delivery#customize_delivery): This feature has to due with the app size, be aware apps
have a size limit in the play store, so how are applications like games published(they are quite big), these types of apps very often use this feature, this
means that they publish something like a base module or base version of the app and other parts of it are downloaded on demand using feature modules, this way
the app can be both, publish on the play store and get bigger on users demand to extend its functionallity.

* [Multi-window Features](https://developer.android.com/develop/adaptive-apps/guides/support-multi-window-mode): **Split-screen mode** fills the screen with two
apps, showing them either side by side or one above the other. Users can drag the divider separating the two apps to make one app larger and the other smaller.
**Picture-in-picture mode** enables users to continue video playback while interacting with another app and similar things. **Desktop windowing mode**, in which
users can freely resize each activity, can be enabled by manufacturers of large screen devices.

* **Dependency Injection Frameworks:** Dagger, Dagger/Anvil, Dagger/Hilt, Koin, Metro, for KMP Metro seems to be the more performant option, Kotlin-Inject

* [Creating a UI Toolkit From Scratch by Romain Guy and Chet Haase](https://youtu.be/4U9B0qMxIc0?si=BSjpHvTGIm-s-6DV): Real-time rendering systems process 3D
data and generate images instantly, typically at 30 to 120 frames per second. By using dynamic approximations of lighting rather than pre-computing every photon,
they allow immediate user interaction. These systems form the backbone of video games, VR, and interactive architectural design tools. 

  Unreal, unity, blender are rendering systems, they seem to be used in CAD apps too

  An Entity Component System (ECS) AKA entity component framework, is a software architectural pattern predominantly used in game development that favors composition
  over class inheritance. Instead of objects containing both data and behavior, an ECS rigidly separates them into three parts: Entities (unique IDs), Components
  (pure data), and Systems (pure logic).

  All rendering systems need something to render to, they can be referred to as Rendering Surface or Drawing Surface, on Android that something is a Surface, a
  surface can be retrieved by TextureView, SurfaceView, Window or a custom layout. The view system and compose both access the window surface via the canvas.

  Android supplies the canvas from the surface, so the communication with the surface happens in draw and onDraw. When an activity starts and the window, decorview,
  content view is created, a surface is created under the hood

  You should be able to get a frame callback in any rendering system/UI toolkit, it is a callback that runs on every frame.

  In Android the WindowManager is the component basically pulling all the string with the help of other components to provide a way our activities can interact with
  the surface, there is something called `ViewRootImpl`, it kind of holds a reference to the window(IWindow) that is in the system server, it is some sort of root
  element that is responsible for connecting the underlying surface and its canvas with the activity and is also responsible for triggering the first layout, top
  level layout, top level drawing, top level motion, and event dispatching, in theory it should receive a reference to a `SurfaceHolder` there is much more going on
  and there is more components participating in this process(it means it might not literally be doing that directly but the idea behind the process is that), in the
  UI toolkit of [this example](https://github.com/romainguy/experiment-apex/blob/main/apex/src/main/java/dev/romainguy/apex/Integration.kt), `RootElement` is similar
  to it, as you can see it keeps a reference to the holder which provides the Canvas.



  




Android 16 (API level 36) overrides screen orientation, aspect ratio, and resizability restrictions, but this only seems to hold true for large screen devices

https://developer.android.com/studio/write/lint
