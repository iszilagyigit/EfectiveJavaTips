# EfectiveJavaTips

## Introduction  
Tipps from **Effective Java (Third Edition)** Get the book from Amazon for details.
  

## Creating and Destroying Objects.  
  
Item 1. Consider static factory methods instead of constructors.  
  
>BigInteger.valueOf  
>Date.from  

Item 2. Consider builder when faced with many constructor parameters  
  
> When facing classes with constructor having lot (>5) of parameters and many optional.
  
Item 3. Enforce Singelton with private constructor or an **enum** type  
  
Item 4. Enforce Utility Class no instanciability with private constructor  
  
Item 5. Prefer dependency injection to hardwiring resources
  
Item 6. Avoid creating unnecessary objects

```java
// example of creating unnecessary objects (outbox)  
Long sum = 0L;  
for (long i = 0; i <= 1_000_000L; i++) sum += i;  
return sum;  
```

Item 7. Eliminate obsolate object references  
  
> With note that nulling out object references should be an _exception_ rather then the norm  
> Possible memory leak causes: 
> * class manage its own memory (ex: array)
> * cache
> * listeners and other callbacks (use WeakHashMap)
  
Item 8. Avoid finalizers and cleaners  
  
Item 9. Prefer try-with-resources to try-finally
  
> Have your class implement AutoClosable when needed.
 

## Method common to all Objects
  
Item 10. Follow the contract when overriding **equals**
  
> See _Object.equals_  
(https://docs.oracle.com/javase/8/docs/api/java/lang/Object.html#equals-java.lang.Object-)  
> reflexive, symmetric, transitive, consistent  

Item 11. Always override **hashCode** when you override **equals**
  
Item 12. Always override **toString**
  
Item 13. Override **clone** judiciously
  
Item 14. Consider implementing _Comparable_ interface
  
## Classes and Interfaces  
  
Item 15. Minimize the accessibility of classes and members  
  
> Access levels preference: private, package-private, protected, public 

Item 16. In public classes use accessor methods not public fields.  
  
Item 17. Minimize **_mutability**_  
    
Example immutable classes: String, BigInteger.  
For "future" java versions (12+?) see also "value class"  
https://www.oracle.com/technetwork/java/jvmls2016-goetz-3126134.pdf
  
> Rules for immutable class:  
> * Don't provide methods that modify the object's state  
> * Ensure that the class can't be extended  
> * Make all fields final  
> * Make all fields private  
> * Ensure exclusive access to any mutable components  
  
Item 18. Favor composition over inheritance  
  
> See also "Head First: Design Patterns"
  
Item 19. Design and **document** for inheritance or else prohibit it  
  
Item 20. Prefer interfaces to abstract classes  
  
Item 21. Design interfaces for posterity
  
## Generics
  
Item 26: Don't use raw types.
  
> For example raw type corresponding to List<E> is List  

Item 27: Eliminate unchecked warnings

> If you can't eliminate and you can prove that the code is typesafe *only then* @SuppressWarnings
 
Item 28: Prefer lists to arrays

> arrays are covariant and reified (enforced by runtime), generics are invariant and erased (by compiler!)
> in case type safety is more impotant as performance

Item 29: Favor generic types

Item 30: Favor generic methods

Item 31: Use bounded wildcard to increase API flexibility.

> while generics are invariants
> for producer use extends for consumer use super

Item 32: Combine generics and varargs judiciously

> Dont do it :-)

Item 33: Consider typesafeheterogeneus containers

> Use Class.asSubclass for safety cast on generics

## Enums and Annotations

Item 34: Use Enums instead of int constants
 
> Implement the toString() method. 
> Any time you need a set of constants whose members are known at compile time.
> Consider "constant-specific" method implementation if needed
> see also strategy-enum pattern
 
Item 35: Use instance fields instead of ordinals

> It was designed for internal use on EnumSet and EnumMap
> Never derive a value of the enum from ordinal.

Item 36: Use EnumSet instead of bit fields.

> Ex: text.applyStyles(EnumSet.of(Style.BOLD, Style.Italic))

Item 37: Use EnumMap instead of ordinal indexing.

> Ex. Map<Enum1, X> enumMap = new EnumMap<>(Enum1.class)

Item 38: Emulate extensible enums with interfaces.
 
> Ex. public enum X implements Interface1

Item 39: Prefer annotations to naming patterns

Item 40: Consistently use the Override annotation
 
> use it in every method that you believe to override a superclass annotation
 
Item 41: Use marker interfaces to define types


## Lambdas and streams
 
Item 42: Prefer lambda to anonymous classes

> Omit the types of all lambda parameters unless the presence makes your code clearer
> Lambda lack names and documentation; if computation isn't self explanatory or exceed few lines don't put it in lambda.

Item 43: Prefer method reference to lambda

> Example: map.merge(key, Integer::sum)
> Where method reference is shorter and clearer use them, otherwise stick with lambdas
> Examples:
> * Integer::parseInt    str -> Integer.parseInt(str)
> * String::toLowerCase  str -> str.toLowerCase()
> * TreeMap<K,V>::new    () -> new TreeMap<>()
> * int[]::new           len -> new int[len]

Item 44: Favor the use of standard functional interfaces.(java.util.function.)

