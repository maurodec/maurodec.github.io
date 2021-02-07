+++
draft = false
date = "2021-02-07T00:00:00-21:00"
title = "Python Decorators"
tags = ["Python"]
slug = "decorators"
+++

Originally described in the "Design Patterns: Elements of Reusable
Object-Oriented Software" book, decorators are a powerful design pattern that
allows us to extend or augment an object's functionality. In this post I will
show with some practical examples how this can be achieved in Python via the
`@decorator` syntax.

<!--more-->

## What do decorators do?

The important question is not what decorators **are**, but what they can **do**
for us. Decorators can be implemented as functions or as classes (we will see
examples of both later), but what they do is "wrap" functions (or even classes)
so that their behavior can be changed seamlessly. Python provides the
`@decorator` syntax to do this, though it is merely syntactic sugar and not
actually required to implement the decorator pattern.

Before we start implementing decorators though, there are a few things we need
to remember:
* Functions and classes are objects, and they can be passed around as
  arguments, functions can also return functions.
* When we define nested functions, they will have access to the context they
  were defined in. This is basically a
  [closure](https://en.wikipedia.org/wiki/Closure_(computer_programming)).

## Building the concept with examples

A decorator will wrap a function and add some behavior (before or after) the
original function. Probably the simplest way of decorating a function is:

{{< gist maurodec 40325afb2da14657400857267f6fd944 >}}

This works, but it's pretty clunky. There's the obvious problem that we need to
remember to call the `decorated` function instead of the original. Of course we
could add something like `say_name = decorated` at the end of our code, but
there's also another problem, our "decorator" is pretty much impossible to
reuse. It's not that this way of decorating functions doesn't work, it does,
but it's just not particularly useful.

If we consider we can pass functions around, we can come up with a slightly
more reusable way of decorating functions. We can write our decorator as a
function that takes a function to be wrapped and whose return value will be
the decorated function. This sounds like a bit of a tongue-twister, it is
better understood when seen in action.

{{< gist maurodec e5ce531f87fe6163ee0ee8e4a4d2887f >}}

If we now call `wrapped_say_name` we will get:

```
I'm going to call the original function...
I'm Mauro.
I just called the original function.
```

There's a few important things to note here:
1. We are passing the `say_name` function as an argument to `decorator`.
2. The nested function, `wrapped`, has access to the context in which it was
  defined and can call `function_to_wrap`.
3. The return value of our function (`decorator`) is a function (`wrapped`).

This is clearly much better as we can now reuse the same code to wrap other
functions. This is still, however, a very flawed example as there are a couple
of things we are not considering:
* What would happen if the wrapped function had arguments that needed to be
  passed?
* What would happen if the wrapped function had to return a value?

Addressing the second point is the easiest, we just need to add a `return` when
calling `function_to_wrap`.
Addressing the first point might be a bit tougher if we want to make sure our
decorator is as generic as it can be. We can obviously add the same parameters
that `function_to_wrap` would take (if it took any), but the generic solution
here would be to take advantage of using
[`* and **`](https://stackoverflow.com/questions/36901/what-does-double-star-asterisk-and-star-asterisk-do-for-parameters)
in function definitions.

Let's look at a more real life example of decorating a function. Let's create
a decorator that will time how long a function takes to execute and will
print it out.

{{< gist maurodec 8d264374c8a2f928d24cfbdb5a0c5143 >}}

The output was:

```
Function took 1.9073486328125e-06 seconds.
0.5
Function took 9.5367431640625e-07 seconds.
5.0
```

In this case we wrapped the `division` function and timed how long it took.
This is a more interesting example because `division` takes two arguments, the
numbers to divide, and also returns the result. What the interface will look
like for our decorator, and what we will do with the return value is something
that we need to account for when designing a decorator. In this case the
decorator's  interface is as generic as it can be, basically taking any
positional and keyword arguments and passing them on to the wrapped function.
It also has to be slightly careful with the return value, as it needs to store
it before returning it so that it can print out the "Function took..." message
instead of returning prematurely.

There is one thing this decorator is still not considering though, exceptions.
Some functions, like the division function can raise exceptions. It is then the
decorator's responsibility to decide that to do (or not do) with them. In this
case exceptions are ignored and allowed to go though, but this means we will
never know how long it took for the function to fail. If it was relevant to us
we would probably wrap the call in a `try/except` block and re-raise the
original exception.

A fixed version of our decorator could look like:

{{< gist maurodec 0d50b5a78a5ff111b7b78a7c0f36a511 >}}

Something interesting about exceptions raised in decorators is that when
looking at the stack trace we can see the decorator is there.

{{< gist maurodec e211af81e6171a803f501eb1a86c1df4 >}}

Now that we've understood what decorators can do, let's look at some syntactic
sugar we can use and at some more complex examples.

## The `@decorator` syntax

Python provides a handy way of decorating functions by preceding a function
definition with a `@` followed by the decorator name. This can be used
in module-level functions or even in class methods. If we go back to our
previous example, we can simply define our `division` function as:

{{< gist maurodec 82f01eba4502b27eb758400fddbb4fcb >}}

If we do this, our definition of `division` is replaced by the decorated
function, so in this case using `@timed` replaces `division` with what we
previously defined as `timed_division`. Using `@timed` just allowed us to call
the wrapped function as if we were calling the original one.

## Decorators with parameters

Up until now, the decorator we were using did not take any arguments, but what
if it did? In this case, the function to wrap would be wrapped with the result
of calling `decorator(args)`. This means that our decorator function has to be
first "built" before it can be used to return a decorated function. This sounds
a bit confusing so let's look at an example. Let's take the `timed` decorator
from before and make it so that it can print a shorter version of the message.
For brevity's sake we will remove the exception handling. This new decorator
will look like so:

{{< gist maurodec 35f2478423a19393e5cf457feac75cf8 >}}

This will output:

```
Function call took 2.1457672119140625e-06 seconds.
0.5
1.1920928955078125e-06s.
0.5
```

What the `timed` function now does is build the decorator itself, while the
`decorator` function is what actually decorates `division`. `decorator` is now
what `timed` was in our previous examples.

It is important to note that now when decorating something, we need to decorate
with a call. Using plain old `@timed` will not work, we need to either use it
like `@timed()` or pass a boolean in this case like `@timed(False)`.

To do this we could also use a class instead of nesting functions. Basically
instead of returning a function we can return a class instance that is also
callable. Calling that class instance will return the decorated function. An
alternative implementation of the decorator in this case could look like so:

{{< gist maurodec a1a0e391255b07b9143a035415171bf2 >}}

When we do `@timed()`, a new instance of the `timed` class is created and
initialized with `verbose = false`. Then that instance is called with
`division` as an argument which is stored in `self.decorated_f` and a reference
to the `wrapper` method is returned. It is the `wrapper` method that will
wrap `division` and replace it. Note that I opted to make the `wrapper` a
method, but it could have also been a nested function like we had been doing
before.

Looking back, we could have also implemented the original decorator as a class
with an `__init__` that took the function to wrap and a `__call__` to act as
the decorated function.

If you want to use a class or a set of nested functions is really up to you, it
depends on what you want to implement and what would look best in that case.

## @functools.wraps

So far we've seen that it is rather easy to decorate a function and replace the
original with it, but by replacing the original we are actually destroying
some information.

All functions have a `__name__` attribute which returns, you've guessed it,
its name. Functions will also have a `__doc__` attribute with their docstring.
However, by replacing the original function, these are lost. If we took
our last example and checked the value of `division.__name__` we would see it
returns `'wrapper'`. If we checked `division.__doc__`, the wrapper's docstring
would be returned and not the one from our `division` function (if we had one).

Thankfully, the standard library comes with
[`functools.wraps`](https://docs.python.org/3/library/functools.html#functools.wraps)
which ensures that the original name and docstring (among others) are
preserved. The implementation is rather simple and can be found
[here](https://docs.python.org/3/library/functools.html#functools.wraps).

## Examples in the standard library

Some commonly used decorators in the standard library include:
* [`@staticmethod`](https://docs.python.org/3/library/functions.html#staticmethod)
  and [`@classmethod`](https://docs.python.org/3/library/functions.html#classmethod)
  for transforming a method into a static method and a class method
  respectively.
* [`@property`](https://docs.python.org/3/library/functions.html#property) for
  defining managed attributes.
* [`@contextlib.contextmanager`](https://docs.python.org/3/library/contextlib.html#contextlib.contextmanager)
  for easily turning a function into a context manager.
* [`unittest.mock.patch`](https://docs.python.org/3/library/unittest.mock.html#unittest.mock.patch)
  for easily patching functions during unit tests.
* [`functools.cache`](https://docs.python.org/3/library/functools.html#functools.cache)
  and [`functools.lru_cache`](https://docs.python.org/3/library/functools.html#functools.lru_cache)
  for caching method calls. The
  [implementation](https://github.com/python/cpython/blob/3.9/Lib/functools.py#L478)
  if the latter is actually quite cool.

## Decorating classes

It is also possible to decorate classes, the difference is that the decorator
will return a class instead of a function (or at least something that behaves
like a class).

One example of this is the
[`@dataclass` decorator](https://www.python.org/dev/peps/pep-0557/) in the
standard library.

While this can be useful, it means treading deeper into metaprogramming
territory, and depending on the case, it is possible that metaclasses fit this
use-case better. This is a whole other topic and is something too big to cover
here.

## Conclusion

Decorators are powerful tools that allow us to enhance our code and change its
behavior in a very simple way that does not require us to change the structure
of our programs. Mastering the use of decorators is a must for every Python
programmer.
