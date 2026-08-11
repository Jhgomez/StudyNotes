
* NavigationSuiteScaffold vs SceneDecoratorStrategy: Both APIs helps us achieve adaptive layouts, the former seems to only be available in Android and not CMP and is part of the
`androidx.compose.material3.adaptive.navigationsuite` package, so it is not exactly part of a navigation library on itself however it integrates well with any navigation library,
the latter is available in CMP and is part of the `androidx.navigation3.scene.SceneDecoratorStrategy`, as you can see is part of navigation's 3 Scene API, the scene API seems to
be more flexible however a little bit more difficult to configure, what we need to understand is what these two APIs helps us to achieve in adaptive layout, and that is displaying
the right navigation UI, which could be a navigation bar(bottom), a navigation rail, or a persistent/expanded navigation drawer, in material 3, that last one is not recommended
anymore, instead you should use an expanded navigation rail. The former API basically "automates" this process, however the former seems to be more "flexible" and can be implemented
across all CMP targets.

* Navigation3 Scene API: The scene API allows us to achieve adaptive UI, it allows us to create decorator(for navigation UI), and strategies, for creating canonical layouts(list-detall,
feed layout, supporting pane, three-pane scaffold, find examples in androidx repo, in the [navigation3 examples](https://github.com/androidx/androidx/tree/androidx-main/compose/material3/adaptive/adaptive-navigation3/src/commonMain/kotlin/androidx/compose/material3/adaptive/navigation3)),
you can also try doing the [adaptive layout course/codelab](https://developer.android.com/courses/pathways/android-basics-compose-unit-4-pathway-3) in google Android's documentation,
you can also find very nice examples in the android git profile, in the [nav3-recipes repo](https://github.com/android/nav3-recipes/tree/main/app/src/main/java/com/example/nav3recipes),
a few very interesting samples are, app/src/main/java/com/example/nav3recipes/scenes/listdetail,
app/src/main/java/com/example/nav3recipes/navscenedecorator(this may be the "most advance one"), app/src/main/java/com/example/nav3recipes/multiplestacks,
nav3-recipes/app/src/main/java/com/example/nav3recipes/commonui(this one shows how to organize stacks usign a different approach than the last few mentioned here). But this is only for
Android, now for CMP
