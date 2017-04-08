+++
title = "Cross compiling Go applications"
draft = false
date = "2017-04-08T00:00:00-03:00"
tags = ["meta", "Go"]
slug = "cross-compile-go"
+++

I often write blog posts on different computers. Sometimes I write on my
Macbook (which is where I run a local Hugo server to test things out), other
times I SSH into my Raspberry Pi and write there until I am on my Macbook
again. While writing my
[Why I learned Python blog post](/blog/learning-python/) I asked some friends
for feedback, however, I did not want to push an unfinished post to Github
Pages, so I decided to serve my Hugo blog from my Raspberry Pi. I soon realized
that I would have to install Hugo from source which could mean trouble...

<!--more-->

## Version mess

I bought a Raspberry Pi in late 2012, so I have one of the original Raspberry
Pi Model B which are... well... pretty underpowered. This is usually not a
problem as I tend to run services which do not need much resources. In it, I am
running a headless setup of Debian 8, which as we all know probably has some
outdated packages, but this tends not to be a problem, until now.

My blog is designed to work with Hugo 0.18+, however, it is not available in
the Debian repositories (well, no version is available actually). This should
be a non-issue, as all it takes is a `go get` to pull and compile the latest
version. Little did I know that the latest Go version available for Debian 8
seems to be 1.3 which is not new enough for building Hugo. I could always
compile a new Go version, but there's a big gotcha, with Go 1.5 the compiler
and runtime were rewritten in Go, meaning that Go 1.4+ is needed for building
it. This means that in order to install Hugo 0.18 I would have to compile Go
1.4 first and then compile Go 1.8. All of that on a Raspberry Pi? No thank you.

## Cross compilation to the rescue

I figured that there must be a simpler way of getting Hugo 0.18 on there, so I
started doing some research to see whether it was possible (and how hard it
would be) to compile a Hugo binary on another architecture (x86_64 in this
case). I soon came across
[this blog post](https://dave.cheney.net/2015/08/22/cross-compilation-with-go-1-5)
that explained how to go about cross compiling code. I decided to try this on
my Macbook, as it was what I was using. The instructions seemed a bit too
simple though, I was sure I was going to run into other issues. Cross compiling
could not be this easy, could it? Well yes, it was. I was pleasantly surprised
at how smooth it all went and how quick it was. All it took was running:

```
env GOOS=linux GOARCH=arm GOARM=6 go build -v github.com/spf13/hugo
```

I then `scp`-ed my freshly built binary and BAM! It worked flawlessly!

## Feeling dumb as bricks

It turns out it did not have to go through all this trouble to get Hugo on
Brinstar (thats what my Pi is called), as the
[Hugo releases page](https://github.com/spf13/hugo/releases) has binaries for
ARM (though I did not test if they worked or not). Not only that, the
[Go downloads page](https://golang.org/dl/) provides ARMv6l binaries which
for sure work on my model, I could have just downloaded that!

{{< figure src="/static/img/crosscompile/facepalm.gif" title="Judge Judy is not pleased" >}}

The moral of the story is: always look for pre-built binaries. All jokes aside,
I was surprised at how uncomplicated cross compiling a Go binary was, which
depending on what type of software you're building could be a very big plus.
