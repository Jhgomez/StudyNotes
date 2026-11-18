# [Create and edit run/debug configurations](https://developer.android.com/studio/run/rundebugconfig)
Here we are explained how configurations that are used to run(application and testst) and debug(application and test) in Android Studio. A very interesting feature 
they explain here is code coverage, we can use it by default in AS because it is enable by default, this feature lets us see what lines of code where executed and
which line where not

# Tips

* To know if a build is a debug build in the app module you can enable build config and use `BuildConfig.DEBUG`, in a library module you should use
  `(context.applicationInfo.flags and ApplicationInfo.FLAG_DEBUGGABLE) != 0`, this is because in a library module the `DEBUG` flag will always be false
