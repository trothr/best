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









