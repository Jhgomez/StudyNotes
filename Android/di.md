# Dagger
Dagger dependencies are satisfied by declaring bindings. These bindings tell Dagger how to create new instances of a dependency. The two most common ways to 
declare bindings are using `@Inject`-annotated constructors and `@Module` binding methods(`@Povides`, `@Bidns`). I will talk more about different concepts but
be aware that the classes that dagger can inject to other classes are called bindings, these bindings can be scoped or unscoped, unscoped binding are bindings
that are not cached meaning they are instantiated everytime we inject it to a class, they are the bindings generated from constructors 
(see [@Inject bindings](#@Inject-bindings)), scoped bindings are created through modules, these modules are added to scoped components using annotations, and is 
the components the objects we use to access/create the dependency graph, inside components you can have a subcomponents which creates a hierarchy, each component can
have its own bindings. Child components can access parent's bindings but not the way around, siblings components can not access each other's bindings without
declaring the other component as a dependency. The components can be scoped or unscoped, scoped components allows us to cache instances of the bindings, but
is our responsibility to use them correctly so we can give sense to the scope name, for example we should only instantiate the singleton component once in our
application, even thought we can instantiate it multiple times but if we do it is not a singleton component, the modules added to scoped components can only be
unscoped or scoped (it has to match the scope of the component that it will be added to). Btw, scopes are just annotations. Unscoped component doesn't seems to
have much of a purpose but you can create them. So the relationship we have is ( "->" means lives in), "unscoped bindings" -> anywhere (because dagger just knows
how to create instances of these classes but each call to this bindings create a new instance, so they can be injected to other bindings, an instance of it can
be turned into a scoped binding if declared inside a module), "scoped bindings" -> modules -> components, but also implicit "scoped bindings" can be created if
they are added directly in the component, using either a constructor binding (a constructor annotated with @Inject but also annotated with the scope) and creating 
a function that returns it inside the component (it would be an abstract function) this creates an implicit scoped binding but the scope annotation in a class
only works in this scenario, it doesn't has any effect inside a module unless the binding is annotated with the scope, the other way to create an implicit binding
is using a builder factory in your component (an inteface annotated with `Component.Factory` can declare a method with parameters annotated with `@BindsInstance`
this creates an implicit scoped binding, btw this last option is used to pass objects that we can not create but want to inject into the graph. Lets see more
info in detail

## Ways Of Declaring Bindings vs Ways of Getting Existing Bindings Injected into a class(Injecting dependencies)
You can declare bindings using any of these methods

* Using `@Inject` in constructors
* Using `@Provides` and `@Binds` in modules(classes or interfaces that are annotated with `@Module`)
* Creating an abstract method directly inside a component returning a scoped annotated or unscoped class with a constructor binding (this is the only way adding
scope annotations to a class have effect otherwise the annotation is just some sort of documentation)
* Injecting through a component's factory using an abstract method inside the factory. This is truly an implicit scoped binding (if the component is annotated
with a scope)
* A module can include other modules which grants access to the bindings declared in the included module to the hosting module.

TODO explain maps and sets

You can consume the bindings with any of the following methods
* Field Injection, this requires your component to create an abstract method with the class that contains the injected fields as a parameter, you then should
  use an instance of the component that contains the method and call the method passing the reference to the class that you want to inject the bindings to.
  Another way to do this field inejction is using `MembersInjector<AClassWIthFieldInjection>`, for this you declare an abstract function in the component like
  `fun pluginInjector(): MembersInjector<AnalyticsPlugin>`
* You can also create abstract methods inside the component, that returns the bindings that where declared in its modules, and then using the instance of the
  component call those methods, but also the methods adding a binding directly to the component as mentioned above.
* But the previous ways of consuming bidngs is only possible in classes where an instance of the component exists and therefore is the entry point to a component's
  graph at runtime, this is needed because a framework entry point (a class that you may define but you don't instantiate, is the framework who isntantiate it like
  an activity or the main method in java) may have fields that need to be injected or just generate instances of bindings, is what I talked about in the previous
  points. But in classes where creating an instance of the component is not practical or doesn't make sense, we can use constructor injection,
  you just need to declare the bindings you need inside a constructor that is annotated with `@Inject`
* You can modify the behavior of how a binding is provided when consumed by wrapping the binding inside provision method, these are explained a little more
  [here](https://dagger.dev/api/latest/dagger/Component.html#provision-methods). These are `Provider<T>` and `Lazy<T>`, the type param represents the binding
  type which can be scoped or unscoped, if scoped the behavior is basically the same for both since they have to respect the scope so a single instance is
  created lazily with either or and then this same instance is returned whenever `get()` is called, but for unscoped bindings this you can really see the
  difference, `Provider` returns a new instance everytime `get()` is called on the provider (even on the same instance of provider) but `lazy` only returns
  one instance per instance of `lazy` this means that different instances of `lazy` generates differents instances of the binding but both, `Lazy` and `Provider`,
  instantiate the class lazily. A provider can contain a lazy method

TODO explain field injection, constuctor, function, Provider, Lazy and MembersInjector

## @Inject bindings
Annotating a class’s constructor with @Inject is the simplest way to define a binding for a particular type. The `@Inject`-annotated constructor tells Dagger 
to use the class’s constructor when creating new instances of the class. These bindings are unscoped, which means anytime we request an instance of the class
a new instance is created, I'll talk more about scopes and components, these binding are don't live inside a component. Basically scopes are just annotations 
we add to a component, it serves two purposes, first it can be used for "documentation" if added to a class that is providing a binding to the graph of a 
scoped component it just tells whoever is reading the code that the class lives in the component using the same scope, in the context of an unscoped binding
using `@Inject` in the constructor this means that we actually have turned that unscoped binding into a scoped binding declared by declaring a binding in a
module using `@Binds` or `@Provides` and annotating that binding with the same scope, what scopes allows us to do is to cache instances of the bindings but 
only if those bindings are annotated of course, you can also declare an unscoped binding that reference an unscoped constructor binding but that doesn't make
much sense and you would just rather leave that class outside the compoent as dagger will know how to instantiate those classes but will produce a new instance
everytime you inject that binding into another binding or a class consuming bindings. So what you need to know is that constructors annotated with `@Inject`
adds an unscoped binding to dagger, it means it will know how to create an instance of the object whenever you request it and everytime you request this object
a new instance is produced, any component annotated with whatever scope is annotated with can consume this bindings, btw a component can be unscoped also, 
but it means it can only consume unscoped bindings meaning that it will produce a new instance of whatever object it declared bindings for meaning that declaring
an unscoped component doesn't even makes any sense instead you would rather just declare the constructor binding, and also know that a constructor unscoped binding
can only consume other unscoped bindings, this means you can not declare a dependency on a scoped binding in a constructor unscoped binding.

## @Povides, @Binds inside modules
A module is either a class, object(specific to kotlin, it is a singleton class), interface or abstract class that is annotated with `@Module`. `@Provides` and
`@Binds` is the way you add bindings in a module. `@Binds` is the preferred way to declare bindings because Dagger only needs the module at compile time, and 
can avoid class loading the module at runtime. `@Binds` can only be declared in abstract methods and therefore the modules where they're declared can only be 
interfaces or abstract classes, not loading a class is delivers more performance. Everything that `@Binds` does can be done with `@Provides` but not the way 
around, this is becasue, as mentioned, `@Binds` are abstract methods and therefore don't have a body, that is why `@Provides` is the only way to inject objects
from a third party lirbary or SDK which we can instantiate on demand but we can't modify the class declaration source code. One interesting way of using
`@Binds` is you can explicitly declare a binding in a module using a zero-parameter `@Binds` method but only if the class constructor is annotated with `@Inject`.
You can turn an uscoped binding that is declared only using its constructor that is annotated with an `@Inject` into an effectively scoped binding if you declare
the a binding with a scoped annotation inside a module, the unscoped binding turns into a effectively scoped binding inside the component and when consumed inside
the component where the module lives. Bewary the paremeterles binding `@Binds` method cannot be scoped or qualified, and the return type cannot have a scoped 
`@Inject` constructor.

## Components
A component can have a scoped or not, if it has a scoped its modules can only declare bindings with the same scope or unscoped bindings. Components may have multiple 
scope annotations applied. This declares that they all refer to the same scope, and so that component may include scoped bindings with any of the scopes it declares.

It is your responsibility to add instnatiate components correctly. That means, for example with a component with the singleton scope, that you should instantiate it
in a class that lives throught the application life cycle, in android that is the application class. You could miss use such component if you instantiate it more than
once, it wouldn't be a singleton

## More Ways To Manage Bindings
### @Qualifier
Sometimes we have more than one implementation of a class that we want to inject but we don't want to be injected as the implementation, instead just the interface
and if we have two implementations this can be conflicting, but we can use the `@Qualifier` annotation, but we need to create our own qualifiers. A qualifier is
any annotation that itself has a @Qualifier annotation, this means we need to create our own annotations, in Java we do

```
@Qualifier
@Documented
@Retention(RUNTIME)
public @interface Named {
  String value() default "";
}
```

in Kotlin 

```
@Qualifier
@Retention(AnnotationRetention.RUNTIME)
annotation class ContextDispatcher(val dispatcher: Dispatcher)
```

There is actually a built in Qualifier, `@Named`, in filed injection is used like `@Inject @Named("water") Heater waterHeater;`. and in binding you use them like

```
@Provides 
@Named("hot plate") 
fun provideHotPlateHeater(): Heater {
  return ElectricHeater(70)
}
```




