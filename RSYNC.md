# RSYNC for bulk file transfer

RSYNC is the tool that I started to write several times.
The goal was to have "synchronized" copies of a collection of files
(original use case, MP3s ripped from CDs). Whenever the "mobile" copy
was in close proximity with the official copy, updates would be sent.

RSYNC handles the small use case I first considered, and much more.
It has become standard with all of the more widely used Linux distributions
and is available for most Unix systems and MacOS. It also runs on MS Windows
via CYGWIN or MINGW.

## Hierarchies

Much computerized file content, especially so-called "static" content,
is conveyed in hierarchical form. A flash drive or thumb drive
is perhaps the most visible form of physical transport for files
and is by nature a file hierarchy.

While RSYNC reliably processes individual files,
it's capability is most prominent when copying whole hierarchies.

# A Simple Recipe

Here is a recommended way to invoke `rsync` ...

   rsync -a -u -x -H -O -S source:/some/path/. target:/some/path/.

In Enlish, "copy all files under this directory to that directory".

This will reliably update a file tree on the source end into an
equivalent tree on the target end. Either "source" or "target" must be
the local system (where the `rsync` command is issued) and should be
left off the path specifier for that end.

The slash-dot at the end of the path specifiers ensures that the
transfer is from folder to folder and helps identify or even eliminate
typographical errors. (It avoids accidentally creating a sub-directory
named "path" on the receiving end.)

`-a` expands to a number of common options
suitable for bulk file transfer

`-u` indicates "update mode" for which RSYNC will not overwrite
a file on the target end which is newer than its counterpart
on the source end

`-x` tells RSYNC to stay within one filesystem.
That is, if the hierarchy being copied has other filesystems
or "shares" mounted below its top level, RSYNC will not descend
into the other space(s).

`-H` causes RSYNC to attempt to retain hard links

`-O` causes RSYNC to omit times on directories

`-S` means to handle sparse files intelligently.
So-called "sparse" files may contain a high percentage of
NULL bytes and can be stored more efficiently on many systems
of that fact is known.


