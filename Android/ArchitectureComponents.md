Jetpack architecture components are viewmodel, lifecycleOwner, lifecycleObserver, room, LiveData, data binding, pagin, work manager. Android core architecture components are always the same 4, activity, content providers, broadcast receivers and services

# Source
Almost all(if not all) of the subjects we mention here can be found from google's [trainnig materials here](https://developer.android.com/develop#core-areas) and in the Android's documentation in the section "Design & Plan"

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

  navController.addOnDestinationChangedListener(new NavController.OnDestinationChangedListener() {
     @Override
     public void onDestinationChanged(@NonNull NavController controller,
             @NonNull NavDestination destination, @Nullable Bundle arguments) {
         if(destination.getId() == R.id.full_screen_destination) {
             toolbar.setVisibility(View.GONE);
             bottomNavigationView.setVisibility(View.GONE);
         } else {
             toolbar.setVisibility(View.VISIBLE);
             bottomNavigationView.setVisibility(View.VISIBLE);
         }

        // or you could add an argument to your fragment and use it like:
        boolean showAppBar = false;
        if (arguments != null) {
            showAppBar = arguments.getBoolean("ShowAppBar", false);
        }
        if(showAppBar) {
            appBar.setVisibility(View.VISIBLE);
        } else {
            appBar.setVisibility(View.GONE);
        }
     }
  });
```

## Lower Level APIs
### FragmentManager
Is responsible for performing actions on an app's fragments, such as adding, removing, or replacing them while managing the back stack also. Each activity is associated with its own fragment manager which manages the fragments displayed inside it(`getSupportFragmentManager()`), at the same time a fragment also has a reference to two instances of fragment manager, `childFragmentManager` and `parentFragmentManager`, the former handles fragments hosted inside it(fragment inside as fragment) and the later gives a reference to the parent fragment's fragment manager(if it is a fragment inside a fragment) or the activity's fragment manager(if fragment is direct child of the activity).

## High Level APIs
### Navigation Library/Navigation Component three main parts
* **Navigation Graph**
* **NavHost(NavHostFramgnet)**: Is the container for all navigation within a specific area of the app's UI. It is basically a view of type `Framgnet`(this is what was used previously) or `FragmentContainrView`(this is the preffered type now a days) by its own those views are just views but to make it a navhost you need to specify the properties `android:name="androidx.navigation.fragment.NavHostFragment"`, `app:defaultNavHost="true"` this one enables NavHost to intercept the system back button presses, and `app:navGraph="@navigation/nav_graph"`, you should be able to set these properties programatically also. Basically fragments are replaced in and out of this view. This is also associated with the activitys fragment manager, and at the same time it associates the `NavController` in it, this means you can find the nav host using the fragment manager and you can find the nav controller from the nav host.
* **NavController**: It is responsible for managing fragments within an Activity, it actually uses `FragmentManager` under the hood

## [Navigation best practices for multi-module projects](https://developer.android.com/guide/navigation/integrations/multi-module)
Since we're talking about modules/modularization and the UI layer(navigation code/logic lives in this layer) we will talk about feature modules, but that could mean different things depending on the context so, in this context a feature module is a module that encapsulates a distinct part of your application’s functionality. However, "feature module" is a term that is also used in the Play Feature Delivery describing a module that can be delivered conditionally or downloaded on-demand.

Feature modules are modules focused around one feature and provides a single navigation graph that encapsulates all of the destinations needed to implement that feature. Feature modules are included, either directly or indirectly, into your app module. The app module is responsible for providing the complete graph for your app and adding the NavHost to your UI. Use the `<include />` tag in your app module's to add the feature modules nav graphs to your main nav graph. After the main nav graph is created and compose by all other nav graphs in the feature modules you can create nav actions in the main nav graph. Common set of destinations, such as a login graph, should be added to your app module's navigation graph instead of each feature nav graph. Each feature module can then navigate across feature modules to navigate to those common destinations.

If your app's top-level destinations are composed of UI elements provided by feature modules, the app module is a natural place to put the top-level navigation and UI elements and when this is true you can use `NavigationUI` to tie destinations to menu items of a `BottomNavigationView` if the ID of the item matches the ID of a destination(you can match a graph's id or the id of a fragment in a graph), then you can let `NavigationUI` handle the `BottomNavigationView` navigation with the following code

```
 NavigationUI.setupWithNavController(bottomNav, navController);
