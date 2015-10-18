# Lecture 1.2

### Elements of Programming

Every non-trivial programming language provides:

* primitive expressions representing the simplest elements
* ways to _combine_ expressions
* ways to _abstract_ experssions, which introduce a name for an expressions by which it can then be referred to.

### The Read-Eval-Print Loop

Functional programming is a bit like using a calculator.

An interactive shell (or REPL, for Read-Eval-Print-Loop) lets one write expressions and responds with their value.

The Scala REPL can be started by simply typing

`> scala`

### Evaluation

A non-primitive expressions is evaluated as follows.

1. Take the leftmost operator
2. Evaluate its operands (left before right)
3. Apply the operator to the operands

A name is evaluated by replacing it with the right hand side of its definition.

The evaluation process stops once it results in a value.

A value is a number (for the moment).

Later on we will consider also other kinds of values.

#### Example

Here is the evalutation of an arithmetic expression:

```
(2 * pi) * radius
(2 * 3.14159) * radius
6.28318 * radius
6.28318 * 10
62.8318
```

### Parameters

Definitions can have parameters. For instance:

```
scala> def square(x: Double) = x * x
squery: (Double)Double

scala> square(2)
4.0

scala> square(5 + 4)
81.0

scala> square(square(4))
256.0

def sumOfSquares(x: Double, y: Double) = square(x) + square(y)
sumOfSquares: (Double, Double)Double
```

### Parameters and Return Types

Function parameters come with their type, which is given after a colon

`def power(x: Double, y: Int): Double = ...`

If a return type if given, it follows the parameter list.

Primitive types are as in Java, but are written capitalized, e.g:

Int			32-bit integers
Double		64-bit floating point numbers
Boolean	boolean values true and false

### Evaluation of Function Applications

Applications of parameterized functions are evaluated in a similar way as operators:

1. Evaluate all function arguments, from left to right
2. Replace the function application by the function's right-hand side, and, at the same time
3. Replace the formal parameters of the function by the actual arguments.

#### Example

```
sumOfSquares(3, 2+2)
sumOfSquares(3, 4)
square(3) + square(4)
3 * 3 + square(4)
9 + square(4)
9 + 4 * 4
9 + 16
25
```

### The substitution model

This scheme of expression evaluation if called the _substitution model_. 

The idea underlying this model is that all evaluation does is _reduce and expressions to a value_.

It can be applied to all expressions, as long as they have no side effects.

The substituion model is formalized in the _λ-calculus_, which gives a foundation for functional programming.

### Termination

Does every expression reduce to a value (in a finite number of steps)?

No. Here is a counter-example:

```
def loop: Int = loop

loop -> loop -> (ad infinitum)
```

### Changing the evaluation strategy

The interpreter reduces function arguments to values before rewriting the function application.

One could alternatively apply the function to unreduced arguments.

For instance:

```
sumOfSquares(3, 2+2)
square(3) + square(2+2)
3 * 3 + square(2+2)
9 + square(2+2)
9 + (2+2) * (2+2)
9 + 4 * (2+2)
9 + 4 * 4
25
```

### Call-by-name and call-by-value

The first evaluation strategy is known as _call-by-value_, the second is known as _call-by-name_.

Both strategies reduce to the same final values as long as:

* the reduced expression consists of pure functions, and
* both evaluations terminate.

Call-by-value has the advantage that it evaluates every function argument only once.

Call-by-name has the advantage that a function argument is not evaluated if the corresponding parameter is unused in the evaluation of the function body.

#### Example

```
def test(x: Int, y: Int) = x * x

test(2, 3)
test(3+4, 8)
test(7, 2*4)
test(3+4, 2*4)
```

```
test(3, 2)
2 * 2
4

same
```

```
test(3+4, 8)

call by value:
test(7, 8)
7 * 7
49

call by name:
(3+4) * (3+4)
7 * (3+4)
7 * 7
49

call by value is faster
```

```
test(7, 2*4)

call by value:
test(7, 8)
7 * 7
49

call by name:
7 * 7 		# y is not used
49

call by name is faster
```

```
test(3+4, 2*4)

same
```