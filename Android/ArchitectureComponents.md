# Source
Almost all(if not all) of the subjects we mention here can be found from google's [trainnig materials here](https://developer.android.com/develop#core-areas)

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

 # Storage
 Android's file system provide the following types of storage to save your app data

* App-specific storage: Store files that are meant for your app's use only, either in dedicated directories within an internal storage volume or different dedicated directories within external storage. Use the directories within internal storage to save sensitive information that other apps shouldn't access.
* Shared storage: Store files that your app intends to share with other apps, including media, documents, and other files.
* Preferences: Store private, primitive data in key-value pairs.
* Databases: Store structured data in a private database using the Room persistence library.

The characteristics of these options are summarized in the following table:

|  | Type of content | Access method | Permissions needed |	Can other apps access? | Files removed on app uninstall? |
|--| --------------- | ------------- | ------------------ | ---------------------- | ------------------------------- |
| App-specific files |	Files meant for your app's use only |	From internal\nstorage, `getFilesDir()` or `getCacheDir()`. From external storage, `getExternalFilesDir()` or `getExternalCacheDir()` | Never needed for internal storage. Not needed for external storage when your app is used on devices that run Android 4.4 (API level 19) or higher| No |	Yes |
| Media |	Shareable media files (images, audio files, videos) |	`MediaStore` API | `READ_EXTERNAL_STORAGE` when accessing other apps' files on Android 11 (API level 30) or higher. `READ_EXTERNAL_STORAGE` or` WRITE_EXTERNAL_STORAGE` when accessing other apps' files on Android 10 (API level 29). Permissions are required for all files on Android 9 (API level 28) or lower | Yes, though the other app needs the `READ_EXTERNAL_STORAGE` permission | No |
| Documents and other files |	Other types of shareable content, including downloaded files | Storage Access Framework	| None | Yes, through the system file picker | No |
| App preferences |	Key-value pairs |	Jetpack Preferences library |	None | No |	Yes |
| Database | Structured data | Room persistence library |	None | No | Yes |

If your app's basic functionality requires certain data, such as when your app is starting up, place the data within internal storage directory or a database. App-specific files that are stored in external storage aren't always accessible because some devices allow users to remove a physical device that corresponds to external storage.

## Cateogries of Storage Locations
Android provides two types of physical storage locations: internal storage and external storage.

Android represents external storage devices using a path, however the exact location of where your files can be saved might vary across devices. For this reason, don't use hard-coded file paths. To avoid accidental disclosure of information, don't use predictable patterns to filenames in ways that could reveal the kinds of information found within a file.

Apps themselves are stored within internal storage by default. If your APK size is very large, however, you can indicate a preference within your app's manifest file to install your app on external storage instead:

```
<manifest ...
  android:installLocation="preferExternal">
  ...
</manifest>
```
## Permissions and access to external storage
Android defines the following storage-related permissions: `READ_EXTERNAL_STORAGE`, `WRITE_EXTERNAL_STORAGE`, and `MANAGE_EXTERNAL_STORAGE`.

The approach to access to storage in Android has changed, previously you had to declare the permissions to read write any file outside the app-specific directories on external storage. More recent versions of Android rely more on a file's purpose than its location for determining an app's ability to access, and write to, a given file. In particular, if your app targets Android 11 (API level 30) or higher, the WRITE_EXTERNAL_STORAGE permission doesn't have any effect on your app's access to storage.

Android 11 introduces the `MANAGE_EXTERNAL_STORAGE` permission, which provides write access to files outside the app-specific directory and `MediaStore`. Most apps doesn't actually need this permission but if you need it then search for a guide on how to manage all files on a storage device.

Apps that target Android 10 (API level 29) and higher are given scoped access into external storage, or scoped storage, by default, this means they only have access to the app-specific directory on external storage, as well as specific types of media that the app has created.

Check the [storage use cases and best practices](https://developer.android.com/training/data-storage/use-cases) guide for examples.

## Viewing Your App Files in AS
Use the Android Studio's `Device Explorer` for exploring a device's files, the following directories are particularly useful:

* `data/data/<app_name>/`: Contains data files for your app stored on internal storage.
* `sdcard/`: Contains user files stored on external user storage (pictures, etc.).

## Access app-specific files
You can store(read/write) your app's specific files in the following locations:

* **Internal storage directories**: These directories include both a dedicated location for storing persistent files, and another location for storing cache data. On Android 10 (API level 29) and higher, these locations are encrypted. No other app can access this files
* **External storage directories**: Has two locations as the internal storage, a location for persisten files and another for cache data, the difference is that is not encypted and it's possible for other apps to access these files if they have the propper permissions, however the files store on those locations are meant to be used by your app only. If you want to share files then store them in the shared storage part of the external storage

When the user uninstalls your app, the files saved in app-specific storage are removed. 

### Internal storage
Internal directories tend to be small. Before writing app-specific files to internal storage, your app should [query the free](#quer-free-space) space on the device.

## Query Free Space
```
// in this example the App needs 10 MB within internal storage.
private static final long NUM_BYTES_NEEDED_FOR_MY_APP = 1024 * 1024 * 10L;

StorageManager storageManager =
        getApplicationContext().getSystemService(StorageManager.class);
UUID appSpecificInternalDirUuid = storageManager.getUuidForPath(getFilesDir());
long availableBytes =
        storageManager.getAllocatableBytes(appSpecificInternalDirUuid);
if (availableBytes >= NUM_BYTES_NEEDED_FOR_MY_APP) {
    storageManager.allocateBytes(
            appSpecificInternalDirUuid, NUM_BYTES_NEEDED_FOR_MY_APP);
} else {
    // this means the storage space availalbe in the user's device is not enough
    // so we give the option to free space by clearing cache or removing files from its local unit

    // To request that the user remove all app cache files instead, set
    // "action" to ACTION_CLEAR_APP_CACHE.
    Intent storageIntent = new Intent();
    storageIntent.setAction(ACTION_MANAGE_STORAGE);
}
```
