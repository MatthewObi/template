Tutorial
========

Hello, world
------------

Let's take a look at the "Hello, world" program::

    package main;

    fn main(): int {
        printf("Hello, world!\n");
        return 0;
    }

As you can see, it just uses the ``printf`` function from C. There is more work to be done with the standard
library. In the future, a normal ``print`` function will be made that will be more powerful and more safe compared
to C's ``printf``. But until this happens, ``printf`` will have to be used.

Our starting point is a function called ``main``. We also must declare our package as being ``main``, otherwise 
it won't work. Packages will be explained in greater detail in another section (to be continued...).

Our ``main`` function returns an ``int``, which in this case is ``0``. Just like in C, this value represents the
error code of the program, with ``0`` representing no error.

When this program is compiled and run, the console will output the following::

    Hello, world!

This means that our compiler is working correctly! Congrats! You've written your first Saturn program!

Variables
---------

You can define variables with the following syntax::

    name : type;

You can assign to variables while declaring them::

    name : type = value;

If you initialize a variable with a value, you can omit the type. Take a look at this example::

    x := 5;

The compiler will know that ``5`` is an ``int32``. Therefore, the type of ``x`` will be ``int32``. This is what is called
"type inference." This is very convenient and reduces the amount of type a programmer has to do.

You may notice that the syntax for this is exactly the same as how you define new variables in mathematics.

To initialize variables of other integer types, you will need to add suffixes to your numbers. 
Take a look at this example::

    x := 5u;
    y := 5l;

In this example, ``x`` is initialized as an ``uint32`` and ``y`` is initialized as an ``int64``. 
Here is a table describing which suffixes are needed for what types.

.. list-table:: Constant Suffixes
   :widths: 35 35
   :header-rows: 1

   * - Type
     - Suffix
   * - ``uint8``
     - ``0b``
   * - ``int8``
     - ``0sb``
   * - ``int16``
     - ``0s``
   * - ``uint16``
     - ``0us``
   * - ``int32``
     - ``0``
   * - ``uint32``
     - ``0u``
   * - ``int64``
     - ``0l``
   * - ``uint64``
     - ``0ul``

Assignment
----------

You can assign new values to variables, like so::

    x := 2;
    printf("x = %d\n", x);
    x = 45;
    printf("x = %d\n", x);

The output of this code will be::

    x = 2
    x = 45

.. note:: 
    
    You cannot assign new values to ``const`` variables. ``const`` will be discussed in a future section.

Expressions
-----------

The following table shows what expressions are valid in Saturn programs:

.. list-table:: Expression Types
   :widths: 35 128
   :header-rows: 1

   * - Type
     - Description
   * - ``a + b``
     - Returns the addition of ``a`` and ``b``.
   * - ``a - b``
     - Returns the subtraction of ``a`` and ``b``.
   * - ``a * b``
     - Returns the product of ``a`` and ``b``.
   * - ``a / b``
     - Returns the division of ``a`` and ``b``.
   * - ``a % b``
     - Returns the remainder of ``a`` and ``b``.
   * - ``a & b``
     - Returns the bitwise and of ``a`` and ``b``.
   * - ``a | b``
     - Returns the bitwise or of ``a`` and ``b``.
   * - ``a ^ b``
     - Returns the bitwise xor of ``a`` and ``b``.
   * - ``~a``
     - Returns the bitwise not of ``a``.
   * - ``&a``
     - Returns the address of ``a``, where ``a`` is a variable.
   * - ``*a``
     - Returns the dereferenced value located at ``a``, where ``a`` is a or evaluates to a pointer variable.
   * - ``a && b``
     - Returns the boolean and of ``a`` and ``b``, where ``a`` and ``b`` are truth values. Uses short-circuit evaluation.
   * - ``a || b``
     - Returns the boolean or of ``a`` and ``b``, where ``a`` and ``b`` are truth values. Uses short-circuit evaluation.
   * - ``!a``
     - Returns the boolean not of ``a``, where ``a`` is a truth value.
   * - ``a[b]``
     - Returns the bth element located at ``a``, where ``a`` is an array or collection variable and ``b`` is an index value.

