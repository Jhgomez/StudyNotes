
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

* Live wallpapers: They make use of the ``
```
class MyWallpaperService : WallpaperService() {
  override fun onCreateEngine(): Engine = WallpaperEngine()

  private inner class WallpaperEngine : WallpaperService.Engine() {

    override fun onTouchEvent(event: MotionEvent?) {
      if (event?.action == MotionEvent.ACTION_DOWN) {
        val canvas = surfaceHolder?.lockCanvas() ?: return

        val paint = Paint().apply {
          val randomColor = Random.nextInt(16_777_216)
            .toString(16)
            .padStart(6, '0')
          color = Color.parseColor("#$randomColor")
          style = Paint.Style.FILL
        }
        canvas.drawPaint(paint)

        surfaceHolder.unlockCanvasAndPost(canvas)
      }
    }
  }
}
```

```xml
<?xml version="1.0" encoding="utf-8"?>
<manifest>
  <application>

  <service
      android:name="MyWallpaperService"
      android:enabled="true"
      android:permission="android.permission.BIND_WALLPAPER">
    <intent-filter>
      <action android:name="android.service.wallpaper.WallpaperService" />
    </intent-filter>

    <meta-data
        android:name="android.service.wallpaper"
        android:resource="@xml/my_wallpaper" />
  </service>

  <uses-feature
      android:name="android.software.live_wallpaper"
      android:required="true" />
  </application>
</manifest>
```

* The `<merge />` tag is extremely useful and can do wonders in your code. However, it suffers from a couple of limitation:

  * <merge /> can only be used as the root tag of an XML layout
  * When inflating a layout starting with a <merge />, you must specify a parent ViewGroup and you must set attachToRoot to true (see the documentation of the inflate() method)

* `ViewStub` is a powerful variation of `<include />` that can help you further optimize your layouts without sacrificing features. You need to set the `layout` property to the layout you want to inflate into the `ViewStub`. When you are ready to inflate the stub, simply invoke the `inflate()` method. You can also simply change the visibility of the stub to VISIBLE or INVISIBLE and the stub will inflate. Note however that the `inflate()` method has the benefit of returning the root View of the inflate layout. It is very important to remember that after the stub is inflated, the stub is removed from the view hierarchy. As such, it is unnecessary to keep a long-lived reference, for instance in an class instance field, to a ViewStub. It's cheap and easy. The only drawback of `ViewStub` is that it currently does not support the `<merge />` tag.

* `Windwow` and `DecorView`: When you setup your user interface by calling `setContentView()` on an Activity, Android adds your views to the Activity's window. The window however does not contain only your views, but a few others created for you. The most important one is the `DecorView`. The `DecorView` is the view(FrameLayout) that actually holds the window's background drawable. Calling `getWindow().setBackgroundDrawable()` from your Activity changes the background of the window by changing the DecorView's background drawable. If you ever have an activity which background is not visible, probably because there is an opaque view on top of it like an `ImageView`, `MapView` or `WebView`, you can gain a little performance by setting the Activity's theme with the attribute `android:theme=@style/Theme.Custom` in the manifest inside the `<activty />` or `<application />` tag. According to [this document](https://android-developers.googleblog.com/2009/03/window-backgrounds-ui-speed.html), Android UI toolkit is not smart enough to prevent the drawing of views hidden by opaque children so we can leverage this optimization
    ```
    <resources>
      <style name="Theme.NoBackground" parent="android:Theme">
          <item name="android:windowBackground">@null</item>
      </style>
    </resources>
    ```
*  "focusable in touch mode" refers to a special mode that allows certain views, like EditText or AutoCompleteTextView, to receive focus when the user enters touch mode. This concept and "touch mode" seems to be very important previously in Android because in the past not all phone where touchscreen but now pretty much all devices are touch screen, touch mode is entered when the last interaction withn an app is from the touch of the screen

*  `OnClick` vs `OnTouch`: touch can acomplish the same functionallity as click but not the way around, this is because click is a very simple callback and doesn't provide much info about the event while touch
  provides a lot info about the event, you can distinguish gestures and position.

* **Event Handling System**: Events represent user interactions with the application, they are managed by the Android framework and handled using event listeners and event handlers

* `CollapsingToolbarLayout`: It wraps a `Toolbar` and at the same time it should be wrapped by an `AppBarLayout`

* `AppBarLayout`: There is a few interesting use cases like when wrapping a `CollapsingToolbarLayout` with this view, also when creating a app bar(also called toolbar) with more than one child like when wrapping a `Toolbar` and a `TabLayout` with this view and in this use case usually there is a `CoordinatorLayout` wrapping the `AppBarLayout` to enable animations. Basically this view lets you create interesting and very custom app bars/top bars/toolbars 

* `TopAppBar`/`Toolbar`/ `ActionBar`: They are basically the same visual component but is the different names you can find it with and also the names seend during its evolution throughout time, and basically they have different features basically the newer implementations have more "up to date" features, the newest implementation being `Toolbar` which can be found in material design

* `DrawerLayout` with `NavigationView`: UI component implemented in material design library, basically the drawer is the `NavigationView` view which has to be wrapped by a `DrawerLayout`

* **Dialogs**: If your app uses Activity 1.5.0 or higher, you can implement custom back navigation for a dialog by using `ComponentDialog` and its `OnBackPressedDispatcher`. `AlertDialog`s implement that interface so just by creating that type of dialogs you can get an instance of the back dispatcher

* **Views that can be integrated with NavController**: `TopAppBar`/`Toolbar`/ `ActionBar`, `CollapsingToolbarLayout`, `AppBarLayout`, `DrawerLayout` with `NavigationView`, and `BottomNavigationView`
