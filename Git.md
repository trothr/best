# Git and GitHub

This page discusses Git and GitHub.

Git is a source code control system not unlike CVS, Subversion,
and others. Git tracks changes and (for textual files) can report
line-by-line differences from one revision to the next. It is
usually used for coordinating work among programmers, which is
its origin: to maintain the Linux kernel source code.

Some of this content is taken from the wikipedia page for Git.

https://en.wikipedia.org/wiki/Git

## Git

Git was created in 2005 by Linus Torvalds, author of the Linux kernel.

Each copy of a specific Git project is a complete stand-alone repository.
Each copy can work independently of others and of the server or
central/master repository.

Git has become, according to some reports, the most popular distributed
version control system. It is free software and is standard with systems
like Linux.

Git is well integrated into some of the more popular IDEs,
notably Eclipse and Visual Studio.

Git is the utility, the client program.
GitHub is one of several Git servers.

## GitHub

There are many popular services supporting Git including GitHub
and GitLab. This particular page is hosted by GitHub.

GitHub was acquired by Microsoft in 2018.
Some users were skeptical and fled to other providers like GitLab.
But Microsoft has proven to be a good steward of the service
even adding Git functionality to some of their software products.

Git is the utility, the client program.
GitHub is one of several Git servers.

## Git server without the "Hub"

One can house one or more Git repositories with only the 'git'
command and an SSH server. This mode of operation is significantly
less feature-rich than GitHub and other servers running their
"enterprise" software, but can be a quick and reliable way of
establishing vital repositories.

See the `--bare` option on the `git init` command.

## Clone First

<!--                                                                 -->
While most Git commands should be issued from within a Git hierarchy
working directory, cloning of a repository naturally must happen
*outside* of such a hierarchy. Examples are ...

    git clone git@github.com:*userid*/*repository*
    git clone https://github.com/*userid*/*repository*

This repository can be cloned with ...

    git clone https://github.com/trothr/best.git

 ... which would create a `best` sub-directory and populate it
with the current set of files.

Note:
Git state information will be stored in a `.git` sub-directory
in the top level of the hierarchy.

## From Within

The following are a few of the commands useful *within* a Git hierarchy:

* git add

Use `git add` to add a file to a repository or collection.
Simply placing a file into the hierarchy does not make it "tracked".
Git will ignore files which have not been explicitly added.

    git add

* git commit

Use `git commit` to commit changes.
Commonly, you'll use the `-a` flag to commit all changes
rather than adding them one at a time.

    git commit -a

* git push

Use `git push` to push the current committed content
to the supporting Git server.

    git push

* git pull

Use `git pull` to pull the latest committed content from the server.

    git pull

* git status

The command `git status` will tell you the status
of your current repository.

    git status






