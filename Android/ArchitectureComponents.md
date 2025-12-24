# Views navigation

```
  getChildFragmentManager().addOnBackStackChangedListener();
  
  requireActivity().getOnBackPressedDispatcher().addCallback();
  
  NavHostFragment.findNavController(this);
  
  NavHostFragment.findNavController(this).getCurrentBackStackEntry().getSavedStateHandle().set();
  NavHostFragment.findNavController(this).getCurrentBackStackEntry().getSavedStateHandle().getLiveData();
  NavHostFragment.findNavController(this).getPreviousBackStackEntry().getSavedStateHandle().set();
  NavHostFragment.findNavController(this).getPreviousBackStackEntry().getSavedStateHandle().getLiveData();
  
  
  NavHostFragment navHostFragment = (NavHostFragment) getSupportFragmentManager()
          .findFragmentById(R.id.nav_host_fragment);
  
  NavController navController = navHostFragment.getNavController();
  NavGraph navGraph = navController.getNavInflater().inflate(R.navigation.bottom_nav_graph);
  navGraph.setStartDestination(R.id.shop);
  navController.setGraph(navGraph);
  NavigationUI.setupWithNavController(binding.bottomNavView, navController);
```

# Itent and Intent Filters
## [Check for unsafe intent launches](https://developer.android.com/guide/components/intents-filters#CheckForUnsafeIntentLaunches)
Configure your VmPolicy, with the below code. If your app targets Android 12 and uses the detectAll() method in its VmPolicy definition, the detectUnsafeIntentLaunch() method is called automatically.
```
fun onCreate() {
    StrictMode.setVmPolicy(VmPolicy.Builder()
        // Other StrictMode checks that you've previously added.
        // ...
        .detectUnsafeIntentLaunch()
        .penaltyLog()
        // Consider also adding penaltyDeath()
        .build())
}
```

you can check an activity will be resolved by an intent before launching it with the below code
```
if (sendIntent.resolveActivity(getPackageManager()) != null) {
    startActivity(chooser);
}
```

For all activities, you must declare your intent filters in the manifest file. However, filters for broadcast receivers can be registered dynamically by calling registerReceiver(). You can then unregister the receiver with unregisterReceiver(). Doing so allows your app to listen for specific broadcasts during only a specified period of time while your app is running.

In apps manifest you usually see the below tags, below you have an expalnation of what they do

* The ACTION_MAIN action indicates this is the main entry point and does not expect any intent data.

* The CATEGORY_LAUNCHER category indicates that this activity's icon should be placed in the system's app launcher. If the <activity> element does not specify an icon with icon, then the system uses the icon from the <application> element.

These two must be paired together in order for the activity to appear in the app launcher.

If your app targets Android 13 or higher, all intents originating from external apps are delivered to an exported component of your app only if that intent matches the actions and categories of an <intent-filter> element that your app declares. This behavior occurs regardless of the sending app's target SDK version.

In the following cases, intent matching isn't enforced:

* Intents delivered to components that don't declare any intent filters.
* Intents originating from within the same app.
* Intents originating from the system; that is, intents being sent from the "system UID" (uid=1000). System apps include system_server and apps that set android:sharedUserId to android.uid.system.
* Intents originating from root.

## Pending Intents
A PendingIntent object is a wrapper around an Intent object. The primary purpose of a PendingIntent is to grant permission to a foreign application to use the contained Intent as if it were executed from your app's own process.

Major use cases for a pending intent include the following:

* Declaring an intent to be executed when the user performs an action with your Notification (the Android system's NotificationManager executes the Intent).
* Declaring an intent to be executed when the user performs an action with your App Widget (the Home screen app executes the Intent).
* Declaring an intent to be executed at a specified future time (the Android system's AlarmManager executes the Intent).

You create pending intents with the below methods, note pending intents are not exectuded like intents do with functions like "startActivity", instead you must declare the intended component type when you create the PendingIntent by calling the respective creator method:

* PendingIntent.getActivity() for an Intent that starts an Activity.

* PendingIntent.getService() for an Intent that starts a Service.

* PendingIntent.getBroadcast() for an Intent that starts a BroadcastReceiver.


If your app targets Android 12 or higher, you must specify the mutability of each PendingIntent object that your app creates. To declare that a given PendingIntent object is mutable or immutable, use the PendingIntent.FLAG_MUTABLE or PendingIntent.FLAG_IMMUTABLE flag, respectively.

In most cases, your app should create immutable PendingIntent objects, as shown in the following code snippet. If a PendingIntent object is immutable, then other apps cannot modify the intent to adjust the result of invoking the intent.

However, certain use cases require mutable PendingIntent objects instead:

* Supporting direct reply actions in notifications. The direct reply requires a change to the clip data in the PendingIntent object that's associated with the reply. Usually, you request this change by passing FILL_IN_CLIP_DATA as a flag to the fillIn() method.
* Associating notifications with the Android Auto framework, using instances of CarAppExtender.
* Placing conversations in bubbles using instances of PendingIntent. A mutable PendingIntent object allows the system to apply the correct flags, such as FLAG_ACTIVITY_MULTIPLE_TASK and FLAG_ACTIVITY_NEW_DOCUMENT.
* Requesting device location information by calling requestLocationUpdates() or similar APIs. The mutable PendingIntent object allows the system to add intent extras that represent location lifecycle events. These events include a change in location and a provider becoming available.
* Scheduling alarms using AlarmManager. The mutable PendingIntent object allows the system to add the EXTRA_ALARM_COUNT intent extra. This extra represents the number of times that a repeating alarm has been triggered. By containing this extra, the intent can accurately notify an app as to whether a repeating alarm was triggered multiple times, such as when the device was asleep.

If your app creates a mutable PendingIntent object, it's strongly recommended that you use an explicit intent and fill in the ComponentName. That way, whenever another app invokes the PendingIntent and passes control back to your app, the same component in your app always starts.

### Use explicit intents within pending intents
To better define how other apps can use your app's pending intents, always wrap a pending intent around an explicit intent. To help follow this best practice, do the following:

* Check that the action, package, and component fields of the base intent are set.
* Use FLAG_IMMUTABLE, added in Android 6.0 (API level 23), to create pending intents. This flag prevents apps that receive a PendingIntent from filling in unpopulated properties. If your app's minSdkVersion is 22 or lower, you can provide safety and compatibility together by just checking if the SDK version is greater or equal to version 23(add flag) if lower jsut create the pending intent

In this document we also learn about **Intent resolution**. If an Intent does not specify an action, it passes the test as long as the filter contains at least one action.

For an intent to pass the category test, every category in the Intent must match a category in the filter. The reverse is not necessary.  Therefore, an intent with no categories always passes this test, regardless of what categories are declared in the filter.

ndroid automatically applies the CATEGORY_DEFAULT category to all implicit intents passed to startActivity() and startActivityForResult(). If you want your activity to receive implicit intents, it must include a category for "android.intent.category.DEFAULT" in its intent filters

queryIntentActivities() returns a list of all activities that can perform the intent passed as an argument, and queryIntentServices() returns a similar list of services. Neither method activates the components; they just list the ones that can respond. There's a similar method, queryBroadcastReceivers(), for broadcast receivers.

## [Package visibility filtering on Android](https://developer.android.com/training/package-visibility)

 ## A nice example
 Find it [here](https://android-developers.googleblog.com/2009/11/integrating-application-with-intents.html)