```

it's generally bad practice for your app module to have a hard dependency on a specific destination embedded deeply within your feature modules' navigation graph. In most cases, you want your app module to know only about the entry point to any embedded or included navigation graphs (this applies outside of feature modules too). If you need to link to a destination deep within your library's navigation graph, the preferred way to do this is by using a deep link. Deep linking is also the only way for a library to navigate to a destination in another library's navigation graph.

Again, to navigate across independent/different feature modules use "Deep links", you can use either implicit or explicit deep links, the difference is when using implicit the back stack is not reset unlike explicit deep link navigation, where the back stack is replaced when navigating. Implicit use an URI and explicit use a pending intent.

It is strongly recommended to always use the default launchMode of `standard` in the declaration of the activity's in the manifest file when using Navigation. When using `standard` launch mode, Navigation automatically handles deep links by calling `handleDeepLink()` to process any explicit or implicit deep links within the Intent. However, this does not happen automatically if the Activity is re-used when using an alternate launchMode such as `singleTop`. In this case, it is necessary to manually call `handleDeepLink()` in `onNewIntent()`

## [NavigationUI](https://developer.android.com/guide/navigation/integrations/ui)
Contains static methods that manage navigation with the top app bar, the navigation drawer, and bottom navigation. Views that can be integrated with NavController are: TopAppBar/Toolbar/ ActionBar, CollapsingToolbarLayout, AppBarLayout, DrawerLayout with NavigationView, and BottomNavigationView. `NavigationUI` uses `NavController`'s callback/listener called `OnDestinationChangedListener` to make these common UI components navigation-aware.

With the top app bar `NavigationUI` uses the destination labels from your navigation graph to keep the title of the top app bar up-to-date.

```
AppBarConfiguration appBarConfiguration =
            new AppBarConfiguration.Builder(navController.getGraph()).build();
// or
AppBarConfiguration appBarConfiguration =
        new AppBarConfiguration.Builder(R.id.main, R.id.profile).build();

// or ir you want Navigation button to appear as an Up button for all destinations
// you may need the following set up if you need to navigate back to a previous activity from the top level destination fragment in other activity

AppBarConfiguration appBarConfiguration = new AppBarConfiguration.Builder()
        .setFallbackOnNavigateUpListener(::onSupportNavigateUp)
        .build();
    
NavigationUI.setupWithNavController(toolbar, navController, appBarConfiguration);

// for collapsing tool bars
NavigationUI.setupWithNavController(layout, toolbar, navController, appBarConfiguration);
```

Having a top app bar in the activity works well when the app bar's layout is similar in all destinations of the app. If, however, your top app bar changes across destinations, then consider removing the top app bar from the activity and instead you should define it in each destination fragment. This means you'd declare a `Toolbar` and possible variations with `AppBarLayout` accordingly in each fragment and then in the `onViewCreated` method link those views with the navigation controller with `NavigationUI.setupWithNavController`. This will result in the app bar animating with the rest of the layout during fragment transitions when a fragment transition is set.

We have seen how to set up the top app bar, but what about navigation drawers and bottom navigation, as we mentioned before we can also set up the nav controller with those views also, but first we need to know that under the hood they use a `menu` component and is that menu component which will helps us link and navigate to a destination in the nav graph. The secret is we should match the below ids

```
in the nav graph

<fragment android:id="@+id/matching_id"
       android:label="@string/details"
       android:name="com.example.android.myapp.DetailsFragment" />
```

```
In a menu, its item id has to match the destination we want to navigate to id
 <item
      android:id="@+id/matching_id"
      android:icon="@drawable/ic_details"
      android:title="@string/details" />
```

An alternative scenerario to link menu items and destination in the nav graph is when the menu was added via the Activity's `onCreateOptionsMenu()` or a fragments callback, then you need to do this

```
// from a fragment

