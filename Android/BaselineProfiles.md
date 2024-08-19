{\rtf1\ansi\ansicpg1252\cocoartf2709
\cocoatextscaling0\cocoaplatform0{\fonttbl\f0\fswiss\fcharset0 Helvetica;}
{\colortbl;\red255\green255\blue255;\red191\green191\blue191;\red251\green0\blue19;\red251\green0\blue7;
\red251\green0\blue28;\red35\green255\blue10;\red103\green79\blue12;\red6\green0\blue8;\red168\green135\blue5;
\red206\green0\blue19;\red34\green255\blue6;\red1\green23\blue6;\red251\green0\blue7;\red251\green0\blue48;
\red34\green255\blue11;\red9\green0\blue7;\red34\green255\blue28;\red251\green0\blue12;\red24\green51\blue255;
\red10\green1\blue15;\red24\green33\blue255;\red10\green1\blue15;}
{\*\expandedcolortbl;;\csgray\c79525;\cssrgb\c100000\c0\c8125;\cssrgb\c100000\c841\c0;
\cssrgb\c100000\c0\c13888;\cssrgb\c1630\c100000\c1630;\cssrgb\c48268\c37765\c4782;\cssrgb\c1826\c200\c2454;\cssrgb\c72041\c59218\c0;
\cssrgb\c85351\c0\c8517;\cssrgb\c0\c100000\c0;\cssrgb\c0\c11696\c2002;\cssrgb\c100000\c0\c0;\cssrgb\c100000\c0\c24490;
\cssrgb\c0\c100000\c2883;\cssrgb\c3197\c139\c2360;\cssrgb\c0\c100000\c13754;\cssrgb\c100000\c0\c3335;\cssrgb\c12776\c32420\c100000;
\cssrgb\c4022\c614\c7012;\cssrgb\c12885\c26291\c100000;\cssrgb\c4022\c614\c7012;}
\margl1440\margr1440\vieww30040\viewh16360\viewkind0
\pard\tx720\tx1440\tx2160\tx2880\tx3600\tx4320\tx5040\tx5760\tx6480\tx7200\tx7920\tx8640\pardirnatural\partightenfactor0

\f0\fs24 \cf0 \
Performance\
\
Baseline Profiles\
\
	Android Code Execution Evolution\
	Some of the history/background of how google used to optimize apps, performance or execution is evaluated in three dimensions, initial performance(performance after install and/or after app start), eventual performance(performance	after the runtime has a chance to discover some hot paths), disk size(cost of the optimizations in terms of disk space required)\
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
	Baseline Profiles are a way for the app to provide the app with what is important to the runtime. It is a way to bundle optimized code to the APK itself, they work for apps as well as libraries(libraries creators can benefit from baseline	profiles by providing them to all consumers)\
\
	They can be ported back to android 7\
\
	\cf19 Generate Baseline Profiles\
	\
	\cf20 You can use Jetpack Macro Benchmark library. \
\
	\cf21 Measure Effectiveness\cf20 \
\
	There is two options,\
		\
		1.- Check field metrics: You can use Google Play Vitals or Firebase Performance Monitoring\
\
		2.-  Lab Environment: You can use Jetpack Macrobenchmark \cf22 run it locally on a device \cf0 \
\
\
\
}