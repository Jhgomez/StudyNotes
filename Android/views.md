
* public abstract class **Transition** / package androidx.transition: Subclasses are Autotransition, ChangeBounds, ChangeClipBounds, ChangeImageTransform, ChangeScroll, ChangeTransform, Explode, Fade, Hold,
  LavelMoveTransition, Slide, TextScale, TransitionSet, Visibility. Any Transition has two main jobs: (1) capture property values, and (2) play animations based on changes to captured property values. Transitions
  may not work correctly with either SurfaceView or TextureView, due to the way that these views are displayed on the screen. For SurfaceView, the problem is that the view is updated from a non-UI
  thread, so changes to the view due to transitions (such as moving and resizing the view) may be out of sync with the display inside those bounds. TextureView is more compatible with transitions in
  general, but some specific transitions (such as Fade) may not be compatible with TextureView because they rely on android.view.ViewOverlay functionality, which does not currently work
  with TextureView. Transitions can be declared in XML resource files inside the res/transition directory.

* public interface **TypeEvaluator<T>**/ package android.animation: Interface for use with the ValueAnimator.setEvaluator(TypeEvaluator) function. Evaluators allow developers to create animations on arbitrary
  property types, by allowing them to supply custom evaluators for types that are not automatically understood and used by the animation system.

* public class **ViewGroupOverlay** extends **ViewOverlay**/ package android.view: is an extra layer that sits on top of a ViewGroup (the "host view") which is drawn after all other content in that
  view (including the view group's children). Interaction with the overlay layer is done by adding and removing views and drawables. You can not instantiate this class instead a view child like ImageView 
  or TextView will call `this.getOverlay()` it return and instance of `ViewOverlay` which only accepts drawables while in a ViewGroup child LinearLayout, FrameLayout, etc we get an `ViewGroupOverlay`
  which accepts also views besides drawables

* public class **GestureOverlayView** / package android.gesture: A transparent overlay for gesture input that can be placed on top of other widgets or contain other widgets.

* public class **GestureDetector** / package android.view: Detects various gestures and events using the supplied MotionEvents. The GestureDetector.OnGestureListener callback will notify users when a
  particular motion event has occurred. This class should only be used with MotionEvents reported via touch (don't use for trackball events). To use this class:

    * Create an instance of the GestureDetector for your View
    * In the View.onTouchEvent(MotionEvent) method ensure you call onTouchEvent(MotionEvent). The methods defined in your callback will be executed when the events occur.
    * If listening for GestureDetector.OnContextClickListener.onContextClick(MotionEvent) you must call onGenericMotionEvent(MotionEvent) in View.onGenericMotionEvent(MotionEvent).

* **ColorFilter vs Tint**: You can set color filter to an ImageView, drawable and paint objects and a tint color to a drawable, they are very similar since they change the color of a drawable, you could
  even think of setting tint color property as a simple version of setting color tint, you might like to use tint property for simple use cases for that use the `setTint` method or the properties in the layout
  with `android:tint` and `android:tintMode` to set mode, but for more complex tasks you should use color filter. You can use/set color filter in any Paint object, this means you can use it to draw on the canvas   of any custom view. There is three implementations of color filter interface `PortterDuffColorFIlter`, `LightingColorFIlter` and `ColorMatrixColorFilter` being the last one the most flexible meaning it
  allows you to manipulate the colors even further. There are some alternatives to Color Filter like `Shader` and `MaskFilter`, you can not create a custom implementation of Color Filter if you
  need "full power" you can use the OpenGL alternative which would give access to GLSL(GL shader language) shaders

* **Pallete API**: API included in Android Support Library, it lets you extract prominent colors from an image. You can load your drawables as a Bitmap and pass it to Palette to access its colors. For more information, read [Selecting colors with the Palette API.](https://developer.android.com/develop/ui/views/graphics/palette-colors)

* Using Glide vs Loading Local drawable resources: Leverage caching strategies. Implement disk and memory caching to prevent redundant resource loading. Using libraries such as Glide or Picasso can help reduce memory usage by managing image loading efficiently. On average, these libraries can decrease memory consumption by 50%, leading to smoother scroll performance and a more responsive interface.

* Resource optimization

| Optimization Technique |	Percentage Improvement | Tool/Technology |
| ---------------------- | ----------------------- | --------------- |
| Vector Graphics	| 80% file size reduction	| SVG |
| Adaptive Icons	| 20% loading time decrease	| Android Adaptive SDK |
| Image Compression	| 25-34% size savings	| WebP |
| Memory Caching	| 50% memory usage reduction	| Glide/Picasso |
| Lazy Loading	| 30% load time reduction	| Custom Implementation |
| Resolution-Specific Assets | Variable improvement	| Android Resource Qualifiers |
| Unused Asset Cleanup	| 5-15% APK size reduction	| Android Lint |

* Types of Drawables: there are several but in this case we want to mention "Nine-Patch"/"9-Patch" Images which are usually used for Stretchable Backgrounds

* **9-Patch vs Vector**: In vector graphics all sides are scaled or stretched when we set it to any background whereas in 9-patch we can define which sides can scale or stretch so at runtime only those side scale
  which we set it to scale in 9-patch tool.

* **Shader**: They are applied to a paint objcet. Implementations we can use are:
    * **BitmapShader**: Used to draw a bitmap as a texture. It can repeat or stretch the bitmap across the drawing area.
    * **RadialGradient**: Creates a gradient that transitions between colors along a straight line.
    * **SweepGradient**: Produces a gradient that sweeps around a central point in a circular fashion.
    * **ComposeShader**:  Combines two shaders using a blending mode.
    * **RuntimeShader**:  Introduced in Android 13, this allows developers to define custom per-pixel effects using the Android Graphics Shading Language (AGSL).

* **MaskFilter**: Base class for object that perform transformations on an alpha-channel mask before drawing it. A subclass of MaskFilter may be installed into a Paint. Blur and emboss are implemented as
  subclasses of MaskFilter. BlurMaskFilter only blurs the alpha mask of what you draw with a Paint in onDraw()—it creates a soft edge/“glow”. It does not Gaussian-blur arbitrary view content, and it doesn’t
  affect child views drawn by the framework. It also often requires software rendering (setLayerType(LAYER_TYPE_SOFTWARE, …)), so it’s the wrong tool for a container blur. It looks good on text, you can do
  `getPaint` on an TeztView