> Examples: 
> * Predicate<T>  boolean test(T t)
> * Function<T,R) R apply(T t)
> * Supplier<T>   T get()
> * Consumer<T>   void accept(T t)
> * UnaryOperator<T> T apply(T t)
> * BinaryOperator<T> T apply(T t1, T t2)
>   
> Use primitive functional interface instead of basic functional interface
> Always annotate your functional interface with @FunctionalInterface annotation
  
Item 45: Use streams judiciously

> overusing streams makes program hard to read and maintain
> name carefuly the lambda parameter to increase the readability of stream pipeline
> using helper method is even more important for readability then in iterative code

Item 46: Prefer side effect free functions in streams

> essence of stream pipelines are side effect free function objects. The terminal operation
> forEach should inly be used to report the result, not for calculation.
> You need to know about collectors. The most important collector factories are:
> toList, toSet, toMap, groupingBy

Itemp 47: Prefer Collection to Stream as a return type

> Collection or an appropiate subtype is generally the best return type for public 
> sequence returning method, but do not store large sequence in memory ust to return it
> as a collection.

Item 48: Use caution when making streams parallel

> Parallelizing a pipeline is unlikely increase its performance if th esource is from *Stream.iterate*
> or the operation *limit* is used. Performance gain is the best on streams over ArrayList, HashMap,
HashSet, ConcurrentHashMap, arrays; int ranges and long ranges.

## Methods

Item 49: Check paramters for validity

> Each time you write a public method or constructor think about what restrictions exists on its parameters.
> See also Objects.requireNonNull or custom @NonNull @Nullable annotations.

Item 50: Make defensive copies when needed

> If a class has mutable components that it gets from or returns to its clients, the class must defensively
> copy those components. If the cost of the copy would be prohibitive and the class trust its clients not to modify
> the components inappropriately, then the defensive copy may be replaced by documentation.

> Do not use clone method to make defensive copies by non final classes.

Item 51: Design method signatures carefully

* Choose method names carefully
* Don't overboard with convenient methods. When in doubt, leave it out.
* For parameter types favor interfaces over classes
* Prefer two element enum instead of boolean unless the meaning is clear from method name.
* Avoid long parameter list. Preferable less then 4
1) to break the method in multiple methods
2) use helper klass to hold group of parameters
3) adapt the Builder pattern from Object creation to method invocation

Item 52: Use overloading judiciously

> selection among overloaded methods (same name oder parameters!) is static (compile time),
> while selection over overridden methods is dyanmic(runtime)

example:
```java
Set<Integer> set = new TreeSet<>();
List<Integer> list = new ArrayList<>();
for (int i = -3; i < 3; i++) { set.add(i);list.add(i);}
// remove postive elements:
for (int i = 0; i < 3; i++) { set.remove(i);list.remove(i);}
System.out.println(set + " " + list);
// prints [-3, -2, -1][-2, 0, 2] Because of overloaded remove method.
// Correct would be  list.remove((Integer)i); or list.remove(Integer.valueOf(i));
```
* Do NOT overload methods to take DIFFERENT functional interfaces in the same argument position.
* A safe conservative policy is never to export overloading with the same number of parameters.

Item 53. Use varargs judiciously

> Precede the varargs parameter with any required parameters, and be aware of the performance consequences 
using varargs.

Item 54. Return empty collections or arrays, instead of not nulls.

> Don't return null in place of empty array or collections.



## Exceptions
 
Item 69. Use exceptions only for `exceptional` conditions  
  
> They should be never used for ordinary control flow.
> Well designed API should not force the clients to user exceptions for ordinary control flow.
 ```java
 // Horrible abuse from exceptions, don't ever do this.
 try {
   while (true) range[i++].climb();
 }catch (ArrayIndexOutOfBoundException e) {...}
```
Item 70. Use checked exceptions for `recoverable` conditions and runtime exceptions for programming errors.
  
> By confronting the user with checked exception, the API designer presents a mandate to recover from the condition  
> The great majority of runtime excetions in java indicate `precondition violation`  
> One problem with this advise is that it *is not always clear* wheater your are dealing with recoverable condition or programming error.  
> If is not clear wheather recovery is possible you are probably better using unchecked exceptions. (see Item71)
  
Item 71. Avoid unnecesarry use of checked exceptions
  
Item 72. Favor the use of standard exceptions.  
  
> zB. IllegalArgumentException, IllegalStateException, IndexOutOfBoundException, UnsupportedOperationException
> makes your API easier to learn and use because use conventions that programmers are familiar with
  
Item 73. Throws exceptions appropiate to the abstraction
  
> While `exception translation` is superior to mindless propagation of exceptions from lower layers, `it should not be overused`
  
Item 74. **Document** all exceptions thrown by each method
  
> Use the javadoc @throws tag to document each exception can throw but **do not use the throws keyword on unchecked exceptions**
  
Item 75. Include failure capture information in detail message
    
Item 76. Strive for failure atomicity  

> A failed method invocation should leave the object in the state that it was in prior to the invocation
  
Item 77. Don't ignore exceptions

```java
// Empty catch block ignore exception - Higly suspect!
try {
...
}catch (SomeException e) {};
```






