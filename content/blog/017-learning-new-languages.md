+++
draft = false
date = "2022-04-10T00:00:00-00:00"
title = "The difficulty in learning a new Programming Language"
tags = ["Engineering"]
slug = "learning-new-languages"
+++

Programming Languages come in all shapes and sizes. When attempting to learn a
new Programming Language there are many hurdles one has to overcome, some easy
and some very challenging.

Here I will explore what some of these hurdles are.

<!--more-->

## Familiarity

The first and most obvious barrier to entry is familiarity, or rather,
similarities to other language one may be familiar with.

It is much easier to pick up a Programming Language if it's syntax is similar
to others you already know. For example, learning Java if you're a C programmer
is probably easier than trying to pick it up if you've only ever programmed in
Basic. If the syntax for your code does not feel alien, writing it will be
easier and come more naturally.

Similarity with some caveats though. Common keywords that mean different things
could cause some confusion. For example, `with` in Python is completely
different to the one in Visual Basic, or `static` in C means something
completely different than it does in Java. Another example is how different
`this` can behave in certain situations in Java or C# compared to Javascript.

Lack of familiarity can be challenging in some cases. New concepts can
sometimes be hard to grasp and can only really be learned by doing, one such
example is Rust and its borrowing rules. In other cases it can be a massive
challenge, such as when learning a Functional Language for the first time.

## Tooling and ecosystem

How easy it is to jump on board and start building something can also be a
hindrance, or at least affect the developer experience greatly. In some cases
there are no issues to overcome. For example, interpreted languages are, for
the most part great in this regard. Running a Python script is extremely easy,
even when dependencies are involved (at least as a general rule).

In other cases things can be a little tricker. Compiling some C you've written
is rather simple, however, things can get a bit messy as the number of files
grows and external dependencies are included. Javascript is easy to run when
doing small things or testing things out, but the recommended toolchain is, in
my opinion, nightmarish (or at least it used to be a few years ago).

Moving from an Open Source ecosystem where one can inspect the source of
libraries and see what is happening underneath is also very different than
attempting to work in a Closed Sourced one where everything is opaque.

## Documentation, popularity and resources

It is nearly impossible to learn a new language if the availability of
knowledge isn't there. Having good documentation and learning resources is
essential. A language being popular can also help, as it is likely that there
will be more support from the community, for example in the form of questions
and answers or code snippets (though the latter is usually a double edged
sword). Code reviews are also a great way to learn and do things "the right
way".

## Finding a project

Finding a good project to actually apply all the knowledge you are acquiring
(or trying to) is what I struggle with the most. How many To-Do lists,
Calculators or API Clients that you're never going to use can you code?

Ideally, you will find a project that you are going to find useful and actually
use, with a relatively limited scope, all while requiring non-trivial use of
different features in the language and its standard library. This I feel is the
hardest part.

## Why learn a new language

The question is actually, "Why not?!". Learning new languages will expose you
to new ideas and new ways of doing things. This is objectively good and will
make you a better developer. But even if you chose to learn a language you
thought was terrible and you would never use, you can still get value from it
by at least learning how NOT to do things.