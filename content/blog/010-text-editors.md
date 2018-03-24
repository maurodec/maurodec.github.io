+++
draft = false
date = "2018-03-24T00:00:00-00:00"
title = "Text editors: which is the best?"
tags = ["Engineering", "Tools"]
slug = "best-text-editors"
+++

Text editors are probably the most basic tool of every software developer,
without them we would not be able to do our jobs. It makes sense then to try
and find out what the best text editor is, doesn't it? Is it Vim? Is it Emacs?
Is it another? It's important to first look at what we want in a text editor
before we are able to answer this.

<!--more-->

## All editors are different

The big question we have to ask ourselves is, can I edit text comfortably?
Followed by, does the editor provide any extra functionality that will help
me work more efficiently? Even for something as fundamental as text editors,
we can safely say that not all text editors are created equal.

Some newer text editors like [**Atom**](https://atom.io/) or
[**VS Code**](https://code.visualstudio.com/) are very user friendly.
They provide things like syntax highlighting and code completion for pretty
much any mainstream language out of the box. Plugins allow to extend them in
pretty much any way anybody would want and they also integrate well with other
tools like git.

These editors are great for everybody, whether you're a new developer or a
seasoned one. They come in really handy if you need to get up to speed quickly
and do not have time to set up a more complicated development environment.
Anybody can start using them without having to go through any sort of tutorial
which means there's virtually no barrier to entry.
They also run pretty much anywhere provided a graphical interface is available.
The big downside to them is that they require [a ton of RAM to be
available](https://github.com/jhallen/joes-sandbox/tree/master/editor-perf)
meaning they may not always be suitable depending on the environment you're
developing on or you need to work with large files.

They are also free and Open Source, which is always more than welcome.

[**Sublime Text**](https://www.sublimetext.com/) is very similar in all aspects
to Atom and VS Code that happens to actually perform really well however,
it is not free or Open Source which might put off a lot of people especially
because development has been a bit slow lately.
[Lime](https://github.com/limetext/lime) looked like a promising FOSS
alternative to Sublime, but seems to be slightly abandoned.

What about more classic text editors? [**Vim**](https://www.vim.org/) and
[**Emacs**](https://www.gnu.org/software/emacs/) have been around
for decades and and are revered by many as the best text editors in existence,
which is better is a whole other story though. The reality is that they are
extremely mature pieces of software. Both are reliable, extensible, and perform
exceptionally well, that along with the fact that they have been ported to
pretty much every OS imaginable means they cam be used in any development
environment. Both editors are incredibly powerful and can be modified to be
able to do anything (there's even crazy things such as [Emacs as an
OS](http://wiki.c2.com/?EmacsAsOperatingSystem)).

The harsh reality is that both editors can be hard to learn and do take time to
set up nicely, thankfuly some tools like `vimtutor` exist to help newcomers.
Such a high barrier to entry means that reaping the benefits of using them is
more of a long time investment.

## How do I pick the best editor?

Just use them! **There's no best editor, there's just what works for you.** The
environment you have to work on, the tasks you need to do and even how
experienced you are means that one editor may suit you better than another.
Maybe you find that Vim macros are something you cannot live without or memory
usage isn't a problem in your case, or find that
[Teletype](https://teletype.atom.io/) is a must for your job. Whatever your
reasons are, use what you're comfortable with and what allows you to do your
job better. **Live your truth!**

Using one editor or another will not make you a better programmer, in fact,
using the right tools for the right job is one of the things shows that you're
good at what you do.

Personally, I'm a Sublime Text user. It's powerful, easy to use and has sane
defaults. If I need to use it on a new machine or a machine that is not mine
I can change it to my liking in less than two minutes. It also performs really
well, so I don't have to worry about it taking up all my RAM or having problems
with it when opening large files (which I often do). Can some editing tasks be
slower than in Vim for example? Yes, definitely, but in my case __keyboard
inputs are not the bottleneck, thinking about how I'm going to structure my
code is__.

## You should still learn Vim though

While this might sound a bit contradictory, I believe everybody should know how
to use Vim. The reason for this is **ubiquity**.

Countless times I've found myself having to use machines where it is the only
text editor available and where I'm not able to install or run anything else.
I don't mean be a master Vim user, but I do think you need to have the basics
such as saving, quitting, and basic text editing down. Being able to use Vim on
a basic level has saved my ass more than I care to admit.

## The Final Veredict

Spend an afternoon trying new editors and see what works for you and which you
feel the most comfortable working with. And remember it is not a life or death
matter, you can always switch if you need to 💪.
