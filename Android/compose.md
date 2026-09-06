
* `NavigationSuiteScaffold` vs `SceneDecoratorStrategy`: Both APIs helps us achieve adaptive layouts, the former seems to only be available in Android and not CMP and is part of the
`androidx.compose.material3.adaptive.navigationsuite` package, so it is not exactly part of a navigation library on itself however it integrates well with any navigation library,
the latter is available in CMP and is part of the `androidx.navigation3.scene.SceneDecoratorStrategy`, as you can see is part of navigation's 3 Scene API, the scene API seems to
be more flexible however a little bit more difficult to configure, what we need to understand is what these two APIs helps us to achieve in adaptive layout, and that is displaying
the right navigation UI, which could be a navigation bar(bottom), a navigation rail, or a persistent/expanded navigation drawer, in material 3, that last one is not recommended
anymore, instead you should use an expanded navigation rail. The former API basically "automates" this process, however the former seems to be more "flexible" and can be implemented
across all CMP targets.

* **Navigation State** vs **Navigation Back Stack**: Basically the former is just an "abstract" concept and the latter is an actual component of the navigation3 API, so the state is
represented by what the content of the back stack is, the back stack is a list of `NavKey`s(objects implementing `NavKey` interface), so we need to keep a reference to this list in
order to make the `NavDisplay` "navigate" around `NavEntry`s by modifying the stack, a `NavEntry` is created with the `entryProvider` DSL but it can be decorated as mentioned in
**Important Navigation3 NavEntry Decorators**, which at the same time bundles the backstack inside the object returned by the function `rememberDecoratedNavEntries` which is in charge
 of somehow absorbing the backstack, decorate the `NavEntries`(provided by the `entryProvider` dsl to the param with the same name) and bundle them with the stack(provided by the
`backStack` param), it will also take a list of `NavEntry` decorators, and finally return a list of `NavEntry`s, the backstack somehow is implicitly available to the `NavDisplay`
after we call this function(We will have to look into the source code to know how but it is probably using a `CompositionLocalProvider`) which kind of obscures the backstack being
passed explicitly to `NavDisplay` to the developer so you have to keep a reference to it somewhere else so you can modify it, remember `NavEntry`s map `NavKey`s to specific
composables/screens, in this setup we just pass a list of decorated `NavEntries` and a `onBack` parameter to `NavDisplay` and we can start modifying the stack to navigate across
`NavEntry`s, what is important to know about the returned `NavEntry` list is that it only survives recompositions and config changes but not system-initiated process death, we will talk
more about this detail because if we don't survive the stack state we could loose navigation state/app state across system-initiated process death and app recreation after process death,
The other way to configure a `NavDisplay` is to pass a the backstack directly, the `onBack` lambda, and the entry in the form of `entryProvider` DSL. But we will focus in the `navDispaly`
signature that takes the `EntryList` because the functionallity added to the entries by the decorators are essential in a modern apps. So now we are talking about two lists, first the
backstack and then the nav entriest list, they are essentially list, and therefore anyway of creating a list will work, each with its own implications, using `listOf<NavEntry>()` and
`mutableListOf<NavEntry>()` are definitely valid however you would need to store it in a way that whenever you need to add, remove, move items within the list, you need to create a new
list, the initial list would be turned into a state using a funciton like `mutableState`, this way whenever we assign the new list holding the updated value of the stack it can trigger
recompositions, but also wrapp it around `remember` or `rememberSaveable` depending on the persistence you want it to have but also if the object being wrapped is parcelable which is
required by `rememberSaveable`, if you want to make it parcelable you may need to write its serializer manually, or you can store it in a `MainViewmodel` and put it in a state that is
changed by a new instance of the state whenever you need to change the state of the stack, another way make the stack state trackable to compose is to use `mutableStateListOf` depending
on the architecture of your app you could store it in the viewmodel or "locally" to your root composble or create an App state holder, which is what we usually preffer to do, however
there is an even better way to create a `NavKey`(stack) list, that is the `rememberNavBackStack()` function, it takes a list of `NavKey`s and seems to return a `mutableStateList` wrapped
arround `rememberSerializable` which we already talked about in this document, meaning that the list survives conf changes, recompositions and system-init process death, so now that we
have a list that is presistent a trackable to compose runtime, we now can be sure that our nav entries list produced by `rememberDecoratedNavEntries` can be recreated across system-init
process death and app recreation using the correct stack state and therefore landing to the correct screen when user returns to app. We will talk about hoisting the stack in a plain state
holder class which follows the state holder pattern which is what `rememberLazyListState()` does, basically we wrap the components that make our app state capable to survive system-init
process death around a state class which can only survive recompositions but not conf changes nor process death. Lets talk about it in **Multiple back stack** section below