@Override
public void onViewCreated(@NonNull View view, @Nullable Bundle savedInstanceState) {
    super.onViewCreated(view, savedInstanceState);

    // Get MenuHost from the activity
    MenuHost menuHost = requireActivity();

    // Add a MenuProvider tied to the fragment's lifecycle
    menuHost.addMenuProvider(new MenuProvider() {
        @Override
        public void onCreateMenu(@NonNull Menu menu, @NonNull MenuInflater menuInflater) {
            menuInflater.inflate(R.menu.my_fragment_menu, menu);
        }

        @Override
        public boolean onMenuItemSelected(@NonNull MenuItem menuItem) {
            NavController navController = Navigation.findNavController(this, R.id.nav_host_fragment);

            return NavigationUI.onNavDestinationSelected(item, navController) || super.onMenuItemSelected(item);
        }
    }, getViewLifecycleOwner(), Lifecycle.State.RESUMED);
}


// from an Activity
@Override
public boolean onCreateOptionsMenu(Menu menu) {
    MenuInflater inflater = getMenuInflater();
    inflater.inflate(R.menu.game_menu, menu);
    return true;
}

@Override
public boolean onOptionsItemSelected(MenuItem item) {
    NavController navController = Navigation.findNavController(this, R.id.nav_host_fragment);
    return NavigationUI.onNavDestinationSelected(item, navController)
            || super.onOptionsItemSelected(item);
}
```

After these values match then, for a drawer, first create the views, usually you would create a `DrawerLayout` inside it you have two items, `FragmentContainerView` and `NavigationView`(this is the actual drawer), then connect/link your drawer to your nav graph with

```
AppBarConfiguration appBarConfiguration =
        new AppBarConfiguration.Builder(navController.getGraph())
            .setDrawerLayout(drawerLayout)
            .build();

NavHostFragment navHostFragment = supportFragmentManager.findFragmentById(R.id.nav_host_fragment);
NavController navController = navHostFragment.getNavController();
NavigationView navView = findViewById(R.id.nav_view);
NavigationUI.setupWithNavController(navView, navController);
```

After you do this, the top app bar helpers automatically transition between the drawer icon and the Up icon as the current destination changes. You don't need to use ActionBarDrawerToggle. Remember to link your menu items to the destinations in the graph as explained above.

The last view we could configure with the graph is `BottomNavigationView`, so first, just add it to xml, then just do the following, and remember to link the menu items with the destinations in the nav graph as described above

```
NavHostFragment navHostFragment = supportFragmentManager.findFragmentById(R.id.nav_host_fragment);
    NavController navController = navHostFragment.getNavController();
    BottomNavigationView bottomNav = findViewById(R.id.bottom_nav);
    NavigationUI.setupWithNavController(bottomNav, navController);
```

# Itent and Intent Filters
Using an implicit intent to start a service is a security hazard

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
 There are three fundamental ways to save data on the device:

* Internal storage
* External storage
* Content providers

 Android's file system provide the following types of storage to save your app data

* App-specific storage: Store files that are meant for your app's use only, either in dedicated directories within an internal storage volume or different dedicated directories within external storage. Use the directories within internal storage to save sensitive information that other apps shouldn't access.
* Shared storage: Store files that your app intends to share with other apps, including media, documents, and other files. consider using a content provider instead, which offers read and write permissions to other apps and can make dynamic permission grants on a case-by-case basis, this means you can use the app specific storage option and make it "public" through a content provider for control on who and when can access.
* Preferences: Store private, primitive data in key-value pairs.
* Databases: Store structured data in a private database using the Room persistence library.

The characteristics of these options are summarized in the following table:

|  | Type of content | Access method | Permissions needed |	Can other apps access? | Files removed on app uninstall? |
|--| --------------- | ------------- | ------------------ | ---------------------- | ------------------------------- |
| App-specific files |	Files meant for your app's use only |	From internal storage, `getFilesDir()` or `getCacheDir()`. From external storage, `getExternalFilesDir()` or `getExternalCacheDir()` | Never needed for internal storage. Not needed for external storage when your app is used on devices that run Android 4.4 (API level 19) or higher| No |	Yes |
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

* [Access and store files](https://developer.android.com/training/data-storage/app-specific#internal-access-store-files)
* [Create Cache Files](https://developer.android.com/training/data-storage/app-specific#internal-create-cache):  cache directory is designed to store a small amount of your app's sensitive data. To determine how much cache space is currently available for your app, call `getCacheQuotaBytes()`. You should always maintain your app's cache files within internal storage.
* [Remove cache files](https://developer.android.com/training/data-storage/app-specific#internal-remove-cache)

### External Storage
On Android 4.4 (API level 19) or higher, your app doesn't need to request any storage-related permissions to access app-specific directories within external storage.

On devices that run Android 9 (API level 28) or lower, your app can access the app-specific files that belong to other apps, provided that your app has the appropriate storage permissions. apps that target Android 10 (API level 29) and higher are given scoped access into external storage, or scoped storage, by default. When scoped storage is enabled, apps cannot access the app-specific directories that belong to other apps.

 Don't store executables or class files on external storage prior to dynamic loading. If your app does retrieve executable files from external storage, make sure the files are signed and cryptographically verified prior to dynamic loading(taken from "security checklist" documentation).

#### Verify that Storage is Available
Verify that the volume is accessible before trying to read app-specific data from, or write app-specific data to, external storage.

```
// Checks if a volume containing external storage is available
// for read and write.
private boolean isExternalStorageWritable() {
    return Environment.getExternalStorageState().equals(Environment.MEDIA_MOUNTED);
}

