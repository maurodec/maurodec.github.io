+++
draft = false
date = "2021-04-05T00:00:00-00:00"
title = "Short Thoughts: The existential horror of Progress Bars"
tags = ["Short Thoughts", "UI"]
slug = "progress-bars"
+++

Progress bars are UI elements that have been in use for decades. They are
so commonplace that not only we don't question them, but we also expect them
to be there. However, are they actually any good? Do we need them?

<!--more-->

## Types of Progress Indicators

I think instead of talking about progress bars we need to talk about progress
indicators. Basically a set of UI elements that show that work is being done
and that the user must wait. We can place these indicators in two categories:
elements showing an "amount of progress" (determinate indicators) and elements
showing "indefinite progress" (indeterminate indicators). The former category
would contain things like progress bars that fill up, UI elements showing a
percentage etc. In contrast, the latter would contain elements like spinners,
progress bars (that don't actually show a value and instead show some sort of
animation) or even different mouse cursors such as an hourglass or Mac OS'
dreaded beach ball.

## Determinate indicators are (kind of) a lie

Showing a task's percentage of completion sounds like a great idea. It shows
how much work is done and therefore how much is left, but most importantly it
can give the user a rough idea of how long until something will be done. The
problem, in general, is not with the indicator itself but with the tasks.
Realistically, the progress of a lot of tasks cannot be accurately (or even
roughly) estimated. This is especially bad when things like networking are
involved. It's not uncommon to see progress bars fly only to get stuck for a
long time near the end or in random places.

Does this mean determinate indicators are useless? If they can't show accurate
progress, wouldn't an indeterminate indicator work just as well?

## It's all about the feedback

If we can argue against having determine indicators unless they are accurate,
can we argue against indeterminate indicators and to just say a "Please wait"
text would work well enough?

I don't think so...

Progress indicators serve another purpose, which is to tell the user that stuff
is happening and the application is not frozen. While may not actually be true,
it at least gives the illusion that work is being done behind the scenes. Not
only that, different kinds of indicators will subconsciously inform the user
of the magnitude of what is happening in the background and thus how long a
"normal" wait time would be. For example, showing a skeleton on a web page
not only tells the user that it is loading, but also that the information
will be loaded at any instant. This is conveyed not only by showing the user
(a fake version of) the page they are loading immediately, but also by taking
advantage of what users are already used to! If we used a progress bar for that
same page it would probably feel slower (even if it took the same amount of
time) simply because we are used to seeing progress bars for longer tasks. The
opposite  I believe also applies. Normally things like spinners are used for
short loading times. Using a spinner for something like an OS upgrade can work
but only if it's accompanied by some other information. If this was not the
case, and users just saw a spinning circle for half an hour, they would probably
think something is broken.

Basically, the way we've been using progress indicators determines our
expectations for the future and in turn determines how we will be able to use
them again.

## The best indicator is no indicator

The best progress indicator is the one not shown, not because we chose not to
show one but because we can actually mask it. An example of this would be
loading things while some animation is shown or even pre-loading information
that we are likely to show in the future. An example of this is fading out a
login screen. This gives whatever should be shown e.g. a desktop some time to
load while making it feel seamless. Another good example of this in action is
in video games, where things can be preemptively loaded for example during a
cutscene.

Finding places where this can be done is extremely hard though and this not
done often

## Conclusion

Progress indicators are weird. More often than not they aren't even remotely
accurate, however, we need them to give us emotional comfort and to assure us
work is happening behind the scenes and that everything is going according to
plan. It is always a good idea too, to do work in advance and not have to ask
the user to wait.
