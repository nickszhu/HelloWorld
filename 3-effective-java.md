# General Programming

### Scope of Local Variables

Use local variable with minimal scope:
* Declare the scope of a local variable where it first used
* Initialize every local variable
* Prefer for-loops to while-loops
* Keep method small and focused on single task

### For-each loop vs For loop
Use for-each loop or enhanced for loop:
* readability and maintainability
* less likelihood of errors

### Use libraries 
Advantage of libraries over your code:
* Knowledge of expert
* New features are added in major release
* Better performance

### Float, Double, Exact Calculations
Use `int`, `long`, or `BigDecimal` for exact calculations because `float` and `double` are carefully designed for accurate **approximations**

### Primitive Types vs Boxed Primitive
Use primitive types:
* Better performance, because boxed primitive types need repeatedly boxed and unboxed operations
* When unboxing, it can throw a `NullPointException`
* When boxed primitives are used, `==` operator is almost wrong and hard to debug

### String vs other Types
Avoid using `String`, it is poor subsititues for other value, aggregate, or capacity type.

### StringBuilder vs String Concatenation
Avoid String concatenation, because of its poor performance

### Interface and Class Reference
Use interface to refer to parameters, return values, variables and field. Use least specific class type if no appropriate interface type.
* more flexible
* backward-compatible

### Optimization
* Good programs rather than fast program
* Avoid decisions that limit performance, because once decisions are made they hard to be changed or optimized later
* Measure the performance carefully before and after optimization (e.g. use profiling)

### Naming Conventions
* lower case for packages or modules
* title case for classes and interfaces
* camel for method name, fields, local viarable
* upper ase for constant 
* one capital letter for type parameters

# Creating and Destroying Objects

### Static Factory Methods and Constructors
Use static factory methods (e.g. `Date.from()`):
* they have name
* no new object each time they are invoked
* they can return an object of any subtype. more flexibility to change implementations of subtypes from release to release, without breaking backward compatibility.
* decouple service provider frameworks from implementation providers.

### Builders and Contructors
buildler:
* make client code much easier to read and write

### Noninstantiability
**Without a private constructor** the class is inaccessible outside and cannot be subclassed.

### Dependency Injection
Dependency injection would improve flexibility and testability compare to static utility and singleton.

### Try-with-resources vs Try-Finally
Use try with resources:
* close resources
* shorter, readable, diagnostics


# Classes
### Accessor vs Public fields
Avoid using public fields:
* cannot change its representation

### Immutability
In generall, classes should be immutable by:
* Don't provide methods that modify the state of objects
* Ensure class can't be extended, to prevent careless or malicious subclass from compromising immuatability
* Make all field final to express your intent
* Make all fields private to prevent client from obtaining access
* Ensure exclusive access to any mutable components.

Benefits of immutability:
* Immutable objects are simple because only one state, providing failure atomicity for free
* inherently thread-safe
* can share immutable objects freely
* immutable objects make great building blocks for other objects

Disadvantage of immutability:
* require a separate object for each distinct value.
* need to provide supporting classes (e.g. `StringBuilder` for `String`)

### Inheritance vs Composition
Inheritance violates encapsulation. It is appropriate only when:
* a genuine subtype relationship exists between the subclass and superclass.
* both of them are in the same package
* the superclass is desinged for inheritance

Use of composition and forwarding is usually more robust and more powerfull than that of inheritance.

### Inheritance Documentation
If you decide that a class can be inherited then you must document its self-use of overridable methods.
Designing and Implementing inheritance are difficult because lifelong support.

### Interface Design and Posterity
Best practice when designing an interface:
* choose method names meaningfully and carefully
* don't go overboeard in providing convenience methods because maintaining public methos is costly.
* avoid long parameter list (<=4)
* for parameter types, favor interfaces over classes
* prefer two-element Enum types over `boolean` parameters, more meaningful and extensible.

### Static and Non-Static Member Classes
If you declare a member class that doesn't require access to its enclosing instance then always put `static` modifier in its declaration. Otherwise, each instance will have a hidden extraneous reference to its enclosing instance, which takes time and space. More seriously, causing catastronphic memory leak.
