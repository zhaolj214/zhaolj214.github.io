---
layout: post
title:  "java generics and collections"
categories: 
tags: java generics
author: 若水三千
---

* content
{:toc}

###2.1 Subtyping and the Substitution Principle###

> <i>**Substitution Principle**</i>: a variable of a given type may be assigned a value of any subtype
of that type, and a method with a parameter of a given type may be invoked with an
argument of any subtype of that type.

So List<Integer> is not a subtype of List<Number>, nor is List<Number> a subtype of
List<Integer>; all we have is the trivial case, where List<Integer> is a subtype of itself,
and we also have that List<Integer> is a subtype of Collection<Integer>.

Arrays behave quite differently; with them, Integer[] is a subtype of Number[].

```java
    Integer[] ints = {1, 2, 0,};  
    Number[] nums = ints;   
    nums[2] = 3.14;  
```

> have a run-time error: Exception in thread "main" java.lang.ArrayStoreException: java.lang.Double

when we would like lists to behave more like arrays, in that we want to accept not only a list with elements of
given type, but also a list with elements of any subtype of a given type. For this prupose, we use `wildcards`.

###2.2 Widcards with extends###

? extends E means any type that is subtype of some type E. In general if a structure contains elements with a type of form ? extends E, we can get elements out of the structure, but we can't put elements int the structure.


###2.2 Widcards with super###

? super E means any type that is supertype of E.

```java
    public static <T> void copy(List<? super T> dst, List<? extends T> src) {
        for (int i = 0; i < src.size(); i++) {
            dst.set(i, src.get(i));
        }
    }
```

2.4 The Get and Put Principle

> <i>**The Get and Put Principle**</i>: use an extends wildcard when you only get values out of a
structure, use a super wildcard when you only put values into a structure, and don’t use
a wildcard when you both get and put.

2.8 Restrictions on Wildcards

Instance Creation   

top-level parameters in instance creation are prohibited from containing wildcard. Nested wildcards are primitted.

```java

List<List<?>> lists = new ArrayList<List<?>>();
lists.add(Arrays.asList(1,2,3));
lists.add(Arrays.asList("four","five"));
```

Generic Method Calls

1. a generic method call includes explict type parameters, those type parameters must't be wildcard.

```java
    class Lists {
        public static <T> List<T> factory() {
            return new ArrayList<T>();
        }
    }
```

An exception is java.math.BigDecimal, which compares as the same two
decimals that have the same value but different precisions, such as 4.0 and 4.00

recursive bound: <T extends C<T, U>, U extends D<T, U>>, in the collection as candiate for the maximum, and then compares the candidate with each element in the collection.

look at the signature of this method in the Java library, you will see something
that looks even worse than the preceding code:
<T extends Object & Comparable<? super T>>
T max(Collection<? extends T> coll)
This is there for backward compatibility

6.1 Reifiable Types

reifiable if it is one of the following:
- A primitive type  
(such as int)  
- A nonparameterized class or interface type  
(such as Number, String, or Runnable)  
- A parameterized type in which all type arguments are unbounded wildcards  
(such as List<?>, ArrayList<?>, or Map<?, ?>)  
- A raw type  
(such as List, ArrayList, or Map)  
- An array whose component type is reifiable  
(such as int[], Number[], List<?>[], List[], or int[][])  
A type is not reifiable if it is one of the following:  
- A type variable  
(such as T)  
- A parameterized type with actual parameters  
(such as List<Number>, ArrayList<String>, or Map<String, Integer>)  
- A parameterized type with a bound  
(such as List<? extends Number> or Comparable<? super String>)  
So the type List<? extends Object> is not reifiable, even though it is equivalent to List<?>.