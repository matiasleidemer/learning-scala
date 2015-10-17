# Lesson 01

Paradigm: In science, a _paradigm" described distinct concepts or thought patterns in some scientific discipline.

Main programming paradigms:

* imperative programming (C, Java)
* functional programming
* logic programming

Orthogonal to it:

* object-oriented programming

### Review: Imperative programming

Imperative programming is about

* modifying mutable variables
* using assignments
* and control structures such as if-then-else, loops, break, continue, return

The most common informal way to understand imperative programs is as instruction sequences for a Von Neumann computer.

### Imperative Programs and Computers

There's a strong correspondence between

Mutable variables <-> memory cells
Variable dereferences <-> load instructions
Variable assignments <-> store instructions
Controle structures <-> jumps

Problem: Scaling up. How can we aboud conceptualizing programs word by word?

Reference: John Backus, Can Programming Be Liberated from the von. Neumann Style?, Turing Award Lecture 1978.

### Scaling Up

In the end, pure imperative programming is limited by the "Von Neumann" bottleneck:

_One tend to conceptualize data structures word-by-word_

We need other techniques for defining high-level abstractions such as collections, polynomials, geometric shapes, string, documents.

Ideally: Develop _theories_ of collections, shapes, strings, ...

### What is a Theory?

In methematics, a theory consists of

* one or more data types
* operations on these types
* laws that described the relationships between values and operations

Normally, a theory does not describe mutations!

### Theories without Mutation

For instance the theory of polynomials defines the sum of two polynomials by laws such as:

`(a*x + b) + (c*x + d) = (a+c) *x + (b+d)`

 But it does not define an operator to change a coefficient while keeping the polynomial the same.
 
 Whereas in an imprative program one _can_ write:
 
 ```
 class Polynomial { double[] coefficient; }
 Polynomial p = ...;
 p.coefficient[0] = 42;
 ```
 
 ### Theories without Mutation
 
 Other example:
 
 The theory of strings defines a concatenations operator `++` which is associative:
 
 `(a ++ b) ++ c = a ++ (b ++ c)`
 
 But it does not define an operator to change a sequence element while keeping the sequence the same.
 
 (This one, some languages _do_ get right: e.g. Java's strings are immutable)
 
### Consequences for Programming

If we want to implement high-level concepts following their mathematical theories, there's no place for mutation.

* The theories do not admit it
* Mutation can destroy useful laws in the theories

Therefore, let's

* concentrate on defining theories for operators expressed as functions
* avoid mutations
* have powerful ways to abstract and compose functions

### Functional Programming

* In a _restricted_ sense, functional programming (FP) means programming without mutable variables, assignments, loops, and other imperative control structures
* In a _wider_ sense, functional programming means focusing on the functions
* In particular, functions can be values that are produced, consumed, and composed
* All this becomes easier in a functional language.

### Functional Programming Languages

* In a _restricted_ sense, a functional programming language is one which does not have mutable variables, assignments, or imperative control structures.
* In a _wider_ sense, a funcional programming language enables the construction of elegant programs that focus on functions.
* In particular, functions in a FP language are first-class citizens.

This means:

* they can be defined anywhere, including inside other functions
* like any other value, they can be passed as parameters to functions and returned as results
* as for other values, there exists a set of operators to compose functions

### Some functional programming languages

In the restricted sense:

* Pure Lips, XSLT, XPath, XQuery, FP
* Haskell (without I/O Monad or UnsafePerformIO)

In the wider sense:

* Lisp, Scheme, Racket, Clojure
* SML, Ocaml, F#
* Haskell (full language)
* Scala
* Smalltalk, Ruby and Javascript (blocks)

### History of FP languages

* 1959		Lisp
* 1975-77	ML, FP, Scheme
* 1978		Smalltalk
* 1986		Standard ML
* 1990		Haskell, Erlang
* 1999		XSLT
* 2000		OCaml
* 2003		Scala, XQuery
* 2005		F#
* 2007		Clojure

### Why Functional Programming?

Functional Programming is becoming increasingly popular, because it offers the following benefits:

* simpler reasoning principles
* better modularity
* good for exploiting parallelism for multicore and cloud computing

