# Lecture 1.3

### Call-by-name, Call-by-value and termination

You know from the last module that the call-by-name and call-by-value evaluation strategies reduce an expression to the same value, as long as both evaluations terminate.

But what if termination is not guaranteed?

We have:

* If Call-by-value evaluation of an expression _e_ terminates, then Call-by-name evaluation of _e_ terminates, too.
* The other direction is not true.

### Non-termination example

Question: Find an expression that terminates under Call-by-name but not under Call-by-value

Let's define

```scala
def first(x: Int, y: Int) = x
```

and consider the expression `first(1, loop)`

Under Call-by-name:

```scala
first(1, loop)
> 1 // no need to evaluate loop since it's no used
```

Under Call-by-value:

```scala
first(1, loop)
> loop // will loop forever, since loop evaluates to itself, this expression won't terminate
```

### Scala's evaluation strategy

Scala normally uses call-by-value.

But if the type of a function parameter stars with `=>` it uses call-by-name.

Example:

```scala
def constOne(x: Int, y: => Int) = 1
```

Let's trace the evaluations of 

```scala
constOne(1 + 2, loop)
```

and

```scala
constOne(loop, 1 + 2)
```

### Trace of constOne(1 + 2, loop)

```scala
constOne(1 + 2, loop)
constOne(3, loop) // no need to reduce, it's a call-by-name parameter)
// -> 1
```

```scala
constOne(loop, 1 + 2)
// no progress because loop reduces to itself
```