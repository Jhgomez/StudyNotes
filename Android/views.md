
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

* public class [GestureDetector](https://developer.android.com/develop/ui/views/layout/custom-views/making-interactive#inputgesture) / package android.view: Detects various gestures and events using the supplied MotionEvents. The GestureDetector.OnGestureListener callback will notify users when a
  particular motion event has occurred. This class should only be used with MotionEvents reported via touch (don't use for trackball events). To use this class:

    * Create an instance of the GestureDetector for your View
    * In the View.onTouchEvent(MotionEvent) method ensure you call onTouchEvent(MotionEvent). The methods defined in your callback will be executed when the events occur.
    * If listening for GestureDetector.OnContextClickListener.onContextClick(MotionEvent) you must call onGenericMotionEvent(MotionEvent) in View.onGenericMotionEvent(MotionEvent).
 
  We can use this API/interface to implement things like [drag and scale](https://developer.android.com/develop/ui/views/touch-and-input/gestures/scale)

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

* `TopAppBar`/`Toolbar`/ `ActionBar`: They are basically the same visual component but is the different names you can find it with and also the names seend during its evolution throughout time, and basically they have different features basically the newer implementations have more "up to date" features, the newest implementation being `Toolbar` which can be found in material design. You might not want to set up your `toolbar` with Navigation controller so in simple use cases where you might not need to link it to ta navigation graph just set up your toolbar with the following function `setSupportActionBar(myToolbar)`, Be aware that the reason you should set a toolbar as [described here](https://developer.android.com/develop/ui/views/components/appbar/setting-up) is that the apps come by default with an `ActionBar` which since depends on the platform it is running on, it will have different functionallity available so for this reason is best to use something more stable which is the main reason you want to hide the action bar and replace it with the "AndroidX AppCompat library" since you can control its version you will get backwards compatibility and stability

* `DrawerLayout` with `NavigationView`: UI component implemented in material design library, basically the drawer is the `NavigationView` view which has to be wrapped by a `DrawerLayout`

* **Dialogs**: If your app uses Activity 1.5.0 or higher, you can implement custom back navigation for a dialog by using `ComponentDialog` and its `OnBackPressedDispatcher`. `AlertDialog`s implement that interface so just by creating that type of dialogs you can get an instance of the back dispatcher.

* [Show a dialog fullscreen or as an embedded fragment](https://developer.android.com/develop/ui/views/components/dialogs#FullscreenDialog): First override `onCreateDialog` to add the below code
  ```
  Dialog dialog = super.onCreateDialog(savedInstanceState);
  dialog.requestWindowFeature(Window.FEATURE_NO_TITLE);
  retun dialog;
  ```
  Then in your activity or fragment call something like this
  ```
  if (isLargeLayout) {
      // The device is using a large layout, so show the fragment as a
      // dialog.
      myDialogFragment.show(fragmentManager, "dialog");
  } else {
      // The device is smaller, so show the fragment fullscreen.
      FragmentTransaction transaction = fragmentManager.beginTransaction();
      // For a polished look, specify a transition animation.
      transaction.setTransition(FragmentTransaction.TRANSIT_FRAGMENT_OPEN);
      // To make it fullscreen, use the 'content' root view as the container
      // for the fragment, which is always the root view for the activity.
      transaction
        .add(android.R.id.content, myDialogFragment)
        .addToBackStack(null)
        .commit();
  }
  ```
  To define the `isLargeLayout` variable use two resource qualifiers `res/values/bools.xml` and `res/values-large/bools.xml`
  ```
  <!-- true in large and false in regular size -->
  <resources>
    <bool name="large_layout">true</bool>
  </resources>
  ```
  Then consume it with
  ```
  isLargeLayout = getResources().getBoolean(R.bool.large_layout);
  ```

* [Show an activity as a dialog on large screens](https://developer.android.com/develop/ui/views/components/dialogs#ActivityAsDialog): To show an activity as a dialog only on large screens, apply the Theme.Holo.DialogWhenLarge theme to the <activity> manifest element:
  ```
  <activity android:theme="@android:style/Theme.Holo.DialogWhenLarge" >
  ```

* **Views that can be integrated with NavController**: `TopAppBar`/`Toolbar`/ `ActionBar`, `CollapsingToolbarLayout`, `AppBarLayout`, `DrawerLayout` with `NavigationView`, and `BottomNavigationView`

* **Action Mode/ActionMode**: Things I know I can do with this API is create something similar to a menu on the top app bar with **contextual action mode** menus which is an implementation of this API. The other thing is enable text selection in `TextView`, `EditText`, and `WebView`. In a `TextView`, for example, when you select text you will see options that display inside the top app bar and you will see default options("copy" and "paste") but you can add your custom options by passing `true` to the `TextView` method `setTextIsSelectable`, then pass a callback to `setCustomSelectionActionModeCallback` in which you can add, remove options to the menu displayed by the `ActionMode`, in text views when implementing this logic you will need `TextView`'s methods like `getSelectionStart()` and `getSelectionEnd()` to perform your actions

* **Types of Menus**: We can find **"Options Menu"s**, in an activity override method `onCreateOptionsMenu`(always call `return super.onCreateOptionsMenu(menu);`) and handle clicks in the menu items overriding `onOptionsItemSelected` and in a Fragment you need to get instance of activity, parse it to `MenuHost` and add a provider with the method `addMenuProvider` if you need to navigate when an option is selected then in the "options selected" method return the boolean value with the following code `NavigationUI.onNavDestinationSelected(item, navController) || super.onOptionsItemSelected(item);`. If you want to modify/update your menu then the [official documentation](https://developer.android.com/develop/ui/views/components/menus#ChangingTheMenu). Other type is **"Contextual Menu"**, they offer actions that affect a specific item, very commonly used with recyclerview items and there is two ways we can display a contextual menu, a **floating context menu** which is displayed similar to a dialog, to create pass the view you want to be attached the menu to to the method `registerForContextMenu()` and override methods `onCreateContextMenu`(here you inflate menu with menuInflater calling `getMenuInflater`) and `onContextItemSelected`. The second option we have to display a contextual menu is **contextual action mode** this is an implementation of `ActionMode`, they display a contextual action bar, or CAB, at the top of the screen with action items that affect the selected item(s). When this mode is active, users can perform an action on multiple items at once. This CAB isn't necessarily associated with the app bar. They operate independently, although the contextual action bar visually overtakes the app bar position, its UI is usually presented either when a click/touch and hold(LongClick) happens or items with a chedcbox are selected. Check [this documentation](https://developer.android.com/develop/ui/views/components/menus#CABforViews) to see how to implement it. The third and last last type of menu(after contextual menu) is a **"Popup Menu"**, this isn't the same as a context menu, which is generally for actions that affect selected content. For actions that affect selected content, use the contextual action mode or floating context menu. You can create a popup menu with the below code. Icons at the top app bar are usally called **"Actions"** and options that don't fit inside the top app bar and are displayed in a three dot icon are called **"Overflow menus"**.

```
PopupMenu popup = new PopupMenu(this, v);
    popup.getMenuInflater().inflate(R.menu.actions, popup.getMenu());
    popup.show();
```

* [Action Views and Action Providers](https://developer.android.com/develop/ui/views/components/appbar/action-views): Now that we have talked about action mode and menus, you can see those concepts are related, and at the same time those concepts are related to this one and we will even expand those further when we talk about other APIs below, like performing a search with a `SearchView`, or `ShareActionProvider`(used to easily add a share button to your app’s ActionBar or Toolbar). Basically both, action views and action providers are visual components that live in the action bar/toolbar/top app bar, **action views** are for example, again, a `SearchView` and **action providers** are for example, also again, a `ShareActionProvider`, basically an action view lets you perform some action on the top app bar without having to change activities or fragments while action providers initially appear as a button(on the top app bar) or menu item(this one also on the top app bar but since there exists different types of menus maybe we could use this in those different types of menus also and not all types of menus are option menus, we could also use them with contextual menus or popup menus maybe). To implement an **action view** in a menu you do that in the items definition(Menu xml file), to an item element set one of the following attributes `app:actionViewClass`(class of a widget that implements the action) or `app:actionLayout`(ayout resource describing the action's components), then set `app:showAsAction` attribute to `ifRoom|collapseActionView` or `never|collapseActionView`(`collapseActionView` flag indicates how to display the widget when the user isn't interacting with it), you can configure the action inside activity's `onCreateOptionsMenu` method, in there find the menu item in which you declared the previously mentioned properties with this code `menu.findItem(R.id.action_search)` with the `MenuItem` object obtained you can write the following line `SearchView searchView = (SearchView) searchItem.getActionView();` and here you have a reference to the action view, in this case a `SearchView`, that you can add listeners to configure any action you want to perform when user inputs some text. An action view can expand and you can add listeners for that in the same method we just mentioned(`onCreateOptionsMenu`), create a listener with `new OnActionExpandListener()`, and use the menu item we are configuring as an action view(we already showed how to find it) and pass it here `MenuItemCompat.setOnActionExpandListener(actionMenuItem, expandListener);`. To add an **action provider**, similarly to the action view, set the property `app:actionProviderClass` to the fully qualified class name for the action provider class, for example `app:actionProviderClass="androidx.appcompat.widget.ShareActionProvider"`, and also set `app:showAsAction="ifRoom"`, be aware it's unnecessary to declare an icon for the widget, since `ShareActionProvider` provides its own graphics. If you are using a custom action, declare an icon.

* `Backdrop` Vs `BottomDialogSheet`: These are UI components defined in Material Design 2, the former is used as a main container while the later is used to provide optional/additional information. The former has concepts like front and back layers while those concepts don't exist in the later, they might look similar at first but they are actually different.

* [Settings Component](https://developer.android.com/develop/ui/views/components/settings): This API is used to design a native look settings screen fragment(implementing `PreferenceFragmentCompat`), we can find [native design guidelines](https://source.android.com/docs/core/settings/settings-guidelines) to create these screens and according to the official documentation, the settings are stored by default using `SharedPreferences`

* [Search Component](https://developer.android.com/develop/ui/views/search): You can implement this as `SearchView` view which can be added in the top app bar as an action in the options menu of the top app bar if you want the search UI to be displayed when the user taps an icon of your choice on the top app bar that you want to set up as the search view "starter" then you have to configure it when creating the menu, if for any reason your icon is added to the overload menu of the top app bar then it won't display the search UI on the top app bar in which case you have to be prepared for this scenario and make use of the other option to display a search interface with the `Search Dialog`, if you can be sure the icon will be always visible in the top app bar then with the search view is enough otherwise you should be prepared with both. Be aware it doesn't have to be implemented in the top app bar, however it usually is. After you have the UI you have to configure how your search interface will behave with an xml file of type `searchable`(this type of configuration can not be created at runtime), after you create a configuration you need to create an Activity, this is because when a search is performed with these UI components then an intent is created an you search activity is started and passed to the activity, the intent will contain some extras you can use to implement the search logic. With all of these configurations, components and views then you can enable voice search(this uses the recognizer API under the hood), Provide search suggestions based on recent user queries(uses a content provider of type `SearchRecentSuggestionsProvider` under the hood, btw this type of result seem to only support text so you would have to work your logic using strings), provide custom search suggestions that match actual results in your application data(it also uses a content provider under the hood but here you have to create a database table in which you can configure lots of options like an intent that will be launched, another column to include an extra in the intent that is launched when an itme in clicked), the last feature we will talk about is to offer your application's search suggestions in the system-wide Quick Search Box(for this you have to implement the previous feature of custom search results).

* [AppSearch](https://developer.android.com/develop/ui/views/search/appsearch): This API is commonly used along with the search component. Lets explain it with an example, [this](https://github.com/android/search-samples/tree/main/AppSearchSample) note taking app uses `AppSearch` to index a user's notes and allows users to search over their notes, you can also see the `SearchView` used in combination with `AppSearch` in this example. The reason behind using this API could be to have a fast, mobile-first storage implementation with low I/O use, also it offers highly efficient indexing and querying over large data sets, and has relevance ranking and usage scoring. All these features of this API are great but maybe the one almost everybody looks at first is that is very performant, it offers lower latency for indexing and searching over large datasets **compared to SQLite**. AppSearch simplifies cross-type queries by supporting single queries whereas SQLite merges results from multiple tables.

* **Recognizer**: There are different types of recognizers that help do things like, Speech to text/Speech Recognition(using `RecognizerIntent`). Optical Character Recognition (OCR) in Android allows you to extract text from images or videos, you use ML Kit (Google's Machine Learning Library) to interact with the `TextRecognizer` API which is used to recognize text in images or video, such as street signs, it seems to be possible to use an implementation of the `TextRecognizer` API with the "Google Vision API"
 
* **GestureDetector**: AI Edge Gesture Recognizer, A Google AI solution that uses machine learning to detect hands and recognize specific hand gestures in still images, video files, or live video streams.

* **Event system/Input Events**: You have **event handlers** and **event listeners**, event handlers can be defined/customized by either overriding it's methods in a custom view, for example to handle a click which is actually a series of of touch events(`onTouchEvent()` method). Knowing how to use input events we can manage our custom views scroll behaviour and customize things like panning, fling and drag(scrolling), using events we also can enable zooming in a custom view. An important API in detecting scroll, fling, and other gestures is the `Scroller` and `OverScroller`

* [How property animation differs from view animation](https://developer.android.com/develop/ui/views/animations/prop-animation#property-vs-view): In the view animation system if you animated a button to move across the screen, the button draws correctly, but the actual location where you can click the button does not change, so you have to implement your own logic to handle this. With the property animation system, these constraints are completely removed, and you can animate any property of any object (Views and non-Views) and the object itself is actually modified. The view animation system, however, takes less time to setup and requires less code to write.

* [`ViewPropertyAnimator` vs `ObjectAnimator`](https://android-developers.googleblog.com/2011/05/introducing-viewpropertyanimator.html): Here we can see that the first is a more performant way to do animations which is done by calling `animate()` on a view and then setting the properties we want to animate as if we were using a builder pattern


dispatchKeyEvent (KeyEvent event)
Dispatch a key event to the next view on the focus path. This path runs from the top of the view tree down to the currently focused view. If this view has focus, it will dispatch to itself. Otherwise it will dispatch the next node down the focus path. This method also fires any key listeners.

https://medium.com/androiddevelopers/unbundling-the-stable-windowmanager-a5471ff2907 windowlayoutinfo has a property called displayFeatures(FoldingFeature is the only DisplayFeature implementation)

Important subject that can be linked together are custom views and input events(event dispatching), 

