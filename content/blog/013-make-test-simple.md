+++
draft = false
date = "2018-08-08T00:00:00-00:00"
title = "Short Thoughts: keep your tests simple"
tags = ["Short Thoughts", "Engineering"]
slug = "keep-tests-simple"
+++

Writing good tests, whether they are unit, acceptance, integration etc, is
hard. Few tests will run quickly but probably won't cover much of the code,
however, having high coverage doesn't mean your tests are good either.
The way tests are written also depends on what the software and it's structure
is. Notwithstanding, there's one aspect that I believe always helps,
simplicity.

<!--more-->

## Software is complex

Writing software is hard, and thus, bugs are an unavoidable and undesired side
effect. While complexity should be avoided, some problems require solutions
that are not simple, therefore, we can say some software is inherently complex.

By creating tests we attempt to ensure software behaves the way we want and
that it continues to do so as it is modified. With different kinds of tests at
different abstraction levels we attempt to unravel this complexity.

## Destroying complexity is the whole point

Tests should be kept as __simple and explicit__ as possible. If tests contain
bugs then that defeats the purpose of having them in the first place.When
looking at a test it should be fairly obvious:

* What is being tested.
* What is expected (and what shouldn't happen).
* Where test data comes from.
* How they add value.

There's probably a problem with your tests if:

* There's logic in them aside from the use of simple helper functions (such as,
  for example checking if two collections have the same elements).
* There are branching paths.
* They depend on each other due to side effects.
* It is hard to track where data is coming from or even what the test data is.

## TL;DR

Complexity causes bugs, __keep your tests explicit and easy to follow__ so
that you __avoid the problem tests try to fix in the first place__.
