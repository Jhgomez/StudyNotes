Android Worldwide 2023 notes can be found in  [concepts](concepts.rtf)

# Android Custom Lint
Lint is a static code analysis tool that checks your project source files for potential bugs and optimizations improvements for correctnes, security, performance, usability, accessibility.

The Android Lint API allows users to create cuxtom lint checks, this API can be used when writing server code using either Java or Kotlin

## How to use Android lints
1. in ADS automatically(on the fly, they are any warning or error displayed by the IDE automatically)
2. Run commands to run custom lint checks(press shift key twice and use the "Enter Inspection Name" dialog, not all of them are available by default since it could make compiling/running code way too slow becasue there are a lot of checks/rules) 
3. Get HTML or XML report from a lint analysis

## Getting the most out of Android Lint
1. Configuration - use "Inspection" tool to configure your lint in ADS. Use it to

    * Change scope of lint
    * Change severity of lint
    * Change the highlighting option of lint

2. Annotations - Lets provide hints to code inspection tools. To help detect more subtle code problems. Annotation Exapmles are
    * @NonNull, @Nullable (specific to Java)
    * @Require Permission(Manifest.Permission.SET_WALLPAPER)
    * @MainThread, @ UiThread, @WorkerThread @DrawableRes

3. Lint Internals - it can run analysis on
    * .java and .kt files since the analysis will run over the UAST(Universal Abstract Syntax Tree) that is generated from these type of files
    * .gradle files
    * .xml files

4. Writting Custom Lint Rules - Create a Java or Kotlin module specifically responsible to declare/run lint checks, add it them to the dependencies block of other modules. All these steps are listed in a medium article called "Custom Lint Check In Android Part 2"
    