+++
draft = false
date = "2017-03-12T00:00:00-03:00"
title = "Creating this Blog with Hugo"
tags = ["meta", "Hugo"]
slug = "using-hugo"
+++

It's sometimes a bit funny how trends come and go in tech.
For a long time dynamic websites were seen as the way to go, no matter
for what kind of content. Lately a lot of people have gone back to
basics and (thankfully) decided to build their sites as a collection
of static pages.

When I started this blog I decided I did not want to go through the
hassle of maintaining a complex site and decided to use Hugo, a static
site generator. In this post I will talk about my experience building
my blog using [Hugo](http://gohugo.io/).

<!--more-->

## Choosing Hugo

For the longest time building dynamic websites was considered the way
to go. While this sort of site opens up a whole world of things that
can be done, it also adds a lot of complexity
(for example when deploying or securing a site) that can sometimes
be unnecessary. When I decided to start this blog I did not want to
go through the hassle of creating something from scratch, or even
bother maintaining something like Wordpress or Drupal. I figured a static site
would be good enough for what I needed, as I just wanted to create a
read only site with no user interaction. Not only that, but I could 
use Github pages to host it, making things even simpler.

I remember a few years ago while looking into Go, I read about Hugo and how it 
could be used to generate entire sites based on a few templates and files with 
the actual site content. While this seemed interesting at the time, I
didn't really have much use for it. Fast-forward a few years and
I found myself looking for a tool that I could use to build my blog with.
While I could use something like [Jekyll](https://jekyllrb.com/), Hugo
still seemed like a viable option and I had already done some 
programming in Go as opposed to not even knowing Ruby, so I
decided to go for it instead.

## The good

* Hugo is **fast**. My blog is of course very small, but for big sites, Hugo
  is excellent as it performs really well and it gets faster and
  faster with every version.
* There are tons of themes available already. You can get your site up
  and running in no time by using a theme somebody else created already.
  Creating your own theme is also pretty straightforward and takes no time
  compared to what writing all the HTML/CSS will take.
* There is a site showcase where you can find (with source!) sites that
  were built with Hugo. The key part is here is that you can see HOW
  they were made, so they also serve as development examples and not
  just inspiration.
* Hugo includes a development server, so with a simple `hugo serve` you
  can try out your site without needing to set up anything. Not only that,
  it also has live reload capabilities, so you can develop and view your
  changes in your browser instantly without restarting anything.
* Markdown. Being able to write content in Markdown is so much better than
  having an editor that sometimes works and sometimes doesn't or that is
  frustrating as hell to use. Markdown is simple, and there are some
  incredibly simple and useful Markdown editors out there. Even if you're
  not a technical user Markdown is easy enough to format content with.
* Finally, Hugo is constantly evolving and new features are added with every
  release, so reading each version's changelog is always exciting.

## The bad

* The documentation, well, not all of it, but the lack of a proper
  overview. The documentation is really good at explaining the different
  individual parts that comprise Hugo, it even has a
  [Quickstart Guide](https://gohugo.io/overview/quickstart/).
  This guide however, is more of a basic tour than a guide. There isn't really
  a place in the documentation that presents explains the different concepts
  Hugo introduces and how they fit together when building a site. This means
  that while documentation is good, there isn't really a place
  to start. In my case I had to go look for sites that used Hugo, looked at the
  source and figured out how how their creators built them.
  If there is one place where I think there's room for improvement is
  providing a place where newcomers can see the different parts of
  Hugo and how they for together. It's also worth mentioning that
  the [forums](https://discuss.gohugo.io/) are an amazing place to ask 
  questions when the answers cannot be found in the documentation.

## Conclusion

In my own experience Hugo was an amazing tool. Building my blog was very easy 
and quick, even considering I built the design myself from scratch. It's very 
flexible and allowed me to do everything I wanted. Being able to write posts in
Markdown was also a requirement that Hugo fulfilled. This combined with the
fact that I can just host everything with Github pages without any extra work
meant that using Hugo was more than worth the (little to no) trouble it gave 
me.

If I had to give advice to new Hugo users it would be to go trough the
Quickstart Guide to get an idea of what Hugo is like, then find a blog they
like and see how it was made. I personally found
[spf13.com](https://github.com/spf13/spf13.com) to be incredibly useful.

If you want to see how this was built you can check out the source in the `src`
branch [here](https://github.com/maurodec/maurodec.github.io), or by clicking
the "Source" link in the navigation bar.
