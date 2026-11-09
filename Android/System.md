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

In your app process you have the `PhoneWindow` which is just a representation of the Window within the app process, when you call `setContentView()`, when we call the `setContentView` 
function we pass and instance of the `PhoneWindow` to the window manager `WindowManager.addWindow(phonewindow)` which creates the actual window of our app, this an inter process communication 
between our process and the system process that WindowManager runs on, this communication is done through a `Binder` object this points to the `ActivityRecord`, then calls to 
`mWindowSession.addToDisplayAsUser(IWindow)`, the record helps us identify our window in the system, at this point a clear application has been created in the system server, now a few views 
are created, `decorview`, the window's background points to the background of this view, it also contains another layout, that layout contains the system status bar, action bar, title, and 
menu,(action bar and its title and menu has been replaced with a `Toolbar`), it contain the navigation bar also, but also a view known as R.id.content which is the direct parent of your app's 
UI, but at this point nothing is displayed on screen yet, so the app decides what to draw on screen(we already set the content), window manager decides where on screen should be drawn, and 
then something called `SurfaceFlinger`, actually there is something in between our hierarchy root's node and the window manager and that is the `ViewRootImpl`, it kind of holds a reference to 
the window(IWindow) that is in the system server, it is a root element that is responsible for connecting the underlying surface with the canvas and is also responsible for triggering the first 
layout, top level layout, top level drawing, top level motion, and event dispatching, in theory it should receive a reference to a `SurfaceHolder` there is much more going on and there is more 
components participating in this process(it means it might not literally be doing that directly but the idea behind the process is that), the `SurfaceFlinger` has a three "layers", 
"Container layer", "container Layer"(yes, there is two), "Buffer layer", so the view structure and the layers of tasks are collapsed into a buffer called "Frame Buffer" this buffer basically 
contains the pixels, the hardware display directly reads from that buffer, so basically the window rely on the `SurfaceFlinger` to reach that buffer, the flinger creates a layer that is sent to 
the buffer, and now our activites are up, the buffer layers consist of transactions which is a batch of instructions that process at same time, these instructions contain drawing instructions 
like change visibility, change position, etc.
