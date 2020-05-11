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

> Use Class.asSubclass for safety cast

## Enums and Annotations

## Lambdas and streams
 
## Exceptions
 
Item 69. Use exceptions only for `exceptional` conditions  
  
> They should be never used for ordinary control flow.
> Well designed API should not force the clients to user exceptions for ordinary control flow.
 ```java
 // Horrible abuse fro exceptions, don't ever do this.
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





