# EfectiveJavaTips

1. Introduction  
Tipps from **Effective (Java Third Edition)** Get the book from Amazon for details.
  
2. Creating and Destroying Objects.  
  
2.1 Consider static factory methods instead of constructors.  
  
>BigInteger.valueOf  
>Date.from  

2.2 Consider builder when faced with many constructor parameters  
  
> When facing classes with constructor having lot (>5) of parameters and many optional.
  
2.3 Enforce Singelton with private constructor or an **enum** type  
  
2.4 Enforce Utility Class no instanciability with private constructor  
  
2.5 Prefer dependency injection to hardwiring resources
  
2.6 Avoid creating unnecessary objects

> // example of creating unnecessary objects (outbox)  
> Long sum = 0L;  
> for (long i = 0; i <= 1_000_000L; i++) sum += i;  
> return sum;  
  
2.7 Eliminate obsolate object references  
  
> With note that nulling out object references should be an _exception_ rather then the norm  
> Possible memory leak causes: 
> * class manage its own memory (ex: array)
> * cache
> * listeners and other callbacks (use WeakHashMap)
  
2.8 Avoid finalizers and cleaners  
  
2.9 Prefer try-with-resources to try-finally
  
> Have your class implement AutoClosable when needed.

  


  





