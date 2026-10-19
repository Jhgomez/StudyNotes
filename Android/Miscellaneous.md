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

  Every rendering system needs something that can be called a "render loop" or some sort of pulse to know when to draw on screen, this is because rendering systems
  need to draw ne content at some interval(usually that is called FPS, frames per second, the ideal rate for the human eye is 60-120 frames per second to see a very
  fluent screen), in Android that happens via `Choreographer`, it basically provides a callback on every frame, this helps the rendering system know when is the
  appropriate time to collect the rendering info and then displaying it, previously this was done randomly(without using a pulse) in Android but now it is done using
  this pulse, if you do it randomly you could get some tearing(drawing at the same time as the screen is being refreshed, means you may be drawing your next frame at
  the same time as the previous frame is also displayd causing animation to look rather messy and also input events should be gotten directly before you start drawing
  stuff which reduces latency when the user taps on the screen and when the result of the taps appear as rendering objects on screen), so display synchronization
  avoids "tearing" and optimizes input latency, this pulse is in sync with whatever the underlying hardware is doing to refresh. The difference between a UI toolkit,
  either the view system or compose, and games, is that first you need to know games usually run using some engine like Unity, Unreal, etc, and those engines actually
  override the whole view hierarchy and even the window that a normal application would need to be displayed and render effectively only when needed(when invalidations
  happens) so that is the difference, ui toolkit rendering elements re-render only when they have been invalidated while game engines usually render on a loop, meaning
  they render each frame even if there is no changes, which is a reason why games could drain more battery than a regular app
  




Android 16 (API level 36) overrides screen orientation, aspect ratio, and resizability restrictions, but this only seems to hold true for large screen devices

https://developer.android.com/studio/write/lint
