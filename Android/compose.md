
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
nav rails and expanded nav rails. Usually what you want is compose to be able to track the state changes of a list that survives recompositions, configuration changes and systgem
initiated proess death, this is possible by using the "old concept" of "saved state"/"saved state registry" 

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

