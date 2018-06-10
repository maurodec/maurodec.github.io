+++
draft = false
date = "2017-04-20T00:00:00-03:00"
title = "Amet - Flattening a Python dictionary as environment variables"
tags = ["Python", "Amet", "Open Source"]
slug = "amet"
+++

I recently had to build an ETL job in Python that was initially going to be
deployed on AWS. Little did I know that a last minute change from AWS to
Heroku would cause me to change how the job's configuration was going to be
read significantly.

<!--more-->

## A bit of Background

ETL jobs do not usually require much interaction. You pretty much just need to
figure out how to pass it some configuration values (such as a database
connection string). You can do this in several ways, but probably the easiest
are to either read everything from `sys.argv` or to use a configuration file. I
tend to go for the latter, as I cannot be bothered to parse CLI arguments, plus
it is a lot easier to share and swap configuration files instead of command
line arguments. As for configuration files I tend to favor JSON over other
formats, as it is easy to read/write by humans, allows for lists and nested
objects and the `json` module makes reading these files trivial.

As I said before, this was initially going to run on AWS, but it was later
decided that it would be run in Heroku. This is usually not a problem, unless
you decided that your configuration would reside on configuration files.

## The problem

The downside to configuration files is that since you usually keep secret
values in them you should not add them to version control systems such as git
(yes, even if your repository is private). This can become a problem with
some environments such as Heroku where you have no way of pushing you config
files. You should, in this cases, use environment variables for configuration.

Changing from configuration files to environment variables poses several
obvious problems. First and foremost some code will have to be changed to
accommodate this new requirement. Not only that, working with environment
variables is not nearly as user friendly as a JSON file, but worst of all,
environment variables are "flat", meaning that you cannot have nested values
(and no, trying to encode something like a JSON object into an environment
variable isn't even an option).

## The solution

The solution I came up with was relatively simple. I wrote a function that
will attempt to fill a prototype configuration dictionary with the expected
configuration values. It does this by iterating through the dictionary and,
for every key whose value is not a dictionary, looks for an environment
variable whose name is the same as the key. However, if the value is a
dictionary, it will recursively call itself and do the same, although in this
case the key containing this dictionary will be taken into account when
building the variable's name.

A simplified pseudocode version of the function looks like:

{{< gist maurodec e9ec8db07e87dd15cb786524b17edf54 >}}

As you can see this has its own problems. Without any extra work, any `int`
values will not be converted automatically, probably making it infuriatingly
inconsistent. This method also does not support lists without doing some
probably ugly things. Finally, in some cases names may clash, although that
would be highly improbable (and would probably mean you're using terrible
names for keys anyway).

Up until this point, however, we only cared about reading values and not
writing them. Unless we want to create those environment variables manually
(which I do not recommend) we also need some code to generate the key value
pairs for us.  This is even simpler than reading.

A simplified pseudocode version of the function looks like:

{{< gist maurodec efe473036f1fc55aa20c3651fdf5d4ef >}}

After we have our dictionary of variable names as keys we can either
`export` them or (in my case)
[call the Heroku API](https://devcenter.heroku.com/articles/config-vars)
so they are set in my app's configuration.

## Amet - The solution, packaged.

I wrote a library in Pythom, **Amet**, that packages these two functions so
that they can be used from any Python script. [The code with instructions can
be found here](https://github.com/maurodec/amet).

Amet provides two functions, `load_from_environment` and `dump` to help with
reading and creating any relevant environment variables. It also provides some
extras such as automatic parsing of types and some error handling. This means
that if you are expecting an environment variable to be an `int`, `float`, or
`bool` value, it will be automatically converted for you

The library is still pretty green, so any contributions are more than welcome.

I hope it works well for you and saves you time and headaches 😁.
