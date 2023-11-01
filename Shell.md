# Shell Scripting

This markdown document discusses some best practices for shell scripting.

## `/bin/sh`

Always start generic shell scripts with `#!/bin/sh`.

As I write, in the early 2020s, I see a lot of `#!/bin/bash`.
While BASH is an excellent shell, and my own preferred shell
for interactive work, it's not always right for scripting.
It's usually *not needed* for scripting. There are few things BASH
can do that other Bourne-compatible shells cannot also do, but unless
you really need those features, don't introduce a BASH requirement.

We're talking about scripting here.
As a login shell, or for command processing, *yes*, BASH is way better.

On POSIX systems (Unix, Linux, MacOS, and things like them)
`/bin/sh` is required by the system specification and is required
to be Bourne-compatible. So you're in good shape coding `#!/bin/sh`.

If you really need to use BASH, see "Alternative Interpreters" next.

Again, resist the temptation to code `#!/bin/bash`.
9 times out of 10 it will work, but that is deceptive success.

## Alternative Interpreters

The `#!` syntax at the start of a shell script is a "magic number".
That particular sequence "pound bang" tells the operating system
"this is a script". Immediately after that should be the fully-qualified
path to the interpreter of interest. (If the system does not recognize
the filename coded then the script may fail or the system will pass
the script to `/bin/sh`.)

Many interpreted languages can be invoked just by the name of the script
which is written in that language. Perl, for example, can be indicated
with `#!/usr/bin/perl`. That presumes Perl is installed and also that it
resides at `/usr/bin/perl`. There is a better way.

The `PATH` variable lists directories where your command shell should
look for executable commands and programs. Better than hard-coding
the fully-qualified path to the interpreter you want, try this ...

    #!/usr/bin/env perl

One of the functions of `/usr/bin/env` is to find the named interpreter
in a directory listed in `$PATH` and then pass the script to it. So if
you wanted BASH, you would code ...

    #!/usr/bin/env bash

The system would then search your `PATH` variable, find `bash`
(which could be in any of several different locations),
and passes the script along to it.

This method works for other languages than Perl and BASH,
like Python and Rexx.

## Capturing Output

In the shell, output of a command can be captured into a variable.
The historical way to do this is ...

    variable=`command`

It's best to use the historical form.
There's a newer form `variable=$(command)`, but there are some shells
where that syntax fails. So go with the older syntax even if it's ugly.

## Clean Conditionals

A standard built-in command in Bourne-compatible shells is `if`.
Formally, `if` runs a command and switches based on success or failure
of that command. If the command returns zero (success) the commands
between `then` and `fi` are executed. You can also have `else`,
but we won't get into that in this document.

There is a standard command `test` which performs comparisons
(both numeric and string equivalence). For readability, `test` can be
expressed as `[`. In this latter form, the command must "close" with `]`.
Thus you can write a more readable conditional sequence ...

    if [ "$A" = "blah" ] ; then echo "foo!" ; else echo "fum!" ;  fi

The actual operation of `[` is the `test` command, but the brackets
provide clearer visualization. This makes maintenance easier.

## Use Pipelines

Shell pipes are a powerful feature, if not well-understood.

When chaining commands in a pipeline, you're likely to benefit
from common tools like AWK, SED, GREP, and XARGS. Discussion of these
is beyond the scope of this document, but do learn about those.

And there is a better pipeline, but that's another story

## More to Come

We need to talk about profiling.

We need to discuss the `exec` command.

We also need to talk about "sourcing" versus invoking or executing.


