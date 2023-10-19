# Make

This document describes `make` in the simplest terms.

With the popularity of Interactive Development Environments (IDEs)
tools like `make` are less widely known. Also, whether for
multi-platform viability or out of ignorance, some developers
may create overly complicated makefiles. As always, keep it simple.

## Basic Make

`make` is a standard Unix utility. <br/>
It is presumably for compiling programs and building software packages,
but that is misleading. While it is a powerful development tool,
it is useful for more than just writing programs.

`make` is a recipe processor. <br/>
It can be, and has been, used for system administration and management.
It can also be used for general project management.

The basic operation of `make` is to ensure that one or more files
are up-to-date with respect to other files (call them dependencies).
The files in turn can represent other things like states or events
or goals or objectives.

A recipe typically looks like ...

    target:     dependency1 dependency2 dep3 dep4
                action
                action2
                action3

Targets and dependencies are most easily represented by files.
(They do not have to be actual files.) In the above recipe, if the
target `target` exists and is newer than all of its dependencies
`dependency1`, `dependency2`, `dep3`, `dep4`, then it is considered
up-to-date and no further action is needed. If one or more of its
dependencies is newer, then the list of actions is processed.
The actions are commands.

The recipe for each of the dependencies is also driven, if it is known.

## Just Make

In the open source world, a common goal is "just make". <br/>
That is, you'd like for your project to be so seamless that someone can
download the source code and simply enter `make` in the top directory
of the checked-out hierarchy.

The methodology follows the FLOSS "standard recipe" ...

    ./configure
    make
    make install

The final step might be skipped if it turns out to be intrusive,
like if it requires administrative privileges. Or it can be re-directed,
"installing" to an alternate directory or hierarchy.

Sadly, we don't use this recipe in most Voltage build work.
It is the norm for a huge number of open source projects,
to the point of being a mantra for some groups.


