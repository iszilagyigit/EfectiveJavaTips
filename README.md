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
> Don't provide methods that modify the object's state  
> Ensure that the class can't be extended  
> Make all fields final  
> Make all fields private  
> Ensure exclusive access to any mutable components  
  
  






