# Dagger
Dagger dependencies are satisfied by declaring bindings. These bindings tell Dagger how to create new instances of a dependency. The two most common ways to 
declare bindings are using `@Inject`-annotated constructors and `@Module` binding methods(`@Povides`, `@Bidns`).

## Ways Of Declaring Bindings vs Ways of Getting Existing Bindings Injected into a class
* Using `@Inject` in constructors
* Using `@Provides` and `@Binds` in modules(classes or interfaces that are annotated with `@Module`)

## @Inject bindings
Annotating a class’s constructor with @Inject is the simplest way to define a binding for a particular type. The @Inject-annotated constructor tells Dagger 
to use the class’s constructor when creating new instances of the class. These bindings are unscoped, which means anytime we request an instance of the class
a new instance is created, I'll talk more about scopes and components, but basically scopes are just annotations we add to a component, it serves two purposes,
first it can be used as "documentaiton", you add this to classes that are being injected into the graph or classes that are being injected classes into its
fields, for example
a helper class 

