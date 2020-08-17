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

To be continued...