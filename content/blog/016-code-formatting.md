+++
draft = false
date = "2021-04-19T00:00:00-00:00"
title = "Use automated code formatting"
tags = ["Engineering"]
slug = "code-formatting"
+++

Tabs or spaces? Newlines before braces? End every line with a semicolon, even
if unneeded? Code formatting is one of those topics where discussions are
endless and consensus is pretty much impossible. Everybody prefers things a
certain way and sometimes it can be tough to find a middle ground where
everyone is happy.

In this post I will argue in favor of using tools to enforce code formatting in
order to ensure it stays consistent.

<!--more-->

## The benefits of automating code formatting

When coding, everybody has their own preferences on how to format their code.
Maybe it's because they learned following one style or another, or simply
because they are applying the style of one programming language to another.
Whatever the reason may be doesn't really matter. If several people are working
on the same codebase and they all attempt to apply their own style to it,
problems are bound to come up.

Utilizing automated code formatting provides important benefits with very
little disadvantages. The most obvious one is that all the code will be
consistently formatted which makes reading easier. This in turn, helps reduce
cognitive load which might help prevent bugs when having to read complicated
code. In addition, if the format followed is a well known standard
([like PEP8](https://www.python.org/dev/peps/pep-0008/) for Python) it will
probably also be consistent with third party libraries.

Having a consistent format throughout a codebase will also make the code feel
less like it belongs to a specific person and more like it belongs to everyone
contributing to it.

There are a few things that need to be considered when using a code formatter
though. First an foremost, the standard or format chosen needs to be a good one
that promotes readability. If the code ends up horribly formatted and is hard
to read then all the possible benefits are negated (and it could arguably make
things worse). Integrating one of these tools mid project is also something
that should not be taken lightly, as formatting everything in one go will make
following the change history harder.

There's also the question of when to apply it. Should it be done in the editor
when a file is saved? Something like a Git hook? Do you apply it automatically
in your CI pipeline or do you make it fail if files need formatting? This
really depends on those involved in development and what works best for them.


## Bonus: Static analysis

While we are on the topic of code quality, we can take the opportunity to talk
about static analysis. Depending on the language you're developing on, several
tools can also be integrated to catch errors before they become a problem.
Things like linters can help find common mistakes or point out places where the
structure of the code can be improved. They are also normally really easy to
include in your CI pipeline so there's really no excuse to not do so.

Sometimes new tools aren't even needed. Compiling your code with options such
as `-Wall` can help avoid running potentially unsafe code.


## Conclusion

Integrating a code formatting tool in your development process is relatively
easy, and together with other static analysis tools can provide a boost in the
quality of the software produced. Integrating these tools is something that is
so easy and painless to do that even if the benefits were small it would still
be worth doing.
