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

To be continued...