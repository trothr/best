# Simplicity of C

C is a simple language.
When coding in C keep the simplicity in mind.

If you've been thrown into a C project and it's not your language
you're not alone. I empathize. Hang in there. If you have inherited
obfuscated C, we feel your pain. This guide cannot fix that code
but will hopefully guide you to better methods than whoever dumped
that complexity on you.

C should be simple.

## Algebraic Expresions

C is an algebraic language.
It's all about asignment of a result from the right-hand side to a
variable on the left-hand side. The assignment itself returns a result
and can be asigned to yet another variable or used in an equation.

Functions are called for two reasons: their *results* (the return value)
or their *side effects* (what happens apart from the equation). Or both.
Consider the `printf()` function. It is called for its side effect,
printing formatted output, but it also returns a value, the number
of characters printed.

    bytesout = printf("this R a test\n");

You can discard the return value, and many programmers often do.

    printf("this R a test\n");

But the return value can also indicate success or failure.
Consider it a status code or a "return code".

    rc = printf("this R a test\n");

In the case of `printf()`, if the return code is negative that's an error.

You can, of course, do actual algebra:

    a = b + c * ( d + e / f );

And again, the assignment returns a value:

    a1 = a2 = a = b + c * ( d + e / f );

Writing C really is a matter of defining functions
which most often in turn call other functions.

## Conditional Execution

C has an `if` statement.

    if (somevalue) *statement*;

If `somevalue` is non-zero, then *statement* is evaluated.
(There is no `then` required.)

C also has an `else` statement which must follow `if`.

    if (somevalue) *statement*;
             else  *otherstatement*;

Some infix operators used in conditional logic are ...

    ==  equal
    !=  not equal
    <   less than
    >   greater than
    <=  less than or equal
    >=  greater than or equal
    &&  logical and, not to be confused with bitwise and
    ||  logical or, not to be confused with bitwise or

Whatever you do, keep it simple.

## Fundamental Data Types

C is gets you closer to the hardware than most other programming languages,
apart from assembly language which varies for each instruction set.
The data types reflect that.

There are three primary data types: `char` for characters, `int` for
integers, and `float` for non-integers (floating point). `char` is
actually a very short integer (8 bits) and usually considered unsigned
though it's not guaranteed to be unsigned unless you say so.

There are modifiers which let you get specific: `short`, `long`,
`signed`, `unsigned`. You'll have to consult with the documentation
for your compiler to be sure of the details.

C also makes heavy use of pointers.
A pointer to an item of a particular type is declared by placing
an asterisk ahead of the variable name. For example, `char *string`
defines a pointer to a character array (a string) and `string` then is
the name of the variable. Later in your program, `*string` refers to
the character at the start of the array while `string` refers to
the whole array.

A variable declared as an array (and not as a pointer per se) can also
be used as a pointer variable. If we define that character string as ...

   char string[256];

 ... the compiler reserves 256 bytes for character storage and `string`
refers to that storage. `string` can also refer to individual characters
either with a subscript on the right or with an asterisk on the left.

## About Character Strings

For newcomers, C seems to treat character strings differently than other
data types. But not really. Remember that C takes you as close as possible
to the hardware without having a unique dialect (like you'd have with
assembler). C treats a string as a vector of single byte characters
because that's how strings are processed by the harwdware.

When declaring a string variable, there are two ways. You can declare an
array of characters or you can declare a pointer to an array of characters.
The choice of which declaration to use depends on what you want to do.
If you want a simple string to be passed along to a function, you might ...

    char *dave;

and then assign a value to it

    dave = "How now brown cow";

You can then pass it as an argument to a function:

    printf(dave);   /* ignoring formatting */

In this case, the compiler allocates storage, but it's not for general
use and will usually be marked read-only.

If you want to manipulate the string, you should declare it as a
[re]writable buffer.

    char davey[100];

Then load the buffer any way you like. A simple copy would be:

    strcpy(davey,dave);

(Copying characters is not terribly interesting. Sorry about that.)

## Derived Data Types