// Checks if a volume containing external storage is available to at least read.
private boolean isExternalStorageReadable() {
     return Environment.getExternalStorageState().equals(Environment.MEDIA_MOUNTED) ||
            Environment.getExternalStorageState().equals(Environment.MEDIA_MOUNTED_READ_ONLY);
}
```

On devices without removable external storage, use the following command to enable a virtual volume for testing your external storage availability logic:

```
adb shell sm set-virtual-disk true
```

There can be more than one external storage unit and even an external storage can be created from a partition in the local storage, so to access the right external storage unit/partition, use the below code
```
File[] externalStorageVolumes =
        ContextCompat.getExternalFilesDirs(getApplicationContext(), null);
File primaryExternalStorage = externalStorageVolumes[0];
```

Chek more:
* [Access persistent files](https://developer.android.com/training/data-storage/app-specific#external-access-files)
* [Create Cache Files](https://developer.android.com/training/data-storage/app-specific#external-cache-create)
* [Remove Cache Files](https://developer.android.com/training/data-storage/app-specific#external-cache-remove)

#### Media content
If your app works with media files that provide value to the user only within your app, it's best to store them in app-specific directories within external storage
```
@Nullable
File getAppSpecificAlbumStorageDir(Context context, String albumName) {
    // Get the pictures directory that's inside the app-specific directory on
    // external storage.
    File file = new File(context.getExternalFilesDir(
            Environment.DIRECTORY_PICTURES), albumName);
    if (file == null || !file.mkdirs()) {
        Log.e(LOG_TAG, "Directory not created");
    }
    return file;
}
```

It's important that you use directory names provided by API constants like DIRECTORY_PICTURES. These directory names ensure that the files are treated properly by the system. If none of the pre-defined sub-directory names suit your files, you can instead pass null into getExternalFilesDir(). This returns the root app-specific directory within external storage.


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

    // You can also calculate devices available space with
    // StorageStatsManager.getFreeBytes() / StorageStatsManager.getTotalBytes()
}
```

You can write the file right away(without checking available space), then catch an IOException if one occurs. You may need to do this if you don't know exactly how much space you need, like when changing an image from PNG to JPG before storing it

### Create a storage management activity
You can declare a custom "manage space" activity using the `android:manageSpaceActivity` attribute in the manifest file. File manager apps can invoke this activity even when your app doesn't export the activity; that is, when your activity sets `android:exported` to false.

## Shared Storage(The opposite of app-specific storage)
Android provides APIs for storing and accessing the following types of shareable data:

