# Dagger
Dagger dependencies are satisfied by declaring bindings. These bindings tell Dagger how to create new instances of a dependency. The two most common ways to 
declare bindings are using `@Inject`-annotated constructors and `@Module` binding methods(`@Povides`, `@Bidns`).

## Ways Of Declaring Bindings vs Ways of Getting Existing Bindings Injected into a class(Injecting dependencies)
You can declare bindings using any of these methods

* Using `@Inject` in constructors
* Using `@Provides` and `@Binds` in modules(classes or interfaces that are annotated with `@Module`)

TODO explain maps and sets

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
A module is either a class, object(specific to kotlin, it is a singleton class), interface or abstract class that is annotated with `@Module`, but you should
prefer interface or abstract class because when you use them Dagger only needs the module at compile time which means it doesn't need to load the class at 
runtime which also means that `@Bind` should be preferred over `@Provides`, everything that `@Binds` does can be done with `@Provides` but not the way around,
you'll understand why in a second. 
