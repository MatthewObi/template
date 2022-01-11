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

    [<begin>..<end>]
    [<begin>..<end>:<step>]

The range is exclusive. If you wish to use an inclusive range, you will need to use the syntax below:
::

    [<begin>...<end>]
    [<begin>...<end>:<step>]

If step is not defined, it will default to ``1``.

In the below example, we create a variable ``a`` which counts from 0 to 5::

    for a in [0..5] {
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

    for a in [0..5] do printf("%d\n", a);

Currently this is the only version of the ``for`` loop that is available. In the future, I will have a version that
can iterate over a collection like an array, map, or other collection.

Pointers
--------

Pointers are variables that hold the address of another variable. They allow the programmer to reference other 
variables in their code.

Pointers are defined so:
::

    <name>: *<pointee-type>;

You can get the address of a variable using ``&<variable>``. 
::

    i: int = 5;
    iptr: *int = &i; //iptr now 'points' to i

    printf("%X", iptr); // Prints the address of i

Addresses assigned to variables are usually random, so you should not try to expect that variables will have 
specific addresses.

You can grab the value at the specified address by using the dereference operator:
::

    iptr: *int = &i; //iptr now 'points' to i
    j := *iptr; // dereference iptr and set j to that value.
    printf(if i == j then "true" else "false"); // Prints true

Be careful, though. Pointers are quite dangerous and if the address in a pointer is not valid, you could create 
all kinds of nasty bugs. For instance, the program will crash if you try to dereference the address ``0`` AKA 
``null``.
::

    iptr: *int = null; //iptr holds the dangerous address 0.
    j := *iptr; // CRASH!

You can mitigate this by checking for null before dereferencing a pointer.
::

    iptr: *int = null;
    if iptr != null {
      j := *iptr; // We know the pointer isn't null, so we can dereference.
    }

Defining your own types
-----------------------

Using built-in types is all fine and good, but what about creating your own data types?
There is indeed a way in saturn to create your own data types.

::

    type <name>: <underlying-type>;

The above creates a type named ``name``. If  ``<underlying-type>`` is a predefined type, you have just created
a type alias. The code below creates an alias of float64 with the name ``number``.

.. code-block:: C

    type number: float64;
    ...
    myNum: number = 0.4; //Works just like "myNum: float64 = 0.4;"


Structs 
-------

::

    type <name>: struct {
      <fieldname>: <fieldtype>;
      ...
    };

The above syntax creates a ``struct`` with the name ``<name>``. Just like 
structs in C/C++, structs in Saturn are aggregate data types that contain a number of fields, which can be any 
other defined data type.

.. code-block:: C

    type Vector2: struct {
      x: int;
      y: int;
    };

In the above code, we create a struct called ``Vector2``, which holds two data fields (``x`` and ``y``), which are 
both of the type ``int``.

To use structs in our code, we simply declare them as the type of a variable:
::

    myVec2: Vector2;

We can also initialize them using ``:=`` and the struct initialization syntax:
::

    myVec2 := Vector2 {x: 0, y: 10};

We can access the fields of the struct using the ``.`` operator, like so:

.. code-block:: C

    myVec2.x = 4; //We access the x field of myVec2 and set it to 4.
    i : int = myVec2.x; //We declare a variable i and set its value to the value of myVec2.x

The ``.`` also works on pointers to structs, automatically dereferencing the pointer:

.. code-block:: C

    myVec2ptr: *Vector2 = &myVec2;
    j := myVec2ptr.x; //Works. Compiler will automatically dereference myVec2ptr.

Methods
-------

There are some functions that have a strong association with a struct.

The syntax for defining a method is similar to defining a function:

.. code-block:: C

    fn(*<structname>) <methodname>(<arg1name>: <arg1type>, <arg2name>: <arg2type>, ...): <returntype> {
      <body>
    }

To be continued...