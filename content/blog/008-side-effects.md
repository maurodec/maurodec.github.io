+++
draft = false
date = "2017-09-05T00:00:00-00:00"
title = "Code smell and a lesson learned"
tags = ["Engineering"]
slug = "side-effects"
+++

In an ideal world there's always time and resources available to refactor code
and to make sure it is as clean as possible. Even though it is well known that
refactoring code helps with maintainability and thus reduces development costs
in the long run, for various reasons refactoring does not always happen, or at
least not until things start to fall apart.

In this post I will tell a little horror story that happened to me recently and
that could have been avoided if we had stopped to refactor the code we were
working on...

<!--more-->

## Back story

I recently had to work on an Angular 1 app that was having some issues. The app
would display forms based on JSON documents that were usually pretty large. The
problem was that sometimes the forms would take a long time to load (especially
the really large ones), or changing some of the inputs caused noticeable lag.
Some slowness was expected as some of these forms were particularly huge, but
at times the app became too frustrating to use, and even when sitting in the
background, the CPU usage of the app was incredibly high.

## Fixing things little by little

I always found performance problems to be interesting for some reason. I've
come across some problems with really simple solutions (like applying the
[Flyweight](https://en.wikipedia.org/wiki/Flyweight_pattern) pattern to avoid
unnecessary object creation), while others have proven to be a lot more
challenging (such as having to debug and fix polygon merging algorithms). 

For this particular case, I decided to go for simple and obvious optimizations
and best practices first and delve into more complicated ones later. My first
step was to remove functions from expressions such as `ng-disable` and replace
them with attributes on plain objects. This improved performance a lot, as
adding functions in expressions like these causes them to be called often.
Unfortunately it was still not enough, something else had to be done.

The form rendering code was put together impressively quick and was not too
hard to follow, however it was clear that parts of the code had mutated to do
different things than originally intended and thus the naming of some of some
functions did not reflect 100% what they did anymore. After fixing the HTML it
was time to start optimizing the code underneath. One of the most important
functions of the View Controller was in charge of figuring out whether the form
was ready to be submitted, lets call it `setValid`. This function was being
called each time an input changed which sounds reasonable, the problem was that
some inputs could cause other inputs to be disabled triggering another call to
the function. These inputs could in turn disable yet more inputs, causing a
cascade of calls.

## A better solution

Because in most cases inputs would only disable inputs that came after, a
simple but effective solution was to avoid calling the function over and over
and instead wrap part of the logic in a loop. On each iteration, check if
inputs should be disabled (via an already written `isDisabled` function) and
set a flag. This would continue until no inputs were changed. Unless
inputs somehow disabled previous inputs (which was very very rare), no more
than two iterations would be needed to make sure the form was valid. A _very_
simple version of the algorithm looked like this:

{{< gist maurodec c54989238a5cf6685d6e90d3171d2e9d >}}

This solution was pretty straight forward, we loaded forms, checked the number
of iterations and they were indeed 2. We selected an input that would cause
another to be disabled and the number of iterations was also 2! This seemed to
work, notwithstanding, performance did not improve much.

## More optimizations and the real culprit, code smell

Days passed, and more things were optimized, but performance still was not as
expected. While adding some logging statements we accidentally found out that 
the `setValid` function was looping many times, as in, thousands of times for
some forms, but why? This made no sense!
We went through the code, tested things, but couldn't figure out what was
wrong, it made no sense! Until finally... the problem was so obvious! It was in
front of us the whole time but we failed to notice it! We were relying on side
effects for things to work! The `isDisabled` function would not only tell us if
an input was not disabled it would also actually go and disable it. Because 
the `||` operator short circuits only the first input would be disabled, but
subsequent inputs were totally ignored. This made it so that only one input was
disabled per iteration instead of all (or most) of them. We felt like total
fools.

If we had stopped to actually refactor code and make sure functions were
properly named and separated before even attempting to optimize, it would have
saved us a headache, embarrassment, and most importantly, a lot of time.

## Avoiding this in the future

The need to follow best practices and to constantly clean up code is something
we all knew but failed to do. This was a kick in the teeth to remind us that it
is something that always needs to be done, without exception. Because we let
our code rot, we ended up with functions that had side effects we relied on for
our logic to work which eventually bit us in the ass, big time.

This is also a lesson learned on why writing
[pure functions](http://www.onlamp.com/pub/a/onlamp/2007/07/12/introduction-to-haskell-pure-functions.html)
is pretty much always a good idea, as they help make the code easier to
understand especially when functions are nested within other functions. Clearly
seeing what a function does and what it does not helps a lot when attempting to
figure out if a program is correct or not. This does not mean that we should
all move to functional programming, but good things from it can most certainly
be followed.

Of course this was a very stupid mistake that we failed to notice because we
were busy looking at details and not the whole pictures, but these points
still stand. It is important to keep your code clean in order to avoid silly
mistakes, at least I know that is what I will be doing in the future as much
as I can.