* **Multiple Back Stacks**: Before we talk about multiple back stack we should know that in material 3 Navigation Drawers are discouraged and they recommend using bottom nav bars,
nav rails and expanded nav rails. Usually what you want is compose to be able to track the state changes of a list that survives recompositions, configuration changes and sys-init
proess death, this is possible by using the "old concept" of "saved state"/"saved state registry" which is provided by APIs like `rememberSaveable` and `rememberSerialisable` which we talk
about in this doucment in another section, in navigation composables we mentioned here this is possible through the APIs mentined in **Navigation State vs Navigation Back Stack**. So here
we want to talk about how to create some kind of nested navigation with multiple stacks, there is different approaches, you could do what is called  "exit through home" pattern, imagine you
have three top level routes A, B and C, your nav bar show those three nav options, each of those routes can navigate to other routes in its flows, for example A can hoe A -> A1 -> A2 and B
and C can do similar navigation, but in here the user always exits through the starting back stack. This means that Route A's entries are always in the list of entries, navigating to a top
level route that is not the starting route replaces the other entries. For example, navigating A->B->C would result in entries for A+C, B's entries are removed. Another way to handle backstack
is by actually keeping all visited routes, keeping a flattened back stack which is a combination of the individual back stacks of all the tabs, for example I go A->A1->A2->B->B1->C->C1->A2
then my stack would be (B, B1, C, C1, A, A1, A2) at this moment B would be our exit point, an example of these approaches can be found [here](https://github.com/android/nav3-recipes/tree/main/app/src/main/java/com/example/nav3recipes/multiplestacks)
for "exit through home" and [here](https://github.com/android/nav3-recipes/blob/main/app/src/main/java/com/example/nav3recipes/commonui/CommonUiActivity.kt) for the other approach. Ok so
how to do multiple backstacks?, first create a `rememberNavState()` composable, this takes two params, the start `NavKey` and the list/set of top level `NavKey`s, use the set of top level
`NavKey`s and transform it into a map that uses the top level key as the key and creates a stack for each key, each stack contains the top level `NavKey` as first element, do that with the
collecitons function `associateWith`, inside the mapper create the stack with `rememberNavBackStack`, again it should include the top level key which will be the root of the given nested stack,
these lists persist across any scenario in Android only, remember they use the `rememberSerializable` along with `mutableStateListOf` to be able to persist the list of keys, we will talk
about how it works in CMP in a second. Now we need to create a NavState class that takes three params, the start key, a top level route key, at applications start up this is the home tab, and is basically
the start key but wrapped just like the stack, using `rememberSerializable` and `mutableStateOf`, and the last param is the stack map we just created. The state class we are creating is what
the composable should return wrapped around `remember` so it can survive compositions, whenever a conf change or a sys-init process death happens we will recreate this state very easily with
the latest persisted top level route, and the state of the substacks for each top level route. But what about the acutal state holder?, the actual state holder is the class I just mentioned
we need to return which encapsulates the three objects I just mentioned, the state holder class is just responsible for exposing the mutable state that represents via a class property
that delegates to the mutable state that is received in the constructor just as a regular property,  the current top level

* **Navigation3 Scene API**: The scene API allows us to achieve adaptive UI, it allows us to create decorator(for displaying navigation UI dinamically), and strategies, for creating
canonical layouts(list-detall, feed layout, supporting pane, three-pane scaffold, find examples in androidx repo, in the [navigation3 examples](https://github.com/androidx/androidx/tree/androidx-main/compose/material3/adaptive/adaptive-navigation3/src/commonMain/kotlin/androidx/compose/material3/adaptive/navigation3)), but not only canonical layout, you can actually create
dialogs(a scene that has composable A on the background and a composable B on top as a dialog, use the nav3 built in `DialogSceneStrategy`), Horizontal pager scene(a scene that lets you
scroll horizontally through different screens like screen A, B and C, as if they where a lazy list but they are main screens that you can scroll through or even just a single page),
you can also try doing the [adaptive layout course/codelab](https://developer.android.com/courses/pathways/android-basics-compose-unit-4-pathway-3) in google Android's documentation,
you can also find very nice examples in the android git profile, in the [nav3-recipes repo](https://github.com/android/nav3-recipes/tree/main/app/src/main/java/com/example/nav3recipes),
a few very interesting samples are, app/src/main/java/com/example/nav3recipes/scenes/listdetail, app/src/main/java/com/example/nav3recipes/navscenedecorator(this may be the "most advance one"),
app/src/main/java/com/example/nav3recipes/multiplestacks, nav3-recipes/app/src/main/java/com/example/nav3recipes/commonui(this one shows how to organize stacks usign a different approach
than the last few mentioned here). This is possible through the `navDisplay`'s parameters(`sceneDecoratorStrategies` and `sceneStrategies`), be aware that the order of these strategies
matter, as the navDisplay will look into each of these strategies in the order they were added to its list to find the right decorator or scene strategy to return. During its search,
navDisplay/navation will look into each strategy and that strategy will let navigation know whether its scene made a match, it works a little different for scene decorators than for
scene stategies, for the latter it relies on the list of `navEntry`s in the current stack that it receives in the parameter of a method of the strategy, the strategy is supposed to
check entries metadata, that metadata is added to each `NavEntry` at the time it was declared, metadata seems to be a key-value map but keys must extend from `NavMetadataKey`, if the stack
contains some `navEntry`s that matches the metadata a given strategy is expecting it will usually forward the instances of the nav antries that matched the metadata to a class implementing the
`Scene` interface, the scene decides how those views are to be displayed, however if it doesn't make a match then it returns null, this way navigation can continue looking in other strategies.
This lets you display the right scene, it usually also relies on the windows size class of the current screen size. Now that we have a scene telling compose what it should display(e.g. list-detail),
it needs to look if there is a decorator that needs to be added around the chosen scene, usually a decorator relies solely on the current windows size class to choose what composable(decorator)
will render. That decorator is also a scene that all it does is add some UI around the already found scene match by the scene strategy, which means you pass the scene to the decorator scene,
using it as a constructor delegator is a nice pattern, in the overriden property `content`(this defines what a scene will render) we add the composable we want and call the wrapped scene
`content` property. This logic implies that navigation first resolve the scene using `sceneStrategies` and then checks for `sceneDecoratorStrategies`, in that order since the scene
returned by the former is decorated in the scene returned by the latter. now for CMP, the

* `rememberSerializable` vs `rememberSaveable` vs `remember`: The first two save objects to `SavedStateRegistry`, which is a low-level Jetpack component that serves as the centralized
bridge for saving and restoring UI state across system-initiated process death and configuration changes. It decouples state preservation from specific lifecycle components like Activities
or Fragments, allowing any custom component to register its own state-saving logic. However, the former uses KotlinX serialization which could be a little less performant than `rememberSaveable`
which uses Parcelable object only, this means the former can be used in CMP and Android, the middle one is available in Android only, The latter saves objects in memory only and can take any
type of object. This means all three can help us persist state across recompositions but the latter can't survive configuration changes and system initiated process death. Check
**Important Navigation3 NavEntry Decorators** as in Navigation3 you need some decorators in order to make some of this APIs work correctly

* **Important Navigation3 NavEntry Decorators**: In navigation 3 is important to know that we need to decorate the NavEntries with at least one decorator, that is
`SaveableStateHolderNavEntryDecorator`, and you obtain an instance of it with `rememberSaveableStateHolderNavEntryDecorator()` function, this decorates our naventries in a way that makes
calls to `rememberSaveable` and `rememberSerializable` work correctly, it seems to provide access to a save state provider. Similarly you almos always want to use `ViewModelStoreNavEntryDecorator`
decorator, which is obtain with the function `rememberViewModelStoreNavEntryDecorator()`, this one requires the previous mentioned decorator to be able to access a `SaveStateHandle` from
a ViewModel which is very common in android development, this decorator provides access to a `ViewModelStoreOwner` in a `CompositionLocalProvider` called `LocalViewModelStoreOwner`
which lets you instantiate viewmodels from a composable in a nav entry aka "content", which means it allows you to scope view models to a `NavEntry`, this changes the composables default behavior
which is that viewModels are scoped to the nearest `ViewModelStoreOwner` which is usually a fragment or activity by default, causing viewmodels to be retained much longer than a composable
lifecycle, it still alive even when the `NavEntry`/composable is not part of the composition, but scoping it to the `NavEntry` changes this behavior and makes sure the VM is cleared whenever
a `NavEntry` is not part of the composition anymore, a good practice would be to scope very specific viewmodels to child composables, for example a small
dialog that launches an interaction with a use case which is not launched anywhere else in the UI, might worth creating a dedicated viewmodel for it which also hold its own state,
and instead of injecting that use case to the "main" composable view model, we could only instantiate a viewmodel for as long as the dialog composable is on screen which can be done
passing a "dedicated" view model store owner, that is created in the desired composable with `rememberViewMOdelStoreOwner`. this works when retrieving viewmodels using koin as well as
just using compose's `viewModel` function. Ok so now we know what nav entry decorators do, but how to use them? well you make a list out of them and then with a `navEntryProvider` which is a
DSL to declare navigation entries, navigation entries are composed of a key and a composable, that key is used to see what is the top key in the stack and match it to the nav entry composable
to render it to the screen, the DSL and the nav entries declared in it are turned into a decorated navEntry list of entries that are decorated with all of the decorators passed in a list
of decorator to the function `rememberDecoratedNavEntries`, it takes three params, first the backstack which is a list of `NavKey`s, that list can be created with any type of list, like `lisfOf`,
`mutableListOf`, however that list wouldn't survive configuration changes if it was modified, but even if it was modified it would cause any recomposition since it is not a state object, so
to do that you'd have to wrap it around a state object and a suitable way to write to the right place, in memory or "saved state registry" depending on if you want to survive recompositions only or
survive configuration changes and system initiated process death also, however it is more easy than that, to get a list that can track only item that have changed, removed or changed its position and
trigger recompositions then just use a `mutableStateListOf`, however that doesn't survive recompositions nor configurations changes nor system initiated process death, so then you would
have to wrap it around the previously mentioned options, `remember` or `rememberSaveable`, however it is easier than that, just create a list that is stored in the correct "saved state registry"
and therefore surviving all scenarios, recompositions, conf changes, system initiated process death, using the funtion `rememberNavBackStack`, that list is what you usually want to pass to the
`rememberDecoratedNavEntries` function, the second param it takes is the list of decorators, the third is the NavKey declaration DSL called `entryProvider`, and at the end all this function does is return
a list of `NavEntry` we can pass to the `NavDisplay` so it knows how to map the current top entry key in the stack to the right composable, however there is a caveat, this returned list doesn't
survive system initiated process death, it only survives conf changes and recompositions, that is why you need make sure that the backstack is either created with `rememberNavBackStack` or is
properly hoisted in something like a viewmodel that saves its state to a "saved state registry", and this also applies to the list of decorators however this last one may not be that critical.
It is important to know that `rememberNavBackStack` used to persist the NavKeys in the stack only works for Android, and for CMP you need to use and overload that also takes a serializer of type
`SavedStateConfiguration` that allows you to handle open polymorphism across all platforms as stated [here](https://kotlinlang.org/docs/multiplatform/compose-navigation-3.html#polymorphic-serialization-for-destination-keys)
which shows how to do "Polymorphic serialization for destination keys﻿"

* ViewModel: is a component that usually encapsulates the communication of the app's UI with lower or inner layers such as domain and/or data layer, it allows us prepare data to be presented
to user, this data represent application state and ViewModel allows to persist it across configuration changes as well as through system-initated process death by using `SaveStateHandle` if
needed, it also provides a safe space to execute suspend functions that don't get interrupted on configuration changes. In compose it can act a state holder to hoist screen level Ui state, in
some cases it could also hoist a specific Ui element state and also perform some UI logic over it, this is usually the case if the UI state needs to interact with buisness logic, i.e., it
could be a chat app that should display contact sugestinons when the user types "@", so we could hoist the Ui element state in the viewmodel in the form of a `mutableState<String>`, and
perform some UI logic from the viewmodel(state owner/state holder) also, the UI logic in this case would be a function that assigns an updated value to the UI state(this would be UI logic),
everytime it changes this launches a check, if the input contains the symbol then we perform some business logic(business logic is the implementation of product requirements) and search
locally or remotely for matches, if they are found the screen level UI state is updated so the UI can render it, that is what the [documentation](https://developer.android.com/develop/ui/compose/state-hoisting#ui-element-state) states. However some [other documentaion](https://developer.android.com/topic/architecture/ui-layer/stateholders#types-state)
states: "UI logic state holder depends on information from the data or domain layers, you should pass that information to it from a business logic state holder. This is because the business
logic state holder is longer lived than the UI logic state holder since it is independent of the UI lifecycle.", again, you can see all depends on your situation, in other words if your
business logic depends on some UI state(meaning it needs to read or write to some UI state) you can hoist the UI state and UI logic in the same Business logic state holder, in most cases,
those business logic state holders(I could call them Screen UI state holders) are viewmodels, and in the same way if a UI logic state holder needs some information from the data layer then it
is just passed to it since Business logic outlives Ui logic. It seems most of developers think your screen UI state should only be one, but it seems that the NowInAndroid app shows something
different, they do combine some flows but a viewmodel could be producing more than one type of UI state, besides it might be problematic trying to emit a new single state from multiple flows
that are not related in any way(combining flows), so insted you could have different state objects and therefore different state reads in your UI, this doesn't seems to be an antipattern and
you should always chose the right tool, and not force your components into a one size fits all solution, and this extactly what is [stated here](https://developer.android.com/topic/architecture/ui-layer#additional-considerations),
only goup states into state objects that are related, you can still have multiple streams if they can be rendered independently from each other, however you can combine stream sources of
state change and one-shot APIs as sources of state changes, as you can [see here](https://developer.android.com/topic/architecture/ui-layer/state-production#one-shot-and). As you can see, there is two "types" of UI
state, Screen UI State, this on usually lives in a VM but it could be a class(state holder), and the other type is UI-element state, the screen UI state is application data transformed by the
ViewModel, or in other words, is what you need to display on the screen. And Ui-element state are the properties intrinsic to UI elements that influence how they are rendered(the visibility,
the input text, enable/disable click). There is also two types of logic, Business logic, which usually changes app data state, thefore changing screen UI state, the vm could be in charge of
applying some filters over it, or combine two different data sources, which is also business logic. These changes are triggered by user input/events aka user interactions with UI components or
external resources like a response from a server. We also have UI logic, which acts over UI state, like changing the color or size of a text based on some value or screen state. Again UI state
can be of two types, but we also said they both can live in the same state holder(if UI element state needs to interact with business logic), either way, we can say UI state is application data
transformed by the ViewModel(state holder).

* Events: In MVI events could be called Intents, and in that context events cause actions, those actions can result in state changes or side effects(navigate to another screen, show a dialog).
However in the context of compose and in the context of Android's [UI layer architecture documentation](https://developer.android.com/topic/architecture/ui-layer/events), events still reperesent user input/actions/intents, however those are UI events, and they say there can be ViewModel events, like when a user clicks to download a file, the user event is the click, it
can cause screen UI state changes, but it will download and when it is completed that can be considered a VM event, they both should cause immediate state changes, it needs to be safe
so using kotlin channels or mutableSharedFlow is wonrg because it is not their nature, we could adapt a shared flow to reply the last messagge but that would make it behave like a state flow
which is exactly why you should use a state flow instead, another option to reduce state changes and "stream" them asap is compose runtime state objects like `mutablesStateList` or `mutableState`, you can expose them with a private setter backing field

* When using a `HorizontalPager` you might like to create a custom LifecycleOwner so that only the visible, settled page is RESUMED, while setting a maxState of STARTED for the adjacent, off-screen pages as [stated here](https://developer.android.com/topic/libraries/architecture/lifecycle#create-custom-lifecycle-owner)

* In fragments and activities we have the component lifecycle and also the view lifecycle, both are represented by an interface called `LifecycleOwner`, but a component's lifecycle can
live longer than the view's lifecycle, the view's lifecycle is known as `viewLifecycleOwner`, the fragment's and activity's lifecycle starts with `onCreate` and ends with `onDestroy`,
the view's lifecycle starts with `onCreateView` and ends with `onDestroyView`, in compose we still have the fragments or activity's lifecycle but there is no view lifecycle,
either a composable is part of the compositon or not, that's its lifecycle, and in compose we can interact with it's host component lifecycle with the following side effects

* **UI tree**, and **UI hierarchy**: Although they might be used interchangeably in other guides, they have different meanings:
  * The Composition is the record of the call graph of composable functions.
  * The UI tree or UI hierarchy is the tree of LayoutNode constructed, updated, and maintained by the composition process.