Data types can be combined in two ways: `struct` and `union`.
`struct` is seen more often.

A `struct` or structure is a collection of data elements which get
processed together. One example is a bounded string which can be
represented as a pointer to the characters in the array and the length
of the string.

The string example might be coded like this:

    struct mystring { char *bytes; int length; };

Then `mystring.bytes` is the string data and `mystring.length` is the
number of bytes in the string.

A `union` is an overlay, where all members of the union
start at the same location in memory. Unions are much less common
than structs, but be aware in case you encounter one.

## Easy Increment and Decrement

You can increment an integer the traditional way ...

    i = i + 1;

You can alternatively increment an integer "in place" so to speak ...

    i++;

The latter is handy for indexing. If you want to reference one byte
at a time in a string, you could write ...

    mychar = string[i++];

The effect is to use `i` as the offset and then increment it after
the reference. OR (here's the tricky part) you can swap precedence ...

    mychar = string[++i];

The latter statement increments the index `i` first and then
uses it to reference the item.

You can also perform increment like this:

    i += 1;

All of the above applies for decrement as well.
Simply use minus rather than plus.

Remember that every expression in C returns a value,
so while `i++;` is a statement on its own `[i++]` can use the value.
The former is used solely for its side effect of incrementing `i`
and its value is ignored.

## The Main Thing

There is the concept of a main routine.

When writing C programs, you're actually defining functions.
`main` is a reserved function name, so if you define `main()`
the compiler and linker will treat that function specially.

C was originally created on and for Unix.
In Unix, commands get their arguments as count and an array.
Your main routine should be defined like this:

    int main(int argc, char *argv[]) { /* your code */ }

Main should return an integer, which becomes the return code
to the command shell which invokes your program. (Zero is fine
unless there was a problem.)

`argc` is the count of arguments.

`argv` is an array of strings. It is actually a pointer
to a list of pointers to characters. `argv[0]` is the name of your
program as it was invoked. `argv[1]` is the first argument and is
in turn a pointer to a character string. You can reference the first
byte of the first argument as `*argv[1]` or as `argv[1][0]`.

## Preprocessor -- Beyond C

C itself is a very simple language.
At some point, the developers recognized the need to do more.
For better or worse, they opted for a pre-processor which scans for
its own symbols and performs replacement.

You will surely use "include files" or "header files".
You'll see the syntax ...

    #include <stdio.h>

There is no need to go deep into C preprocessor mechanics.
Just know that `stdio.h` has information to help the compiler and linker
know what to do for system functions in the "standard I/O" collection.

Many C developers will use conditional compilation, like this:

    #ifdef AIX
    /* code which works for AIX */
    #else
    /* code which works for everything else */
    #endif

Usually such platform-specific coding is moved to some place
(some other source file) so that your program can be simpler
and look cleaner. Keep it simple.

## Prototyping of Functions

When writing C, you're defining functions.
As you write a large application consisting of many functions,
one part of your code will call another part. The compiler needs to know
what calling convention or linkage to apply. Often, people simply put
the called functions ahead of those which call them. But this is
not always effetive, not always doable, in fact.

You'll often see `main()` at the end of a program while other functions
are declared ahead of it. It's not bad practice to put `main()` at the
end, but if you want it at the start, you'll need to provide guidance.

C has a concept of "prototyping".
You can tell the compiler what a function returns and the types
of its arguments. Consider one of the stock functions, `write()`.

    rc = write(int fd, void *buffer, int count);

The function returns an integer, the number of bytes written or negative
for error. Its three arguments are the file descriptor (an integer),
the I/O buffer (a pointer), and the number of bytes (another integer).
This function is part of the Unix standard so it is prototyped in the
`unistd.h` header file.

    int write(int,void*,int);

All you have to do is `#include <unistd.h>`,
but for your own functions you can explicitly prototype if needed.
In this example, `write()` is called like this:

    rc = write(fd,buffer,count);

The whole reason for prototyping is simply to let the compiler know
what kind of value the function will return (in this case an integer)
and how to stack the arguments.


