{\rtf1\ansi\ansicpg1252\cocoartf2759
\cocoatextscaling0\cocoaplatform0{\fonttbl\f0\fswiss\fcharset0 Helvetica;}
{\colortbl;\red255\green255\blue255;\red191\green191\blue191;\red251\green0\blue19;\red251\green0\blue7;
\red251\green0\blue28;\red35\green255\blue10;\red103\green79\blue12;\red6\green0\blue8;\red168\green135\blue5;
\red206\green0\blue19;\red34\green255\blue6;\red1\green23\blue6;\red251\green0\blue7;\red251\green0\blue48;
\red34\green255\blue11;\red9\green0\blue7;\red34\green255\blue28;\red251\green0\blue12;\red24\green51\blue255;
\red10\green1\blue15;\red24\green33\blue255;}
{\*\expandedcolortbl;;\csgray\c79525;\cssrgb\c100000\c0\c8125;\cssrgb\c100000\c841\c0;
\cssrgb\c100000\c0\c13888;\cssrgb\c1630\c100000\c1630;\cssrgb\c48268\c37765\c4782;\cssrgb\c1826\c200\c2454;\cssrgb\c72041\c59218\c0;
\cssrgb\c85351\c0\c8517;\cssrgb\c0\c100000\c0;\cssrgb\c0\c11696\c2002;\cssrgb\c100000\c0\c0;\cssrgb\c100000\c0\c24490;
\cssrgb\c0\c100000\c2883;\cssrgb\c3197\c139\c2360;\cssrgb\c0\c100000\c13754;\cssrgb\c100000\c0\c3335;\cssrgb\c12776\c32420\c100000;
\cssrgb\c4022\c614\c7012;\cssrgb\c12885\c26291\c100000;}
\margl1440\margr1440\vieww30040\viewh17760\viewkind0
\pard\tx720\tx1440\tx2160\tx2880\tx3600\tx4320\tx5040\tx5760\tx6480\tx7200\tx7920\tx8640\pardirnatural\partightenfactor0

\f0\fs24 \cf0 Do that\
Android Dev Summit 20222\
\
\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\
Locale and Media Picker\
\
Make apps dynamically select its language with per app language preferences.\
\
We can now use the Photo Picker to select media from the phone\
\
\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\
\
Custom Modifiers\
\
Use ParentDataModifier to pass information from child to parent composables, this will mostly be used in custom layouts, this is possible after \
creating a class that extends/implements the class previously mentioned and then the information in its constructor and return a reference to\
 the instance through the function that can be overiden and then creating a Modifier extension function that accepts the object we mentioned first.\
\
\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\
\
Compose phases\
\
A composable has three phases, \
	1. Composition: Creates the node tree, basically a description of the the UI\
	2. Layout: Where to place the composables, it consists of two steps measurement and placement\
	3. Drawing: The tree is rendered in using the measure and placement information\
\
\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\
\
Drawing in Compose\
\
In compose you draw using modifiers, it is possible to draw text on the canvas that you access through the modifiers\
\
\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\
\
Animations in compose\
\
You can create size animations using a \'93mutableState\'94 variable that will be wrapped in a \'93updateTransition\'94 function which will return an object \
and from which we can call another function called \'93animateDp\'94, but there is other APIs to animate like \'93AnimateAsSate\'94, \'93Animatable\'94 and \'93Transition\'94\
\
\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\
\
AGSL\
\
Android Graphics Shading Language is used to make animated shades. They are easily incorporated in draw scope. It is based on GLSL(OpenGL). It \
Runs on Android T+. They run on GPU so they are very efficient(parallel pixel calculations)\
\
\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\
\
Use Shaders Previously\
\
Before AGSL in order to use shaders on Android you needed  a surface view with OpenGL\
\
\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\
\
Baseline Profiles\
\
	Android Code Execution Evolution\
	Some of the history/background of how google used to optimize apps, performance or execution is evaluated in three dimensions, initial \
	performance(performance after install and/or after app start), eventual performance(performance after the runtime has a chance to discover \
	some hot paths), disk size(cost of the optimizations in terms of disk space required)\
\
\

\itap1\trowd \taflags1 \trgaph108\trleft-108 \trbrdrt\brdrnil \trbrdrl\brdrnil \trbrdrr\brdrnil 
\clvertalc \clshdrawnil \clheight20 \clbrdrt\brdrs\brdrw20\brdrcf2 \clbrdrl\brdrs\brdrw20\brdrcf2 \clbrdrb\brdrs\brdrw20\brdrcf2 \clbrdrr\brdrs\brdrw20\brdrcf2 \clpadl100 \clpadr100 \gaph\cellx1440
\clvertalc \clshdrawnil \clheight20 \clbrdrt\brdrs\brdrw20\brdrcf2 \clbrdrl\brdrs\brdrw20\brdrcf2 \clbrdrb\brdrs\brdrw20\brdrcf2 \clbrdrr\brdrs\brdrw20\brdrcf2 \clpadl100 \clpadr100 \gaph\cellx2880
\clvertalc \clshdrawnil \clheight20 \clbrdrt\brdrs\brdrw20\brdrcf2 \clbrdrl\brdrs\brdrw20\brdrcf2 \clbrdrb\brdrs\brdrw20\brdrcf2 \clbrdrr\brdrs\brdrw20\brdrcf2 \clpadl100 \clpadr100 \gaph\cellx4320
\clvertalc \clshdrawnil \clheight20 \clbrdrt\brdrs\brdrw20\brdrcf2 \clbrdrl\brdrs\brdrw20\brdrcf2 \clbrdrb\brdrs\brdrw20\brdrcf2 \clbrdrr\brdrs\brdrw20\brdrcf2 \clpadl100 \clpadr100 \gaph\cellx5760
\clvertalc \clshdrawnil \clheight20 \clbrdrt\brdrs\brdrw20\brdrcf2 \clbrdrl\brdrs\brdrw20\brdrcf2 \clbrdrb\brdrs\brdrw20\brdrcf2 \clbrdrr\brdrs\brdrw20\brdrcf2 \clpadl100 \clpadr100 \gaph\cellx7200
\clvertalc \clshdrawnil \clheight20 \clbrdrt\brdrs\brdrw20\brdrcf2 \clbrdrl\brdrs\brdrw20\brdrcf2 \clbrdrb\brdrs\brdrw20\brdrcf2 \clbrdrr\brdrs\brdrw20\brdrcf2 \clpadl100 \clpadr100 \gaph\cellx8640
\pard\intbl\itap1\tx720\tx1440\tx2160\tx2880\tx3600\tx4320\tx5040\tx5760\tx6480\tx7200\tx7920\tx8640\pardirnatural\qc\partightenfactor0
\cf0 \
\cell 
\pard\intbl\itap1\tx720\tx1440\tx2160\tx2880\tx3600\tx4320\tx5040\tx5760\tx6480\tx7200\tx7920\tx8640\pardirnatural\qc\partightenfactor0
\cf0 Android 1.0\cell 
\pard\intbl\itap1\tx720\tx1440\tx2160\tx2880\tx3600\tx4320\tx5040\tx5760\tx6480\tx7200\tx7920\tx8640\pardirnatural\qc\partightenfactor0
\cf0 Android 2.2 Froys\
Introduced Just-in-TIme complier(JIT)\cell 
\pard\intbl\itap1\tx720\tx1440\tx2160\tx2880\tx3600\tx4320\tx5040\tx5760\tx6480\tx7200\tx7920\tx8640\pardirnatural\qc\partightenfactor0
\cf0 Android 5.0 Lollipop\
Introduced full AOT\cell 
\pard\intbl\itap1\tx720\tx1440\tx2160\tx2880\tx3600\tx4320\tx5040\tx5760\tx6480\tx7200\tx7920\tx8640\pardirnatural\qc\partightenfactor0
\cf0 Android 7.0 Nougat\
Hybrid between JIT and finding hot paths(important parts of app) so PGO(Profile-guided optimization) was used\cell 
\pard\intbl\itap1\tx720\tx1440\tx2160\tx2880\tx3600\tx4320\tx5040\tx5760\tx6480\tx7200\tx7920\tx8640\pardirnatural\qc\partightenfactor0
\cf0 Android 9.0 Pie+\
Cloud profiles were introduced\
\cell \row

\itap1\trowd \taflags1 \trgaph108\trleft-108 \trbrdrl\brdrnil \trbrdrr\brdrnil 
\clvertalc \clshdrawnil \clbrdrt\brdrs\brdrw20\brdrcf2 \clbrdrl\brdrs\brdrw20\brdrcf2 \clbrdrb\brdrs\brdrw20\brdrcf2 \clbrdrr\brdrs\brdrw20\brdrcf2 \clpadl100 \clpadr100 \gaph\cellx1440
\clvertalc \clshdrawnil \clbrdrt\brdrs\brdrw20\brdrcf2 \clbrdrl\brdrs\brdrw20\brdrcf2 \clbrdrb\brdrs\brdrw20\brdrcf2 \clbrdrr\brdrs\brdrw20\brdrcf2 \clpadl100 \clpadr100 \gaph\cellx2880
\clvertalc \clshdrawnil \clbrdrt\brdrs\brdrw20\brdrcf2 \clbrdrl\brdrs\brdrw20\brdrcf2 \clbrdrb\brdrs\brdrw20\brdrcf2 \clbrdrr\brdrs\brdrw20\brdrcf2 \clpadl100 \clpadr100 \gaph\cellx4320
\clvertalc \clshdrawnil \clbrdrt\brdrs\brdrw20\brdrcf2 \clbrdrl\brdrs\brdrw20\brdrcf2 \clbrdrb\brdrs\brdrw20\brdrcf2 \clbrdrr\brdrs\brdrw20\brdrcf2 \clpadl100 \clpadr100 \gaph\cellx5760
\clvertalc \clshdrawnil \clbrdrt\brdrs\brdrw20\brdrcf2 \clbrdrl\brdrs\brdrw20\brdrcf2 \clbrdrb\brdrs\brdrw20\brdrcf2 \clbrdrr\brdrs\brdrw20\brdrcf2 \clpadl100 \clpadr100 \gaph\cellx7200
\clvertalc \clshdrawnil \clbrdrt\brdrs\brdrw20\brdrcf2 \clbrdrl\brdrs\brdrw20\brdrcf2 \clbrdrb\brdrs\brdrw20\brdrcf2 \clbrdrr\brdrs\brdrw20\brdrcf2 \clpadl100 \clpadr100 \gaph\cellx8640
\pard\intbl\itap1\tx720\tx1440\tx2160\tx2880\tx3600\tx4320\tx5040\tx5760\tx6480\tx7200\tx7920\tx8640\pardirnatural\qc\partightenfactor0
\cf0 Initial Performance\cell 
\pard\intbl\itap1\tx720\tx1440\tx2160\tx2880\tx3600\tx4320\tx5040\tx5760\tx6480\tx7200\tx7920\tx8640\pardirnatural\qc\partightenfactor0
\cf3 slow\cf0  \cell 
\pard\intbl\itap1\tx720\tx1440\tx2160\tx2880\tx3600\tx4320\tx5040\tx5760\tx6480\tx7200\tx7920\tx8640\pardirnatural\qc\partightenfactor0
\cf0 JIT didn\'92t change this metric - \cf4 slow\cf0 \
\cell 
\pard\intbl\itap1\tx720\tx1440\tx2160\tx2880\tx3600\tx4320\tx5040\tx5760\tx6480\tx7200\tx7920\tx8640\pardirnatural\qc\partightenfactor0
\cf0 After app install a new compiler called dex2oat, it would convert/compile .dex(entire APK) code into optimized dex file(.odex) at install time and from there when the app was started it would load .odex files so it was optimized \
\
app install \cf5 slow\cf0  but app start \cf6 fast\cf0 \cell 
\pard\intbl\itap1\tx720\tx1440\tx2160\tx2880\tx3600\tx4320\tx5040\tx5760\tx6480\tx7200\tx7920\tx8640\pardirnatural\qc\partightenfactor0
\cf0 App install started in Interpreted mode(no optimization) with the JIT compiler and the result where stored in a file called \cf7 profile \cf8 which contained a list of classes and methods which were converted to machine code since they were important to make app fast. Once device was idle dex2oat converted the files in \cf9 profile\cf8  to .odex files(background optimization) so the entire app was not converted/compiled as before. This process is repeated as the app is restarted to optimize new discovered hot-paths\
\
So first start after install \cf10 slow\cf8  but it eventually gets \cf11 faster \cf12 as it is optimized\cf0 \cell 
\pard\intbl\itap1\tx720\tx1440\tx2160\tx2880\tx3600\tx4320\tx5040\tx5760\tx6480\tx7200\tx7920\tx8640\pardirnatural\qc\partightenfactor0
\cf0 In cloud profiles, users interaction with the app helped discover common characteristics in profiles which then were uploaded to google play and then shared with similar devices with a similar platform version, this profiles were then provided to the app at install time as APK metadata, this profile aggregation could have taken several weeks since it depended on users app use, on every new version release this process starts from 0. App is \cf13 slow\cf0  for first users but it get \cf11 faster\cf0  with time, number of users and more users interacting with it\cell \row

\itap1\trowd \taflags1 \trgaph108\trleft-108 \trbrdrl\brdrnil \trbrdrr\brdrnil 
\clvertalc \clshdrawnil \clbrdrt\brdrs\brdrw20\brdrcf2 \clbrdrl\brdrs\brdrw20\brdrcf2 \clbrdrb\brdrs\brdrw20\brdrcf2 \clbrdrr\brdrs\brdrw20\brdrcf2 \clpadl100 \clpadr100 \gaph\cellx1440
\clvertalc \clshdrawnil \clbrdrt\brdrs\brdrw20\brdrcf2 \clbrdrl\brdrs\brdrw20\brdrcf2 \clbrdrb\brdrs\brdrw20\brdrcf2 \clbrdrr\brdrs\brdrw20\brdrcf2 \clpadl100 \clpadr100 \gaph\cellx2880
\clvertalc \clshdrawnil \clbrdrt\brdrs\brdrw20\brdrcf2 \clbrdrl\brdrs\brdrw20\brdrcf2 \clbrdrb\brdrs\brdrw20\brdrcf2 \clbrdrr\brdrs\brdrw20\brdrcf2 \clpadl100 \clpadr100 \gaph\cellx4320
\clvertalc \clshdrawnil \clbrdrt\brdrs\brdrw20\brdrcf2 \clbrdrl\brdrs\brdrw20\brdrcf2 \clbrdrb\brdrs\brdrw20\brdrcf2 \clbrdrr\brdrs\brdrw20\brdrcf2 \clpadl100 \clpadr100 \gaph\cellx5760
\clvertalc \clshdrawnil \clbrdrt\brdrs\brdrw20\brdrcf2 \clbrdrl\brdrs\brdrw20\brdrcf2 \clbrdrb\brdrs\brdrw20\brdrcf2 \clbrdrr\brdrs\brdrw20\brdrcf2 \clpadl100 \clpadr100 \gaph\cellx7200
\clvertalc \clshdrawnil \clbrdrt\brdrs\brdrw20\brdrcf2 \clbrdrl\brdrs\brdrw20\brdrcf2 \clbrdrb\brdrs\brdrw20\brdrcf2 \clbrdrr\brdrs\brdrw20\brdrcf2 \clpadl100 \clpadr100 \gaph\cellx8640
\pard\intbl\itap1\tx720\tx1440\tx2160\tx2880\tx3600\tx4320\tx5040\tx5760\tx6480\tx7200\tx7920\tx8640\pardirnatural\qc\partightenfactor0
\cf0 Eventual Performance\cell 
\pard\intbl\itap1\tx720\tx1440\tx2160\tx2880\tx3600\tx4320\tx5040\tx5760\tx6480\tx7200\tx7920\tx8640\pardirnatural\qc\partightenfactor0
\cf14 slow\cf0 \cell 
\pard\intbl\itap1\tx720\tx1440\tx2160\tx2880\tx3600\tx4320\tx5040\tx5760\tx6480\tx7200\tx7920\tx8640\pardirnatural\qc\partightenfactor0
\cf0 JIT improved this metric - \cf15 fast\
\cf16 JIT would automatically discover hot paths however these optimizations were disposed after the process died so disk space was not affected\cf0 \cell 
\pard\intbl\itap1\tx720\tx1440\tx2160\tx2880\tx3600\tx4320\tx5040\tx5760\tx6480\tx7200\tx7920\tx8640\pardirnatural\qc\partightenfactor0
\cf0 All files where optimized at installation so it was \cf11 fast\cf0 \cell 
\pard\intbl\itap1\tx720\tx1440\tx2160\tx2880\tx3600\tx4320\tx5040\tx5760\tx6480\tx7200\tx7920\tx8640\pardirnatural\qc\partightenfactor0
\cf0 Hot paths were optimized as they were discovered so this metric was \cf11 fast\cf0 \cell 
\pard\intbl\itap1\tx720\tx1440\tx2160\tx2880\tx3600\tx4320\tx5040\tx5760\tx6480\tx7200\tx7920\tx8640\pardirnatural\qc\partightenfactor0
\cf0 The optimizations help to have a very \cf17 good\cf0  performance of app as users number and interaction increases\cell \row

\itap1\trowd \taflags1 \trgaph108\trleft-108 \trbrdrl\brdrnil \trbrdrt\brdrnil \trbrdrr\brdrnil 
\clvertalc \clshdrawnil \clbrdrt\brdrs\brdrw20\brdrcf2 \clbrdrl\brdrs\brdrw20\brdrcf2 \clbrdrb\brdrs\brdrw20\brdrcf2 \clbrdrr\brdrs\brdrw20\brdrcf2 \clpadl100 \clpadr100 \gaph\cellx1440
\clvertalc \clshdrawnil \clbrdrt\brdrs\brdrw20\brdrcf2 \clbrdrl\brdrs\brdrw20\brdrcf2 \clbrdrb\brdrs\brdrw20\brdrcf2 \clbrdrr\brdrs\brdrw20\brdrcf2 \clpadl100 \clpadr100 \gaph\cellx2880
\clvertalc \clshdrawnil \clbrdrt\brdrs\brdrw20\brdrcf2 \clbrdrl\brdrs\brdrw20\brdrcf2 \clbrdrb\brdrs\brdrw20\brdrcf2 \clbrdrr\brdrs\brdrw20\brdrcf2 \clpadl100 \clpadr100 \gaph\cellx4320
\clvertalc \clshdrawnil \clbrdrt\brdrs\brdrw20\brdrcf2 \clbrdrl\brdrs\brdrw20\brdrcf2 \clbrdrb\brdrs\brdrw20\brdrcf2 \clbrdrr\brdrs\brdrw20\brdrcf2 \clpadl100 \clpadr100 \gaph\cellx5760
\clvertalc \clshdrawnil \clbrdrt\brdrs\brdrw20\brdrcf2 \clbrdrl\brdrs\brdrw20\brdrcf2 \clbrdrb\brdrs\brdrw20\brdrcf2 \clbrdrr\brdrs\brdrw20\brdrcf2 \clpadl100 \clpadr100 \gaph\cellx7200
\clvertalc \clshdrawnil \clbrdrt\brdrs\brdrw20\brdrcf2 \clbrdrl\brdrs\brdrw20\brdrcf2 \clbrdrb\brdrs\brdrw20\brdrcf2 \clbrdrr\brdrs\brdrw20\brdrcf2 \clpadl100 \clpadr100 \gaph\cellx8640
\pard\intbl\itap1\tx720\tx1440\tx2160\tx2880\tx3600\tx4320\tx5040\tx5760\tx6480\tx7200\tx7920\tx8640\pardirnatural\qc\partightenfactor0
\cf0 Disk Size\cell 
\pard\intbl\itap1\tx720\tx1440\tx2160\tx2880\tx3600\tx4320\tx5040\tx5760\tx6480\tx7200\tx7920\tx8640\pardirnatural\qc\partightenfactor0
\cf11 small\cf0 \cell 
\pard\intbl\itap1\tx720\tx1440\tx2160\tx2880\tx3600\tx4320\tx5040\tx5760\tx6480\tx7200\tx7920\tx8640\pardirnatural\qc\partightenfactor0
\cf11 Small\cf0 \cell 
\pard\intbl\itap1\tx720\tx1440\tx2160\tx2880\tx3600\tx4320\tx5040\tx5760\tx6480\tx7200\tx7920\tx8640\pardirnatural\qc\partightenfactor0
\cf0 There was a memory \cf18 cost\cf0  for storing the optimized code\cell 
\pard\intbl\itap1\tx720\tx1440\tx2160\tx2880\tx3600\tx4320\tx5040\tx5760\tx6480\tx7200\tx7920\tx8640\pardirnatural\qc\partightenfactor0
\cf0 It is \cf11 smaller\cf0  than in previous API\cell 
\pard\intbl\itap1\tx720\tx1440\tx2160\tx2880\tx3600\tx4320\tx5040\tx5760\tx6480\tx7200\tx7920\tx8640\pardirnatural\partightenfactor0
\cf0 Is still \cf11 smaller\cf0  that some of the previous approaches\cell \lastrow\row
\pard\tx720\tx1440\tx2160\tx2880\tx3600\tx4320\tx5040\tx5760\tx6480\tx7200\tx7920\tx8640\pardirnatural\partightenfactor0
\cf0 \
\
	Baseline Profiles are a way for the app to provide the app with what is important to the runtime. It is a way to bundle optimized code to the APK \
	itself, they work for apps as well as libraries(libraries creators can benefit from baseline profiles by providing them to all consumers)\
\
	They can be ported back to android 7, but before android 9, so between 7-9 in order for the package installer to install the baseline profile rules you need\
	to add a dependency on Android X Profile Installer to your app, this dependency is also useful/needed if your app is going to be available through other services	other than Google Play Store. So you actually should always add this dependency if you\'92re adding a baseline profile.\
\
	\cf19 Generate Baseline Profiles\
	\
	\cf20 You can use Jetpack Macro Benchmark library. \
\
	\cf21 Measure Effectiveness\cf20 \
\
	There is two options, but it means you would compare your previous performance metrics with the new performance metrics using either of the following:\
		\
		1.- Check field metrics: You can use Google Play Vitals or Firebase Performance Monitoring\
\
		2.-  Lab Environment: You can use Jetpack Macrobenchmark run it locally on a device since you can pass a parameter to your test to run it in \
		different compilation modes \
\
\cf0 \'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\
\
Compose Tooling in Android Studio\
The typical UI development workflow consists of three phases, design, develop and test. In each of this phases we can leverage different functionality from \
different tools. The following Is the tools we have available in each phase:\
\
	1.- Design: \
		- Compose Preview: Is an annotation that will let you generate a preview of the composable You can do a design system and preview all \
		colors and fonts. There is a spec parameter you can use to display different screen sizes, the following string would be that parameter value:\
		\'93spec:width=673dp, height-891dp, dpi=480\'94 (reference foldable)\
\
		- Interactive Preview: Is a mode we have available in the preview screen which let us interact with composables\
\
		- Preview Parameters: Add different parameters to the annotation to preview this like different languages using a locale parameter. You can create\
		a class to provide data to the compose preview annotation that represents information from the model component from our architecture(domain layer) 		and that class just has to extend the class PreviewParameterProvider<T> and this class will override a \'93values\'94 property which is a sequence 		of type T and then use an annotation in a parameter of the preview function:\
		\
		class MyDataProvider: PreviewParameterProvider<MyModel> \{\
			\'85\
		\}\
		\
		@Preview\
		fun myComposable(\
			@PreviewParameter(MyDataProvider::Class)\
			information: MyModel\
		) \{\
			\'85\
		\}\
		 \
\
		- Multipreview: Use multi preview annotations like the below in an annotation class, and you can use multiple of these classes\
\
			@Preview(locale = \'93en\'94, name = \'93English\'94)\
			@Preview(locale = \'93ja\'94, name = \'93Japanese\'94)\
			annotation class LocalesPreview\
\
		- Animation Preview: If you build animations using compose you can preview them just from the preview. It supports update transitions and\
		animated visibility, and more will come\
\
	2.- Develop: These tools helps us accelerate building and testing running applications\
		- Live Edit: You can change some parameters Iike clicks callbacks and they will update live on device/emulator. You have the option to make allow		this update to happen automatically or make it manually. You have to enable it from settings/editor\
		- Editor Features: they\'92re divided into three categories, Intention, Code completion, Live templates\
			*- Intention: Helps Creating the composable function(just define signature and right click) and also surround composables with box/row/column\
			*- Code completion: Adds placeholder in lambda functions, suggest Modifier extension functions without typing \'93Modifier.\'94 first\
			*- Live Templates: tipe \'93comp\'94 or \'93prev\'94 to create a new composable or preview respectively. \
\
	3.- Debug: How to analyze layout and recompositions to improve UI performance\
		-  Layout Inspector: Lets you monitor how many times a composable is recomposed or spiked recomposition(good performance if its state \
		has not changed)\
		- Profiler: Lets us record computations happening in our application and now also we can get more info from compose composition tracing, it will \
		tell us what composable caused recomposition or suspicious functions\
\
\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\
\
State Hoisting(Compose)\
\
Is the practice of making composables stateless by moving state to a composable\'92s caller.\
\
\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\
\
\pard\tx720\tx1440\tx2160\tx2880\tx3600\tx4320\tx5040\tx5760\tx6480\tx7200\tx7920\tx8640\pardirnatural\partightenfactor0
\cf0 \ul \ulc0 State Holders and State Production in the UI Layer\
\pard\tx720\tx1440\tx2160\tx2880\tx3600\tx4320\tx5040\tx5760\tx6480\tx7200\tx7920\tx8640\pardirnatural\partightenfactor0
\cf0 \ulnone \
We have to understand app architecture first, so we have the following components:\
	\
	\ul Data layer\ulnone : Is going to expose application state the rest of the hierarchy/components or layers. It contains the vast majority of business logic\
\
	\ul Domain Layer\ulnone : Main mission is to simplify the potential business logic that UI layer could need\
\
	\ul UI layer\ulnone : Display the data provided by the previous layers and in this case we can separate it two entities\
\
		State Holders: They hold and expose state to the UI elements. They hoist logic either business logic or UI logic	\
		UI elements: Render the info on the screen, but when talking in compose these components depend on the other entity, \'93State Holders\'94\
\
There is different types of state holders, UI state, Types of Logic\
\
\pard\tx720\tx1440\tx2160\tx2880\tx3600\tx4320\tx5040\tx5760\tx6480\tx7200\tx7920\tx8640\pardirnatural\partightenfactor0
\cf0 \ul Types of UI State\
\
\pard\tx720\tx1440\tx2160\tx2880\tx3600\tx4320\tx5040\tx5760\tx6480\tx7200\tx7920\tx8640\pardirnatural\partightenfactor0
\cf0 \ulnone 	Screen UI State: Info the app presents to the user, like the Home Screen feed\
\
	UI Elements State: Internal state of a reusable UI element, it can be the scroll position in a list or a selected tab or a selected radio box\
\
\pard\tx720\tx1440\tx2160\tx2880\tx3600\tx4320\tx5040\tx5760\tx6480\tx7200\tx7920\tx8640\pardirnatural\partightenfactor0
\cf0 \ul Types of Logic\ulnone \
We differentiate them by what the logic does\
\
	Business Logic: Implementation of product requirements for application data. Most of it is present in the data layer most of it in the repository implementation\
\
	UI Logic: How to display state changes on the screen, it depends on screen configuration such as screen size, language or orientation, depending on 	configuration the UI logic might be different as in a cellphone a click could trigger navigation while on a tablet it could just display more info on the screen\
\
So this would be the order of the previous components:\
\
        \
	       Data and domain layer				UI layer\
	|\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97|\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97\'97|\
		   	
\fs20 business logic
\fs24 				    
\fs20 UI logic
\fs24 \
	App State \'97\'97\'97\'97\'97\'97\'97\'97> Screen UI State \'97\'97\'97\'97\'97\'97> UI + UI elements state\
\
\
\ul Types of State Holders By Logic\ulnone \
They both can be implemented in a class however there is some different implementations recommended for different state holders\
\
	Business Logic:  Business logic/model state/application state would be hoisted in a screen UI State holder\
	\
	UI logic: UI logic could be hoisted in a UI element state holder meaning in the UI itself or in a State Holder located above like in the ViewModel\
\
Stated Holders Recommended Implementation\
\
	Screen UI State(Hoists business logic data): Is recommended to attach the life of this state holder to a ViewModel because ViewModels survive 	configuration changes and also because they are cached in memory whenever the fragment is in the back stack, and also because they are destroyed when\
	the fragment is not in the back stack meaning there is no state cached leading to weird states for the user this is all possible thanks to the jetpack navigation 	library to which fragments integrate to and that handles the backstack, also because View Models integrate with other libraries like hilt, so we can I	nject elements/classes from data/domain layer  and those components can be passed to the state holder\
\
	UI Element State(Hoist a UI element state): It could just live inside a composable(a boolean for expand composable, selected state of a check box) if the state \
	isn\'92t too complex but if it is, you should hoist the state to a separated class like in compose LazyListState is complex as it has different properties and \
	functions and like so if the composable state is too complicated a new state holder class should be created, these state holder classes are compoundable \
	meaning they can contain other state holder/depend on other state holders\
\
	The following state holders are an example of what you would need in an app:\
\
		ExampleAppState: contains:\
			NavController, currentDestination, shouldShowBottomBar, topLevelDestinations\
	\
		ExampleFeatureScreenViewModel: inside this class we hold the model state and we handle business logic like retrieving a list to pass it down to Screen UI State.\
		The Screen UI State should be exposed as an observable data holde. The following is just an example of the UI state class inside a view model: homeUiState\
			\
		Ui component state: local state like LazyListState, LazyGridState, etc\
\
5 Ways Compose Has Changed How We Test UIs\
Test should be easy to write, fast and reliable however since compose was designed with testability in mind we can say that with compose \'93tests are easier to write, faster and \
more reliable\'94 \
\
	1. Testing In Isolation\
	When you create a compose test you can launch one of your activities by either of the two ways below\
\
		class Ads22ComposeTests \{\
			// This starts the activity you define\
			@get:Rule\
			val composeTestRule = createAndroidComposeRule<MyActivity>()\
			\
			// You also have the option to start an empty activity and set content yourself\
			@get:Rule\
			val composeTestRule = createComposeRule()\
			\
			//Only of the second way of starting/creating an activity in your test\
			@Test\
			fun ads22_isolation() \{\
				composeTestRule.setContent \{\
					MyApp()	// This can be any composable, you can test any composable in isolation, pass its parameters, like fake objects list and dummy objects(clicks)\
				\}\
			\}\
		\}\
\
	2. Automatic Synchronization\
	How the test knows when to send the next action or perform the next assertion, you would need to use tools like espresso which has ways to figure out if the app is	busy or idle(is activity RESUMED?, is there idling resources?, is the main thread idle?, is the UI idle?) and views don\'92t have a way to tell you they\'92re busy, however 	this is exactly what compose does as it exposes a much more straightforward signal to the tests, making the more reliable and faster(using the same test class ass above)\
	\
		// This wouldn\'92t be the right way to synchronize interactions\
		@Test\
		fun mySlowTest() \{\
			composeTestRule.onNodeWithText(\'93Continue\'94).performClick()\
			Thread.sleep(2000) // Don\'92t do this!\
			composeTestRule.onNodeWithText(\'93Welcome\'94).assertIsDisplayed()\
		\}\
\
	Compose works with automatic synchronization, usually you don\'92t have to think too much about it, but you still in some cases need to synchronize asynchronous operations	happening across all the layers of the app.\
\
	3. Controlling time\
	In compose test you can pause time or advance clock as much as needed. This is great for testing state\
\
		@Test\
		fun automaticSync_afterOneSecond() \{\
			composeTestRule.mainClock.autoAdvance = false\
\
			composeTestRule.setContent \{\
				ClockAnimation(startTimeSeconds = 1)	// This can be any composable\
			\}\
\
			composeTestRule.mainClock.advanceTimeBy(1000)\
\
			// You can also go frame by frame\
			composeTestRule.mainClock.advanceTimeByFrame()\
		\}\
\
	4. Waiting For Things to Happen\
	Even with automatic synchronization as test grows it will get harder to deal with all the asynchronous operations that happens and in end-to-end test it might not even wroth	to make sure everything is synchronized, that is why we can tell the test to wait until something happens with the \'93WaitUntil\'94 API, it can pass the test until the body is true\
\
		@Test\
		fun mainScreen_navigateToDetails() \{\
\
			composeTestRule.setContent \{\
				MyScreen(FAKE_ITEMS, \{ \})	// This can be any composable\
			\}\
\
			composeTestRule.waitUntil \{\
				composeTestRule.waitUntil \{\
					composeTestRule\
						.onAllNodesWithText(\'93kotlin\'94)\
						.fetchSemanticsNodes().size > 0\
				\}\
			\}\
		\}\
\
	5. Verify State Restoration\
	We can emulate a configuration change very easily\
		\
		@Test\
		fun restoreState() \{\
\
			val restorationTester = StateRestorationTester(composeTestRule)\
			restorationTester.setContent \{ MyScreen() \}\
			// TODO: Run some actions that modify the state\
			restorationTester.emulateSavedInstanceStateRestore() // Triggers a recreation\
			// TODO: Verify that state has been correctly restored\
		\}		\
\
5 Upcoming Android Studio New Features\
\
	1. Improvements in the network inspector - located in the \'93Resource Manager\'94 \
	2. Download information in the \'93Build Analyzer\'94 - Is a new metric that tells you how much of your build time was spent downloading dependencies, but also	when artifacts are downloaded needlessly so you can fix your buildscript\
	3. Android SDK version upgrade - (personally not using it much since I already know good enough about configuring Gradle)\
	4. Physical Device Mirroring\
	5. Emulator Bluethoot Support - you can simulate a bluetooth connection across different emulator instances\
\
Performance Tips for Jetpack Compose\
\
	1. Benchmark - Write a benchmark to know if your performance optimizations are working\
	2. Deferred State - Read state as late as possible using lambdas\
	3. DerivedStateOf - Used when your state or key is changing more than you need to update your UI\
	4. Stability - Compose determines the stability of composables to determine if they can be skipped, The skipability of a function is determined by the stability	of its parameters, they can be of type \'93Immutable\'94(compiler is sure the values of the object\'92s properties will never change, usually all its parameters will be \'93val\'94s and not 	\'93var\'94s, also they should use immutable collections, also if working it contains a third party library object you can annotate the class with \'93Immutable\'94 to force/tell the compiler	to treat it as immutable even thought those properties will be annotated with \'93unstable\'94, the wrapper class will be annotated with \'93stable\'94) or \'93Stable\'94(Is mutable but the \
	compiler will be notified when properties has changed, in practice this means those properties are wrapped inside a state functions like \'93mutableStateOf\'94, also they 	can be annotated so the compiler treats them as stable with \'93stable\'94 annotation) or \'93Unstable\'94(this classes can\'92t be skipped, these type of objects have \'93var\'94s defined	instead of \'93val\'94s) \
	5. reportFullyDrawn() - Allows Android to optimize your apps startup\
\
Offline-firts Apps\
For both, reads and writes, managing connectivity changes require implementing two main functions, \'93Queues\'94(to deferred/consume actions till the network is available) \
and \'93Network Monitors\'94(As a signal to drain the queue as soon as the network becomes available). External layers should always read from the local data source. Apps \
Don\'92t have to write data offline to be considered offline-first because writes requires more considerations than reads, there still can be failures/network errors and the \
solution is just simply retry if it is needed/required/requested\
\
	Synchronization\
	When getting/reading data from network data source there is two ways of reconciling data in the local data source and is this process is called synchronization\
		\
		Pull-bases\
		Reads latest data on demand like when navigating to a new screen, only fetches the current screen data\
			Pros\
			Relatively easy to implement. Data is not needed will never be fetched\
			Cons\
			Prone to heavy data use. Does not scale well with relational data \
\
		Push-bases\
		Local data source tries to mimic a replica set of the network data source, it usually proactively fetches a small amount of data on first startup to set a baseline		after which it relies on notifications from the server to alert when data is changed.\
			Pros\
			The app can remain offline indefinitely. Minimum data use(only needs data from initial synch to display info). Works well for relational data\
			Cons\
			Versioning data for conflict resolution is non-trivial. Concurrency concerns during synchronization. Must be supported by the network\
\
		If the app generates data, while being offline, that is misaligned with the network data you have to resolve conflicts before synchronization takes place\
\
			Conflict Resolution\
			Last write wins, meaning if different devices writes local data offline and then get online they will sync with the network the last sync will override info from			other devices previews synchs, that means the device with outdated info will be notified about the change and have its data synch wit the network\
\
Modifiers Deep Dive\
\
Design\
What constraints and design goals led to the current Modifier APIs?, Modifiers now use a Modifier.Node API to apply them throughout the whole composition process\
\
Performance\
What does Modifier usage look like today? What performance issues does it present? The new way of applying the modifiers is more performant since it has fewer iterations,\
has fewer compositions, and the generated code is fewer\
\
Future\
How is the new architecture beneficial? How do these changes affect me?\
\
Variable Fonts\
They are fonts that can contain many styles in a single font file, only available on Android O and above\
\
Annotated Strings in Compose\
You can build an annotated string in compose with the following code\
\
	buildAnnotatedString \{\
		val text = getTexParttToFormat()\
		val spanStyle = SpanStyle(\
			fontFamily = FontFamily.Monospace,\
			background = codeSnippetBackground\
		)\
\
		withStyle(style = spanStyle) \{\
			append(codeText)\
		\}\
		append(otherText)\
	\}\
\
Customize a TextField Composable Border\
You can use the \'93border\'94 modifier, and you also have different composable components option \'93TextField\'94, \'93OutlinedTextField\'94, \'93BasicTextField\'94\
\
	TextField(\
		value = textFieldValue,\
		onValueChange = \{ onTextChanged(it) \},\
		modifier = Modifier.\
			border(\
				border = BorderStroke(\
					brush = Brush.linearGradient(Gradient),\
					width = 2.dp\
				),\
				shape = CutCornerShape(12.dp)\
		)\
	)\
\
\
	You also have the option to use the \'93Foundation\'94 component \'93BasicTextField\'94 instead of the \'93Material 3\'94 component, which will give access to 	to customization fields like \'93cursorBrush\'94 which you can pass a brush gradient to change color as the cursor moves or just define a solid color\
	also \'93decorationBox\'94 which lets you add a composable like a row to which you can define a background modifier and then set an icon and then	consume the callback value, which is the text input so the text its written can have an icon and a color background added\
\
	If you need more info check \'93Text in Compose\'94, \'93Fixing Font Padding in Compose Text\'94, \'93Effective State Management for TextField in Compose\'94,\
	\'93Brushing up on Compose Text Coloring\'94 and \'93Animating Brush Text Coloring in Compose\'94\
\
\
Measure App Performance With Profileable Builds\
Android Studio Profiler helps you find where CPU cycles and memory are spent at the end time of inspection, previously profiling an app required a debug build\
, but not anymore as this builds enables a lot of features/functionalities at the cost of performance and and that is why now instead the only thing needed to profile\
an app(measure its performance) is a profileable app, when choosing this type of variant the \'93debuggable\'94 flag in the manifest/buildscript is set to true\
\
	Debug builds\
	These builds lets you use the following features throughout the process of creating your app\
		\
		Build\
		When building a debug variant of the app you can use \'93Apply Changes\'94 and \'93Live Edit\'94 features\
		\
		Debug\
		When debuging these variants you can use \'93Debugger\'94, \'93Database Inspector\'94 and \'93Network Inspector\'94\
		\
		Profile\
		When profiling these type of variants you can use \'93Heap Dump\'94, \'93Live Allocation Recording\'94 and \'93Energy Profiler\'94 features\
\
	Profitable Builds\
	Rendering frames in Debug builds could takes a lot more than in Release builds, but this is all because of the overhead that is implicit when making	and app debuggable to have access to all functionalities/features mentioned above, we can monitor the time a frame takes to render directly in our	cellphone using the developer options in the section \'93monitoring\'94 option \'93Profile HWUI rendering\'94 with \'93On Screen as Bars\'94 this will show a bars overlay,\
	a high bar indicates more time to render a frame, a short frame indicates the opposite and also a smother animation. This is why the \'93profitable\'94 flag was	created,  so you can actually get a more real more \'93release\'94/\'93production\'94/\'93real\'94 performance measurement, turning this flag on enables many profiling tools\
	that measure timing info whiteout the performance overhead of a debug build, available on devices using android 10 or higher\
	\
	Profileable apps have access to the following tools\
		\
		CPU profiler\
		You can use \'93Default View\'94, \'93Callstack Sampling\'94, \'93System Trace\'94\
\
		Memory Profiler\
		You can use \'93Default View\'94 and \'93Native Memory Profiler\'94, if the app is profitable you can not use \'93Heap Dump\'94 nor		 \'93Live Allocation Tracking\'94/\'93Record Java/Kotlin Allocations\'94\
\
		You can not use the \'93Energy Profiler\'94 nor \'93Event Timeline\'94 the app is profitable\
\
	You can use profitable options by making your app profileable in either of the two following ways:\
		\
		Automatically with Android Studio\
		With the \'93Profile\'94 icon right next to the debug icon in the IDE, chose \'93Profile App with Low overhead\'94, AS will automatically build a profitable app\
		of your current build type/variant and attach the profiler. It works with any build type but its recommended to profile a release build(because its		what your users see) \
\
		Manually Configure the App\
		In case you want to diagnose performance issues in production, there is 4 steps to do this:\
			1.- Add this to the manifest(This flag is safe to use in production/release builds as it is design to be usable in release builds to enable 			local profiling and no memory data is readable by the host profiling tools and the shell process as only stack tracers are readable which			typically obfuscated or lacking symbols in release builds) \
				<application>\
					<profileable android:shell=\'93true\'94>\
				</application>\
			\
			2. Switch to release build type variant or any other non-debuggable variant\
			3. Configure a signing key, you can configure a key just for profiling\
			4. Attach the profiler\
\
	So in summary the build types are used for the following purposes\
	\
		Release Build\
		Ideal for production\
		\
		Profileable release build\
		Ideal for Profiling CPU timing\
	\
		Debug Build\
		To use the debugger, inspectors, etc. also for profiling memory, profiling energy\
\
App Quality Insights\
Is a new feature/option in AS where you can see the most impactful crash reports from crashalitycs, they are sorted by the number of impacted users so\
you know which crashes are most impactful, you can click into the stack traces that will lead directly into app codebase\
\
Animations in Compose\
	\
	\'93animatedVisibility()\'94 composable (crane sample app)\
	Just wrap whatever composable you want in this composable to animate its visibility bases on a boolean state\
\
	\'93animateContentSize()\'94 modifier (crane sample app)\
	Use this modifier to make any size change run smoothly, example: in a text changing the max lines based on a state, or directly the height on	any composable. You can specify an \'93animationSpec\'94 parameter in which you can use different \'93animations\'94 like spring and a few more\
\
	\'93AnimatedContent\'94 composable (crane sample app)\
	You can use it to pass a state, like a selection or the value of a Emun, to the parameter of this composable, usually you will evaluate the 	state inside this composable using a \'93when\'94 condition to display different composables depending on the current value. You can also use other	parameters like \'93transitionSpec\'94 which is a lambda where you can define code like the following\
	\
		slideIntoContainer(\
			animationSpec = tween(300, easing = EaseIn),\
			towards = Up\
		).with(\
			slideOutOfContainer(\
				animationSpec = tween(300, easing = Easeout),\
				towards = Down\
			)\
		)\
\
	\'93animateFloatAsState\'94 (Jetsurvery sample app)\
	This sample app has a progress bar created using \'93LinearProgressIndicator\'94 composable which takes a float value to indicate the progress, full \
	progress is the number 1. We can wrap the progress percentage inside this constructor and pass it to the composable and it will animate\
\
	Animate a border of an Image\
	You would use the following code\
		\
		@Composable\
		fun ImageBorderAnimation() \{\
			val infiniteTransition = rememberInfiniteTransition()\
			val rotationAnimation = infiniteTransition.animateFloat(\
				initialValue = 0f,\
				targetValue = 360f,\
				animationSpec = infiniteRepeatable(tween(1000, easing = LinearEasing))\
			)\
			Image(\
				modifier = Modifier\
					.drawBehind \{\
						rotate(rotationAnimation.value) \{\
							drawCircle(rainbowColorBrush, style = Stroke(borderWidth))\
						\}\
					\}\
					.padding(borderWidth)\
					.clip(CircleShape)\
			)	\
		\}\
	\
\
\
\
\
\
\
\
\
\
\
\
\
\
\
\
\
\
\
\
\
\
\
\
\
\
\
\
\
\
\
\
\
\
\
\
\
\
\
\
\
}