* **Media content**: The system provides standard public directories for these kinds of files, so the user has a common location for all their photos, another common location for all their music and audio files, and so on. Your app can access this content using the platform's `MediaStore API`.
* **Documents and other files**: The system has a special directory for containing other file types, such as PDF documents and books that use the EPUB format. Your app can access these files using the platform's Storage Access Framework. If your app wants to access a file within the MediaStore.Downloads collection that your app didn't create, you must use that Storage Access Framework
* [Datasets](https://developer.android.com/training/data-storage/shared/datasets): On Android 11 (API level 30) and higher, the system caches large datasets that multiple apps might use. These datasets can support use cases like machine learning and media playback. Apps can access these shared datasets using the `BlobStoreManager` API.

### Media
App attribution of media files
When scoped storage is enabled for an app that targets Android 10 or higher, the system attributes an app to each media file, which determines the files that your app can access when it hasn't requested any storage permissions. Each file can be attributed to only one app. Therefore, if your app creates a media file that's stored in the photos, videos, or audio files media collection, your app has access to the file.

If the user uninstalls and reinstalls your app, however, you must request READ_EXTERNAL_STORAGE to access the files that your app originally created. This permission request is required because the system considers the file to be attributed to the previously installed version of the app, rather than the newly installed one.

If your app works with media files that provide value to the user only within your app, it's best to store them in app-specific directories within external storage.

### Storage volumes
Apps that target Android 10 or higher can access the unique name that the system assigns to each external storage volume. This naming system helps you efficiently organize and index content, and it gives you control over where new media files are stored.

The following volumes are particularly useful to keep in mind:

* **VOLUME_EXTERNAL** volume provides a view of all shared storage volumes on the device. You can read the contents of this synthetic volume, but you cannot modify the contents.
* **VOLUME_EXTERNAL_PRIMARY** volume represents the primary shared storage volume on the device. You can read and modify the contents of this volume.

### [Location where media was captured](https://developer.android.com/training/data-storage/shared/media#location-media-captured)
Some photographs and videos contain location information in their metadata, which shows the place where a photograph was taken or where a video was recorded.

How you access this location information in your app depends on whether you need to access location information for a photograph or for a video.

### [Update in native code](https://developer.android.com/training/data-storage/shared/media#update-native-code)
If you need to write media files using native libraries, pass the file's associated file descriptor from your Java-based or Kotlin-based code into your native code.

### Use cases that require an alternative to media store

#### Working with other types of files
If your app works with documents and files that don't exclusively contain media content, such as files that use the EPUB or PDF file extension, use the ACTION_OPEN_DOCUMENT intent action, as described in the guide to storing and accessing documents and other files.

#### File sharing in companion apps
In cases where you provide a suite of companion apps, such as a messaging app and a profile app, set up file sharing using content:// URIs. We also recommend this workflow as a security best practice

## Access documents and other files from shared storage(Storage Access Framework)
This is the "Storage Access Framework" we have mentioned a few times before in this document. On devices that run Android 4.4 (API level 19) and higher, your app can interact with a documents provider, including external storage volumes and cloud-based storage, using the Storage Access Framework. This framework allows users to interact with a system picker to choose a documents provider and select specific documents and other files for your app to create, open, or modify.

Because the user is involved in selecting the files or directories that your app can access, this mechanism doesn't require any system permissions, and user control and privacy is enhanced. Additionally, these files, which are stored outside of an app-specific directory and outside of the media store, remain on the device after your app is uninstalled.

Using the framework involves the following steps:

1. An app invokes an intent that contains a storage-related action. This action corresponds to a specific use case that the framework makes available.
2. The user sees a system picker, allowing them to browse a documents provider and choose a location or document where the storage-related action takes place.
3. The app gains read and write access to a URI that represents the user's chosen location or document. Using this URI, the app can perform operations on the chosen location.

### Use cases for accessing documents and other files
The Storage Access Framework supports the following use cases for accessing files and other documents.

* Create a new file: The ACTION_CREATE_DOCUMENT intent action allows users to save a file in a specific location.
* Open a document or file: The ACTION_OPEN_DOCUMENT intent action allows users to select a specific document or file to open.
* Grant access to a directory's contents: The ACTION_OPEN_DOCUMENT_TREE intent action, available on Android 5.0 (API level 21) and higher, allows users to select a specific directory, granting your app access to all of the files and sub-directories within that directory.

## [Send simple data to other apps](https://developer.android.com/training/sharing/send)
Android uses intents and their associated extras to let users share information quickly and easily using their favorite apps.

Android provides two ways for users to share data between apps:

The Android Sharesheet is primarily designed for sending content outside your app and/or directly to another user. For example, sharing a URL with a friend.
The Android intent resolver is best suited for passing data to the next stage of a well-defined task. For example, opening a PDF from your app and letting users pick their preferred viewer.

## [Receive simple data from other apps](https://developer.android.com/training/sharing/receive)
Users of other apps frequently send data to your app through the Android Sharesheet or the intent resolver. Apps that send data to your app must set a MIME type for that data. Your app can receive data sent by another app in the following ways:

* An Activity with a matching intent-filter tag in the manifest
* [Sharing Shortcuts/Share Targets](https://developer.android.com/training/sharing/direct-share-targets) published by your app.
  
Direct Share targets are deep links into a specific Activity within your app. They often represent a person or a group, and the Android Sharesheet shows them. For example, a messaging app can provide a Direct Share target for a person that deep links directly into a conversation with that person. See Provide Direct Share targets for detailed instructions.

## [Sharing files](https://developer.android.com/training/secure-file-sharing)
Apps often have a need to offer one or more of their files to another app. For example, an image gallery may want to offer files to image editors, or a file management app may want to allow users to copy and paste files between areas in external storage. One way a sending app can share a file is to respond to a request from the receiving app.

You can securely share files from your app to another app using content URIs generated by the Android FileProvider component and temporary permissions that you grant to the receiving app for the content URI.

## [Printing FIles](https://developer.android.com/training/printing)
Android users frequently view content solely on their devices, but there are times when showing someone a screen is not an adequate way to share information. Being able to print information from your Android application gives users a way to see a larger version of the content from your app or share it with another person who is not using your application. Printing also allows them to create a snapshot of information that does not depend on having a device, sufficient battery power, or a wireless network connection.

In Android 4.4 (API level 19) and higher, the framework provides services for printing images and documents directly from Android applications. You can enable printing in your application, including printing images, HTML pages and creating custom documents for printing.

## Content Providers
Help an application manage access to data stored by itself or stored by other apps and provide a way to share data with other apps. They encapsulate the data and provide mechanisms for defining data security. Content providers are the standard interface that connects data in one process with code running in another process. you can configure a content provider to let other applications securely access and modify your app data. They provide an abstraction that lets you make modifications to your application data storage implementation without affecting other applications that rely on access to your data. They often provides its own UI for working with the data. They are primarily used by other applications, which access the provider using a provider client object. Together, providers and provider clients offer a consistent, standard interface to data that also handles interprocess communication and secure data access. Typically you use them in either of the following two ways, to access an existing content provider in another application or creating a new content provider in your application to share data with other applications.

A number of other classes rely on the ContentProvider class:

* AbstractThreadedSyncAdapter
* CursorAdapter
* CursorLoader: this one was implemented using the [Loaders](https://developer.android.com/guide/components/loaders) but it seems that after android 9/API level 28 they where deprecated

Some use cases of content providers are:
* To implement custom search suggestions in your application.
* To expose your application data to widgets/Sending data to a widget
* To copy and paste complex data or files from your application to other applications.
* Sharing access to your application data with other applications
* Returning custom search suggestions for your application through the search framework using `SearchRecentSuggestionsProvider`
* Synchronizing application data with your server using an implementation of `AbstractThreadedSyncAdapter`

The Android framework includes content providers that manage data such as audio, video, images, and personal contact information. You can see some of them listed in the reference documentation for the android.provider package.

A content provider can be used to manage access to a variety of data storage sources, including both structured data, such as a SQLite relational database, or unstructured data such as image files.

If you are using a content provider for sharing data between only your own apps, we recommend using the android:protectionLevel attribute set to signature protection. Signature permissions don't require user confirmation, so they provide a better user experience and more controlled access to the content provider data when the apps accessing the data are signed with the same key. You can also set more granular access by declaring the android:grantUriPermissions attribute and using the FLAG_GRANT_READ_URI_PERMISSION and FLAG_GRANT_WRITE_URI_PERMISSION flags in the Intent object that activates the component. The scope of these permissions can be further limited by the <grant-uri-permission> element.

## Example(Content Provider)
Use `ContentResolver` object in your application's Context to communicate with the provider as a client. A provider object(class implementing `ContentProvider`) receives data requests from clients, performs the requested action, and returns the results. This object has methods that call identically named methods in the provider object, an instance of one of the concrete subclasses of ContentProvider. The ContentResolver methods provide the basic "CRUD" (create, retrieve, update, and delete) functions of persistent storage.

To access a provider, your application usually has to request specific permissions in its manifest file.

I will not give a detail example but will describe the actions needed to implement one.

As mentioned we need a provider that acts similar to a server in the sense that clients(ContentResolvers) communicate with them and also usually the clients will be other apps. Content providers are basically an interface the clients use to save, read and modify data, to do this you can store info in any way you want but usually that may be a relational local database or files on the side of the content provided(server), a local DB would be preffered if you need complex objects, and for files like picture, documents, you store and retrieve them as files usually from your private scoped local storage. However the content provider interface is similar to querying from a database and when you implement it you'll override methods for querying, insert, delete, update and when a client interacts with the provider it will be returned a `Cursor` object when reading which will let you iterate over the matches found from perfoming the query.

You will also need to define the provider's authority string, content URIs, and column names(or file names). If you want the provider's application to handle intents, also define intent actions, extras data, and flags. Also define the permissions that you require for applications that want to access your data. Consider defining all these values as constants in a separate contract class. Later, you can expose this class to other developer.

# Services
Services can also be protected using the `android:permission` attribute. By doing so, other applications need to declare a corresponding `<uses-permission>` element in their own manifest to be able to start, stop, or bind to the service. You can get the same behavior at rutning with the function `checkCallingPermission()` before executing the implementation of the call, however, it's recommend using the declarative permissions in the manifest, since those are less prone to oversight.

# Security

## [Play Integrity API](https://developer.android.com/google/play/integrity/overview)
helps you check that user actions and server requests are coming from your genuine app, installed by Google Play, running on a genuine and certified Android device. 

# Interprocess Communication
Some apps attempt to implement IPC using traditional Linux techniques such as network sockets and shared files. However, we recommend instead that you use Android system functionality for IPC such as Intent, Binder or Messenger with a Service, and BroadcastReceiver.

## Binder and Messenger interfaces(taken from "security checklist")
Using Binder or Messenger is the preferred mechanism for RPC style IPC on Android. They provide well-defined interfaces that enable mutual authentication of the endpoints, if required.

We recommend that you design your app interfaces in a way that doesn't require interface-specific permission checks. Binder and Messenger objects aren't declared within the application manifest, and therefore you can't apply declarative permissions directly to them. They generally inherit permissions declared in the application manifest for the Service or Activity within which they are implemented. If you are creating an interface that requires authentication and/or access controls, you must explicitly add those controls as code in the Binder or Messenger interface.

# Extras

## Sync adapter framework/AbstractThreadedSyncAdapter
Is designed to facilitate the synchronization of data between a device and a remote server. It allows apps to manage data updates seamlessly, ensuring that users have access to the most current information without manual intervention. This framework is particularly useful for applications that require regular updates from a server, such as email clients, social media apps, and news aggregators.

Be aware one of their requirements would be to implement a content provider, but in case you're already storing local data in another form you can [create a stub content provider](https://developer.android.com/training/sync-adapters/creating-stub-provider).

## Security in a virtual machine
Dalvik is Android's runtime virtual machine (VM). 

there are two broad issues that might be different about writing apps for Android:

* Some virtual machines, such as the JVM or .NET runtime, act as a security boundary, isolating code from the underlying operating system capabilities. On Android, the Dalvik VM is not a security boundary—the application sandbox is implemented at the OS level, so Dalvik can interoperate with native code in the same application without any security constraints.


* Given the limited storage on mobile devices, it's common for developers to want to build modular applications and use dynamic class loading. When doing this, consider both the source where you retrieve your application logic and where you store it locally. Don't use dynamic class loading from sources that aren't verified, such as unsecured network sources or external storage, because that code might be modified to include malicious behavior.

## Things That Can Not Change
manifest package name is the certificate that application is signed with. The signing certificate represents the author of the application. If you change the certificate an application is signed with, it is now a different application because it comes from a different author. This different application can’t be uploaded to Market as an update to the original application, nor can it be installed onto a device as an update. Info taken from [Dianne's Hackborn article](https://android-developers.googleblog.com/2011/06/things-that-cannot-change.html)

Dynamic vs Static Broadcast Receivers


