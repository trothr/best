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








