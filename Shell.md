# Shell Scripting

This markdown document discusses some best practices for shell scripting.

## `/bin/sh`

Always start generic shell scripts with `#!/bin/sh`.
As I write, in the early 2020s, I see a lot of `#!/bin/bash`.
While BASH is an excellent shell, and my own preferred shell
for interactive work, it's not always right for scripting.
It's usually *not needed* for scripting. There are few things BASH
can do that other Bourne-compatible shells cannot also do.

On POSIX systems (Unix, Linux, MacOS, and things like them)
`/bin/sh` is required by the system specification and is required
to be Bourne-compatible. So you're in good shape coding `#!/bin/sh`.

## Capturing Output

In the shell, output of a command can be captured into a variable.
The historical way to do this is ...

    variable=\`command\`

It's best to use the historical form.
There's a newer form `variable=\$\(command\)`, but it's possible
to encounter shells where that syntax fails.






## Use Pipelines

Shell pipes are a powerful feature, if not well-understood.

And there is a better pipeline, but that's another story


