# [Dive into the Window Manager by Vadim Caen and Pablo Gamito](https://youtu.be/k_JuZCWeeuA?si=NzSGJUAdqTqILLHq)

Status bar and navigation bar both are rendered in its own window with a transparent background, window manager instantiates activities, and manages it lifecycle, this manager allows 
apps to safely share display, it gets the activity on and off screen. It provides a way for apps to draw on screen but also enforces some rules around what is shown on screen.

The process of staring an activity to be visible on screen is managed by the window manager, the steps are:

1. Someone makes a "Start Activity" request, that is usually a "Launcher", that launches an intent the window manager handles
2. Create a task, you can think of it as a stack of activities, if your app is a single activity app and is using Fragments then the task should only contain that one activity, otherwise
   this will piling up activities which is called the back stack
3. Creates an `ActivityRecord`. FYI There is a tree like structure in window manager, the state of the parents are connected to the children, so if we hide a task everything under it hides,
   if we move a task, everything else under it also moves.
4. It sends a request to create a new process for the app to run on, this is sent to the zygote process, zygote is a process that contains all the packages, holding memory, files, basically
   we clone(`fork()`) this process for our app
5. Start activity thread(Main thread)
6. Starts running lifecycle callbacks
