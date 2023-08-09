# RSYNC for bulk file transfer

Use `rsync` to copy files, or even whole hierarchies, from one place
to another. RSYNC is an effective tool for keeping two or more copies
of a collection of files in synch with each other. Some people use RSYNC
in favor of traditional backup procedures. 

RSYNC is the tool that I started to write several times.
The goal was to have "synchronized" copies of a collection of files
(original use case: MP3s ripped from CDs). Whenever the "mobile" copy
was in close proximity with the official copy, updates would be sent.

RSYNC handles the small use case I first considered, and so much more.

Simplified syntax of an `rsync` command is ...

    rsync [options] source target

RSYNC is standard with Linux.
It is available for all Unix platforms (Solaris, HP-UX, AIX, OS X) and
for MacOS. It is available for MS Windows as part of CYGWIN or MINGW.

## Hierarchies

RSYNC is typically used for synchronizing files between different systems
but can also be used for synchronizing (or simply copying) files between
two folders on the same system. 

Example RSYNC usage might be something like ... 

    rsync -av source/. target/.

Much computerized file content, especially so-called "static" content,
is conveyed in hierarchical form. A flash drive or thumb drive
is perhaps the most visible form of physical transport for files
and is by nature a file hierarchy.

While RSYNC reliably processes individual files,
it's value is most visible when copying whole hierarchies.

RSYNC uses Unix syntax. Options are introduced with a dash "-".
Single letter options can be combined following the dash. Options are
separated in this document for clarity, so the above is actually ... 

    rsync -a -v source/. target/.

`-a` stands for "archive mode" (see below)

`-v` stands for "verbose mode" (also below)


## Options

The `-a` option (archive) expands to `-rlptgoD`. These in turn mean ...

`-r` for "recursive" which means follow sub-directories

`-l` to copy symbolic links as symbolic links

`-p` to "preserve permissions"

`-t` to "preserve timestamps", specifically modification times
(file creation times and file access times are not maintained)

`-g` for "preserve group" ownership

`-o` for "perserve owner" (if you have privilege to do so
and you don't already own both copies)

`-D` for `--devices` and `--specials` (not always needed but harmless)


More Options


`-u` for "update mode" which is discussed at length it its own section below

`-H` causes RSYNC to preserve hard links, if possible.
Most Unix filesystems have the concept that two files (as seen in
directory listings) can refer to the same physical entity. For a detailed
explanation, search for "inode" in various internet documents.
With the "-H" option, RSYNC will try to preserve such links.

`-K` meaning "keep directory links" causes RSYNC to treat a sym-linked
directory on the target end as a directory. (It forces RSYNC to not
remove a sym-link to a directory if the same object on the source end
is an actual directory.)

`-O` causes RSYNC to "omit directory times".
This allows that a directory on the target end which gets new files
will have a timestamp reflecting the change. RSYNC will not forcibly
reset the timestamp on target directories to match those in the source.

`-S` means to handle sparse files intelligently.
Sparse files are commonly used as a means of saving physical storage.
A file which has long runs of NULL characters may be stored in the
filesystem using less data blocks. (Since the data blocks have the
exact same NULL content.)

`-x` tells RSYNC to stay within one filesystem.
That is, if the hierarchy being copied has other filesystems,
or "shares", mounted below its top level, RSYNC will not descend
into the other spaces.

`-v` stands for "verbose mode" and causes progress and other details
to be reported while RSYNC is running.

## A Simple Recipe

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

You can add `-v` as needed.

## Update Mode

RSYNC may be the only utility in wide use that safely merges updated
directories. Consider the `-u` option which activates "update mode".

Say you have two identical hierarchies. You modify "file1" in the first
hierarchy and modify "file2" in the second hierarchy. Ordinarily, copying
from hierarchy 1 to hierarchy 2 would replace your changed "file2" with
the original. If instead you run RSYNC with `-u`, the target will contain
the updated versions of both files. "file2" in the target hierarchy will
not have been rolled back. The new version of "file1" will also have been
delivered. Reverse the operation (target back to source) and both
hierarchies will have the latest revisions of all files.

In update mode, RSYNC will not overwrite a file on the target end
which is newer than its counterpart on the source end.

It's not as good as Git, but it helps.


