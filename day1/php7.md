**PHP 7: The Big Five Plus One** by [Cal Evans](https://twitter.com/CalEvans)

1. Exceptions in the engine
2. Scalar type declarations
3. Combinated comparison operator
4. Easy user-land CSPRNG
5. Null coalesce operator

**Exceptions in the engine**

Problem: Fatal errors cannot be gracefully handled.  They do not invoke a finally block.  They do not call an object's destructor.

In PHP 7 we can catch not an exception but an error.  An error is basically all the stuff we're used to in an Exception (now moved to Throwable).  Exception and Error both implement Throwable.  TypeError and ParseError both extend Error.  Wrap you're bootstrap in a try/catch and catch a Throwable.  (You can't implement Throwable as is).  Do not catch Errors except for logging and cleanup.  Errors are code issues that should be fixed, not conditions that can be handled at runtime.  When you get an Error, that's the same as a fatal exception.  For the most part you're not going to be able to recover.

**Scalar type declarations**

Controversial.

Scalars are the basic building blocks of any programming language.  In PHP: int, float, string, bool.

`declare(strict_types=1);` at the top of every file you want, above your namespace.  You can incrementally roll this out.

As soon as 7 goes gold, you're going to see new versions that come out requiring 7.

There are two camps in the core.  1: If I as a dev, and you don't honor that, something bad should happen. 2: Well PHP has been such a forgiving language, so if they pass in a string it should be coerced.

This applies to the calls you make in the file that the declaration is in.  It does not affect where the functions are defined.  And it applies to any language functions that have type hints.  Up until this point we didn't have any.

Widening: the core, in part of the compromise, there was one time they would allow coercion.  THat is when you require a float and are passing in an int.  Because there is no way to lose precision doing this.

Return type declarations: we can define what our functions will return.  [nullable, union?]

**Combinated comparison operator**

Spaceship operator.  Why do we have it?  Ruby does.

First trinary operator in PHP.

**Easy user-land CSPRNG**

Cryptographically secure pseudo random number generator (don't get hung up on the word number)

The rand function in PHP is horribly broken.  So what happens is that users write their own.

Consistant interface to CryptGenRandom on Windows and /dev/urandom on Linux/OSX.

`random_bytes(int length);` and `random_int(int min, int max)`

**Null coalesce operator**

    $name = $firstName ?? "Cal";
    $name .= " ";
    $name .= $lastName ?? "Evans";

