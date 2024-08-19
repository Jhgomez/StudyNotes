## Inline Functions
This feature has to be used with careful since it could lead to more memory usage because when specified in a function the compiler instead of calling and executing the function at runtime it will copy the function call at the call site, you should use this with higher-order functions which are functions that accept other functions which is when we'll mostlikely have a performance gain. This eliminates the overhead of function calls. Use it when a large

## Inline Classes

## Kotlin Functions
They are first class citizens, meaning they can be anywhere, they can be assigned to variables, pass as parameters, pretty much treated as objects. Its possible since all functions return a value which if not define return type is Unit by default.

## Higher-order Functions and Lambdas
As kotlin is a statically typed language(see computer science) and functions are first class citizens, functions can be assigned anywhere as variables, parameters, function return values. Its all possible thanks to the existence of a family of function types to represent functions

## Functions Types
They are used by kotlin to represent functions as a data type/object. Example: val funOne: (Int) -> String = { "" } They can have annotations like @composable before the function parameter and also a receiver type so this is equivalent: SomeScope.() -> Unit equivalent to (SomeScope) -> Unit the previous declaration is similar to an extension function. They can have the suspend before the type. You can give function types a name using type type alias, for example:     typealias custom = (Int, Button) -> Unit The following declaration are equivalent 
- fun example(m: String): String { return m }
- val example: (a: String)  -> a

## Higher order functions
Functions that take functions as parameters or returns a function. 

## Top Level Functions
Functions that exists inside a kotlin package but outside any class/object/interface. No need to instantiate an object to call these functions. They are useful for defining helper or utility functions. In java
these would be static functions inside a helper class. 

## Lateinit vs. Lazy
Lateinit allows us to postpone the initialization of a property until a later time while lazy initializes the property only is first accessed.

## Const vs val vs @JvmField

* **Const vs val**: Both define variables which value can not change after they are assigned, however const can only store primitive values, its value has to be defined at compile time(it can only hold strings and primitives) and it can only be defined/declared inside an object or as a top level variable(outside a class/object/interface). val value can be assigned at runtime but only once and it can be declared anywhere(class/interface/object/top level)
	
* **Const vs @JvmField**: Const characteristics are mentioned above so @JvmField characteristics are: it can declare var or val variables, It can be declared anywhere(top level/class/object) except interface, **what it does is it tells the compiler to expose the variable as a field instead of a property**(all kotlin class variables are exposed as properties meaning they'92re automatically generated a getter/setter at compile time), a field doesn't have generated getters or setters and it doesn't have any restriction on the type of object it holds.

## Jvm Annotations

* **@JvmStatic**: Tells the compiler the method is a static method and can be used in java code. Most likely you will be annotating a method inside a companion object

* **@JvmOverloads**: You can annotate a constructor or a method and this will tell the compiler how call default parameters(if defined) when calling the method from java code.

## Serializable vs Parcelable
* **Serialization**: Is the process of converting an object into a stream of bytes in order to store it into memory so it can be recreated at a later time while keeping the object'92s original state and data
	
If we declared a variable '93transient'94 it won'92t be serialized

* **Parcelable**: Serializable is a standard Java interface. Parcelable is an Android specific interface where you implement the serialization yourself. It was created to be far more efficient than serializable.

## Generics(Type Parameters)
Java and Kotlin can have Generics, type parameters(List<T>) are invariant meaning List<Sting> is not a subtype of List<Object>. They allow us to reuse code with different object types, however to
 increase this flexibility even further we can use variance. In Java, we can implement it by using Wildcard types(?, ? super E, ? extend E). In Kotlin we can define variance at the '93declaration site'94(this feature 
is usually called declaration-site variance) using '93type projections'94, type projections make use of '93variance annotations'94 and there are three of the annotations, one for each variance use
 case. There are two types of variance essentially(variant and invariant), however there is three '93use cases'94 of the variance variant type  and those are the following
	
	//Generics(They are invariant by nature)

	Invariant(invariant)- Defined inside angle brackets '93<T>'94. This means '93List<Number>'94 can not contain a '93List<Integer>'94, however in java you can use bounded type parameters as follows
	'93ClassWithGenerics<T extends Number>'93 in kotlin you can do this with '93ClassWithGenerics<T: Number>'94. In java using type parameters will let the compiler infer the type so you can access methods
	and properties/fields of the defined type however when using wildcards inferring the type is more '93complex'94

	// Wildcards(Java) or Variance Annotation(Kotlin)
	
	Unbounded(Variant) - In Java '93List<?>'94, in Kotlin '93List<*>'94 If you read from any object that is using this wildcard you will get an '93Object'94 type reference and you will not be able to write to it since the compiler
	wouldn'92t be able to guarantee runtime safety the behavior in Kotlin is the same with the difference that it will read it as '93Any?'94 type object.

	Covariant(variant) - In Java it is defined like the following '94<? extends AnyClass>'94 and is called upper bound wildcard, you can only read from it and it will read the type of object that you define. You will get a
	compiler error if you try to write to an object with this wildcard since compiler can not know what type of object you are actually reassigning/adding. In Kotlin this is possible with the '93out'94 keyword '93<out AnyClass>'94
	and again, you can only read from it just like in java, it has the same behavior

	Contravariant(variant) - In java it is defined as follows '93<? Super AnyClass>'94 and is called lower bound wildcard, you can write to it 
f3b only
f0b0  the type of objects defined in the angle brackets  and you can also
	read from it but you will be reading '93Object'94s. In Kotlin you write it with '93<in AnyClass>'94 and you can do the same as in Java but if you read from it will get an object of type '93Any?'94

	Declaration-site Variance
	Is a Kotlin feature that lets you inform the compiler wether your type parameter is Covariant/producer or Contravariant/consumer, basically it is the equivalent to wildcards in Java as explained above
	with the difference that you can '93enforce'94 a type parameter of a class or method to only be covariant or contravariant by specifying the variance annotation in the declaration of the class or method, the only difference
	with this approach in contrast to Java'92s approach is that the compiler wouldn'92t let a class consume values of a type parameter if that type parameter is declared as producer(covariant)

	Use-site Variance
	Basically this is the same place and behavior as Java wildcards

Refied
This has to be used in conjunction with '93inline'94. Inline copies the code of the function without creating a function type object to every calling site and only inline functions can have '93reified'94 type parameters declared. This
will hold the parameter type and is most likely useful if we need to check the type of object or do some introspection of the class of the type

Statements vs Expressions
Statements are used to execute code as we do in Java for example however they can also be used as expressions which means they can assign values to a variable, expressions are used to improve code readibility

Safe Call Operator (?.)
It is used to safely call methods on a variable that is nullable, any attempt of calling a method on a nullable variable with '93null'94 value will return null, this will avoid the program to crash

Not Null Assertion (!!.)
Should be used to call methods on a nullable variable but we'92re completely sure the value is not null since a '93NullPointerException'94 will be thrown if it is null causing the program to crash

Elvis Operator(?:)
We use this operator to assign a default value, throw an exception or use the '93return'94 keyword when a nullable value calls a function, the purpose of doing so is to avoid null pointer exceptions crashes

ReadWriteProperty<T, V> / Property Delegator
This interface lets you create a class that then can be used to delegate the '93setter'94 and '93getter'94 methods of a property to the implementation declared in this class. You have to create the class, implement this interface and override the getValue and setValue methods and then just delegate to a any property in a class which has access to the class that implements this interface using the '93by'94 keyword before instantiating the object










}