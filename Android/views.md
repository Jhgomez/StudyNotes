
* public abstract class **Transition** / package androidx.transition: Subclasses are Autotransition, ChangeBounds, ChangeClipBounds, ChangeImageTransform, ChangeScroll, ChangeTransform, Explode, Fade, Hold,
  LavelMoveTransition, Slide, TextScale, TransitionSet, Visibility. Any Transition has two main jobs: (1) capture property values, and (2) play animations based on changes to captured property values. Transitions
  may not work correctly with either SurfaceView or TextureView, due to the way that these views are displayed on the screen. For SurfaceView, the problem is that the view is updated from a non-UI
  thread, so changes to the view due to transitions (such as moving and resizing the view) may be out of sync with the display inside those bounds. TextureView is more compatible with transitions in
  general, but some specific transitions (such as Fade) may not be compatible with TextureView because they rely on android.view.ViewOverlay functionality, which does not currently work
  with TextureView. Transitions can be declared in XML resource files inside the res/transition directory.

* public interface **TypeEvaluator<T>**/ package android.animation: nterface for use with the ValueAnimator.setEvaluator(TypeEvaluator) function. Evaluators allow developers to create animations on arbitrary
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