Calling Functions
-----------------

You can call functions in Saturn like so::

    <name> ( <arg1>, <arg2>, ... );

Here are some more examples of calling functions, assuming we created a factorial function:

.. code-block:: C

    printf("%d\n", 5); //Prints 5
    x := factorial(5); //Computes factorial of 5 and puts the value into x
    printf("%d\n", factorial(3)); //Computes factorial of 3 
    //and prints the value

Defining new functions
----------------------

In Saturn, you can define your own functions which you can call in your own code. To define a function, use this syntax::

    fn <name> ( <arg1name>: <arg1type>, <arg2name>: <arg2type>, ... ): <returntype> {
        <body>
    }

``<name>`` can be any identifier, meaning any combination of alphanumeric characters and underscore, as long as the
name starts with a letter or an underscore.

``<returntype>`` can be ommitted if the function does not return a value. You can also put ``void`` in this case as
well.

Here's a quick concrete example::

    fn square(x: int): int {
        return x * x;
    }

As you can see, we define a new function with the name ``square``. It has one argument named ``x`` and given a type
of ``int``. The body of the function consists of one statement, which returns the value of ``x * x``.

We can use this function in our code as such::

    fn main(): int {
        x := square(7);
        printf("%d\n", x);
        return 0;
    }

The console should print out the following::

    49

If
--

Like most programming languages, Saturn has ``if`` statements. They are as so::

    if <boolean-expr> {
        <body>
    }

``boolean-expr`` is any expression that results in a boolean value (true or false). This is either a variable that is a 
boolean type or a comparison expression.

In the code below, we only execute the assignment if the expression ``x < 0`` is true.
::

    if x < 0 {
        x = 0;
    }

The above example has just one statement inside the body, so we can condense it like so::

    if x < 0 then x = 0;

We can pair our ``if`` statement with an ``else`` statement.

While
-----

Just like ``if`` statements, ``while`` statements consist of a boolean expression and a body. The difference is, 
``while`` statements will continue executing as long as the boolean expression evaluates to true.
::

    while <boolean-expr> {
        <body>
    }

In the code below, we will execute the ``printf`` function as long as ``x > 0`` is true.

.. code-block:: C

    x := 5;
    while x > 0 {
        printf("%d\n", x); //Prints the value of x.
        x -= 1; //Decrements x
    }

This code should print out::

    5
    4
    3
    2
    1

Just like with ``if`` statements, ``while`` statements can be condensed onto one line, this time with the keyword ``do``::

    while x != VALUE_SUCCESS do x = check_value();

.. note:: 
    
    You should be careful when doing this as there aren't many instances where a while loop will be one statement, and
    it can be very easy to accidentally create an infinite loop this way.

For
---

Just like ``while`` statements, ``for`` statements are loops that contain a body. They defer greatly however as they
also create a variable and use an "iterator_expression" to determine the range of values the variable should go over.
::

    for <variable> in <iterator_expression> {
        <body>
    }

For ``<variable>`` you do not need to provide the type, just the name, as you would with ``:=``. 

The iterator_expression is defined as follows:
::

    <begin>..<end>
    <begin>..<end>:<step>

The range is exclusive. If you wish to use an inclusive range, you will need to use the syntax below:
::

    <begin>...<end>
    <begin>...<end>:<step>

If step is not defined, it will default to ``1``.

In the below example, we create a variable ``a`` which counts from 0 to 5::

    for a in 0..5 {
        printf("%d\n", a);
    }

The above prints out::

    0
    1
    2
    3
    4

Just like with the ``while`` statement, we can condense a for statement onto one line with ``do``.

::

    for a in 0..5 do printf("%d\n", a);

Currently this is the only version of the ``for`` loop that is available. In the future, I will have a version that
can iterate over a collection like an array, map, or other collection.

To be continued...