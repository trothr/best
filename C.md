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

    ==
    !=
    <
    >
    <=
    >=
    && logical and, not to be confused with bitwise and
    || logical or, not to be confused with bitwise or

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

C also makes strong use of pointers.
A pointer to an item of a particular type is defined by placing
an asterisk ahead of the variable name. For example, `char *string`
defines a pointer to a character array (a string) and `string`
then is the name of the variable. Later in your program, `*string`
refers to the character at the start of the array.

The name of an array can also be used as a pointer variable.
If we define that character string as ...

   char string[256];

 ... the compiler reserves 256 bytes for character storage but `string`
can refer to individual characters either with a subscript on the right
or with an asterisk on the left.

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








