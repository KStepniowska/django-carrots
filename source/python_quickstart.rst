======================
Introduction to Python
======================

Let’s start with the running of interpreter which we installed in a previous chapter:

.. code-block:: sh

    (warsztaty) ~$ python
    Python 3.3.1 (...)
    Type "copyright", "credits" or "license" for more information.

    >>>

Now we can count something, for example: 2 + 2

    >>> 2 + 2
    4

Python is excellent as a calculator:

    >>> 6 * 7
    42
    >>> 1252 - 38 * 6
    1024
    >>> (3 - 5) * 7
    -14
    >>> 21 / 7
    3
    >>> 3**2
    9
    >>> 5 / 2
    2

This last result can be quite surprising. We expected rather get two and a half. On the other hand, so
far we have used only whole numbers so for  Python there is no reason to force us to use fractions. 
But we can do it by ourselves:

    >>> 5.0 / 2
    2.5

It is important to note that we type decimals with a dot instead of comma, the same as in english.
Commas will serve us to define tuples :ref:`krotek <bmi-tuples>` (eng. ``tuple``),
but more on that later.


Introduce yourself
==================

Strings
-------

Only numbers, however, are not enough to communicate effectively. We have to learn how to use strings.
Here are some examples:

    >>> "Hello World"
    'Hello World'
    >>> 'Foo Bar'
    'Foo Bar'
    >>> "Rock 'n' Roll"
    "Rock 'n' Roll"
    >>> 'My name is "James"'
    'My name is "James"'

It is also possible to add strings like that:

    >>> 'My name is ' + '"James"'
    'My name is "James"'

and multiply it by whole numbers:

    >>> 'Hastur' * 3
    'HasturHasturHastur'

The string must always begin and end with the same character. This may be an apostrophe (‘) or double
quotes (“). This does not affect the value of the string, for example, while typing “Batman” we 
create a string Batman - quotes are not a part of it. They serve only to indicate that it is a string
(unfortunately Python is not that smart to figure it).


Printing the strings
--------------------

But how to present value in a readable form?
We can do it by using the function print :func:`print`:

    >>> print("Hello World")
    Hello World

We can thus write several strings in a single line, without adding them to each other. They will be 
separated by spaces:

    >>> print("Hi, my name is", "Lucas")
    Hi, my name is Lucas

:func:`print` has also a lot more applications because it could print almost everything. For now, the 
only other kind of values we know are numbers:

    >>> print(1)
    1
    >>> print(1, 2, 3)
    1 2 3
    >>> print("2 + 2 =", 2 + 2)
    2 + 2 = 4

For now, this will end our work with an interactive console. To get out of it, just type `quit()`::

    >>> quit()


Source files
============

So far our code was executed in an interactive mode where we give commands separately and immediately 
get an answer. It’s a great way to experiment and learn new language elements, so we will be back here.

Our first program might look like this::

    print("Hi, my name is Lucas")

Run the program from a command line: 

.. code-block:: sh

    $ python businesscard.py
    Hi, my name is Lucas.
    $

A single program can contain more than one command. each should be on a separate line, for example::

    print("Hi,")
    print("")

    print("My name is Lucas.")

    print("")
    print("Bye.")

Blank lines do not do anything but help visually separate the various parts of the program in order to
facilitate reading its content. Here we split the message header from the content and conclusion.


BMI calculator
==============

Now we type a simple program to calculate `BMI` (`Body Mass Index`_).
The formula for its calculation is as follows:

    BMI = (mass in kg) / (height in m) squared

We know how to share, enhance, and print out the numbers. So let's create a new file called ``bmi.py``
and type a program that calculates our BMI:

.. testcode::

    print("Your BMI is:", 65.5 / (1.75)**2)

After starting::

    $ python bmi.py

In a result we get:

.. testoutput::

    Your BMI is:: 21.387755102

As you can see our program has a few problems:

1. If someone else would like to use this program, changing its content will be necessary. Furthermore 
   how he or she have to guess which values should change. 

2. For a person who does not know the value of BMI table, value `21.387755102` won’t say anything.

3. Printing so many decimal places is unnecessary. BMI is measured with an accuracy of two decimal 
   places.

But programming is finally art of solving problems, so get to work. On this occasion we will see some
new elements of Python.

.. _`Body Mass Index`: http://pl.wikipedia.org/wiki/Body_Mass_Index


Names
=====

Let’s try to solve the first problem. At the beginning we would like to make our program more readable,
that's mean that reader should have sure which value means weight and which means height.

In this purpose we will name the values:

.. testcode::

    weight = 65.5
    height = 1.75

    bmi = weight / height**2
    print("Your BMI is:", bmi)

The result of the program has not changed:

.. testoutput::

    Your BMI is: 21.387755102


To better understand how the names are working, let’s go back for a moment to the interactive mode and name something:

    >>> x = 42
    >>> PI = 3.1415
    >>> name = "Amelia"
    >>> print("Things:", x, PI, name)
    Things: 42 3.1415 Amelia

We can also give a lot of names for the same value:

    >>> y = x
    >>> print(x, y)
    42 42

We can also change the value assigned to the name. It doesn’t need to be the same type as before:


    >>> x = 13
    >>> print(x)
    13
    >>> x = "Scarab"
    >>> print(x)
    Scarab

The names are independent of each other. We have just assigned to``x``
the new value, but the value assigned to ``y`` is unchanged:

    >>> print(y)
    42

.. note:: For those who know other languages.

    You probably wonder why we do not use the term "variable". This is because the names in Python do 
    not work the same way as variables. n most languages, the operation ``y = x`` would create a copy
    of the``x`` and interceded for the variable ``y``.

    In Python nothing is ever duplicated. ``y`` becomes the only alternative name for the same value.
    If you change this value, both the``x`` and ``y`` show the same thing.

    In our example we did not change the number of  ``42``, but only the value assigned to ``x`` (in 
    particular, the numbers are immutable, but in 1897 the lower house of the Indiana accepted change
    the value of the number  π to ``3``; proposal fell only in the Senate). Therefore, ``print(y)``
    will give us ``42``.


As we saw earlier, we can give names to the results of our calculations and use it in the calculations:

    >>> w = 65.5
    >>> h = 175.0 / 100.0
    >>> bmi = w / h**2
    >>> print(w, h, bmi)
    65.5 1.75 21.387755102

But once calculated value doesn’t change:

    >>> w = 64
    >>> print(w, h, bmi)
    64 1.75 21.387755102

Unless we tell Python to calculate it again:

    >>> bmi = w / h**2
    >>> print(w, h, bmi)
    64 1.75 20.8979591837

At the end of this chapter we will add some comments to our program so the user (and ourselves)
remember that the weight has to be given in kilograms.

Comment in Python is everything after the sign ``#`` until the end of the line::

    # -*- coding: utf-8

    # Weight in kilograms
    weight = 65.5

    # Height in meters
    height = 1.75

    bmi = weight / height**2 # Count BMI
    print("Your BMI is:", bmi)

It turns out that the above mentioned formula ``coding`` was simple commentary. Ok, maybe not so 
usual, because this special comment, as distinct from others which are *completely ignored* , is
influencing program works. However, while reading the program, it can be ignored.


Calling a function
==================

Our program looks quite good, but wanting to calculate your BMI you still have to change the content
of the program.  It would be more convenient when to enter the required values ​​in the console and get
back your BMI.

To be able to write such a program we need to learn how to use the functions.
The first function we are going to learn is :func:`help`:

    >>> help
    Type help() for interactive help, or help(object) for help about object.

:func:`help` function is very friendly - it tells us how we should use it. We are also able to tell
you how to use the other functions:

    >>> help(raw_input)  # doctest: +SKIP
    Help on built-in function raw_input in module __builtin__:
    <BLANKLINE>
    raw_input(...)
        raw_input([prompt]) -> string
    <BLANKLINE>
        Read a string from standard input.  The trailing newline is stripped.
        If the user hits EOF (Unix: Ctl-D, Windows: Ctl-Z+Return), raise EOFError.
        On Unix, GNU readline is used if enabled.  The prompt string, if given,
        is printed without a trailing newline before reading. ...

func:`raw_input` will be used to load data from the user.
As at description, it's loading a string:

.. TODO : to call a function you need to add "()".

    >>> raw_input()
    Alice has a cat
    'Alice has a cat'

This function will be more useful if you remember loaded string below the name::

    >>> name = raw_input()
    Joanna
    >>> name
    'Joanna'
    >>> print('Your name is:", name)
    Your name is: Joanna

Is that enough to improve our program?

.. testsetup:: raw_input_test

    raw_input.queue.append("60.5")

.. doctest:: raw_input_test

    >>> w = raw_input()
    60.5
    >>> w
    '60.5'
    >>> print(w + 3)
    Traceback (most recent call last):
      File "<stdin>", line 1, in <module>
    TypeError: cannot concatenate 'str' and 'int' objects

As you can see, Python doesn’t know what result we expect. As we showed before, both subtitles (``str``
) and the numbers (``int``) can be added together. So, are we referring to the number ``63.5`` or to
the string ``"60.53"``? Only we know that and we have to  include this information in the program.

Let’s get to know two more functions:

    >>> help(int)  # doctest: +NORMALIZE_WHITESPACE
    Help on class int in module __builtin__:
    <BLANKLINE>
    class int(object)
    |  int(x[, base]) -> integer
    |
    |  Convert a string or number to an integer, if possible. ...

and:

    >>> help(float)  # doctest: +NORMALIZE_WHITESPACE
    Help on class float in module __builtin__:
    <BLANKLINE>
    class float(object)
    |  float(x) -> floating point number
    |
    |  Convert a string or number to a floating point number, if possible.
    |  ...

The function :func:`help` do not hesitate to inform us that, in fact,
:func:`int` and :func:`float` are not functions, but classes
(we will talk more about it later) - hence the information about all the other things that you can use
it for. For now, we are only interested in only the basic functionality of the conversion of subtitles 
for the number of the appropriate type.

Let’s try out :func:`int` and :func:`float`:

    >>> int("0")
    0
    >>> int(" 63 ")
    63
    >>> int("60.5")
    Traceback (most recent call last):
      File "<stdin>", line 1, in <module>
    ValueError: invalid literal for int() with base 10: '60.5'
    >>> float("0")
    0.0
    >>> float(" 63 ")
    63.0
    >>> float("60.5")
    60.5


Before we use the newly described functions in our program, let’s construct a plan for its activities:

1. Ask the user to enter a height
2. Load a string from the user and remember it under a name ``height``
3. Replace the string with the number of fraction
4. Ask the user to enter the weight
5. Load a string from the user and remember it under the name of ``weight``
6. Replace the string with the number of fraction
7. Using the remembered values ​​calculate BMI and save as ``bmi``
8. Print calculated BMI


t should not surprise us that these eight points can be directly translated into eight lines of our
program (not counting spaces):

.. testsetup::

    raw_input.queue.append("1.75")
    raw_input.queue.append("65.5")

.. testcode::

    print("Height in meters:")
    height = raw_input()
    height = float(height)

    print("Weight in kilograms:")
    weight = raw_input()
    weight = float(weight)

    bmi = weight / height**2 # Count BMI
    print("Your BMI is:", bmi)

.. testoutput::

    Height in meters:
    1.75
    Weight in kilograms:
    65.5
    Your BMI is: 21.387755102


In conclusion, to call the function we need to know its name (yet we met five: :func:`help`,
:func:`raw_input`, :func:`int`, :func:`float` i :func:`quit`),
and what data it expects from us (the list of arguments).

Entering the name itself does not cause the function. It will tell us only that there is a function:

    >>> raw_input  # doctest: +SKIP
    <built-in function raw_input>

All arguments are given in parentheses. To specify more than one, separate them with a comma:

    >>> int("FF", 16)
    255


Checking conditions
===================

Let’s go to our next problem. We want our program to print appropriate classification for calculated
BMI by using the table below:


=====================   ==================
   BMI                     Classification
=====================   ==================
 < 18,5                     underweight
 18,5 – 24,99              normal weight
 ≥ 25,0                      overweight
=====================   ==================


We have to use the conditional statement :keyword:`if`. It will finish the rest of the program under
one of following conditions:

.. testsetup::

    raw_input.queue.append("1.75")
    raw_input.queue.append("65.5")

.. testcode::

    print("Height in meters:")
    height = raw_input()
    height = float(height)

    print("Weight in kilograms:")
    weight = raw_input()
    weight = float(weight)

    bmi = weight / height**2 # Obliczamy BMI

    if bmi < 18.5:
        print("underweight")
    elif bmi < 25.0:
        print("normal weight")
    else:
        print("overweight")

.. testoutput::

    Height in meters:
    1.75
    Weight in kilograms:
    65.5
    normal weight

Comparisons, true or false 
--------------------------

The first element which wasn’t  mentioned yet, are comparisons. For numbers they act exactly like
during the math lessons:

    >>> 2 > 1
    True
    >>> 1 == 2
    False
    >>> 1 == 1.0
    True
    >>> 10 >= 10
    True
    >>> 13 <= 1 + 3
    False
    >>> -1 != 0
    True

The result of comparison is always ``True`` or ``False``.They can be combined into more complex
conditions by using words:keyword:`and` and
:keyword:`or`:

    >>> x = 5
    >>> x < 10
    True
    >>> 2*x > x
    True
    >>> (x < 10) and (2*x > x)
    True
    >>> (x != 5) and (x != 4)
    False
    >>> (x != 5) and (x != 4) or (x == 5)
    True


Indents
-------

Another thing you should pay attention to is the indentation in the code. Open the interactive mode
and type a simple condition, such as::

    >>> if 2 > 1:
    ...

So far nothing happened, as evidenced by a dot instead of incentives ``>>>`` that we've seen until now.
Python expects us to give more  instructions which are supposed to be done if condition ``2 > 1``
turns to be true. Then it could print "OK"::

    >>> if 2 > 1:
    ... print("OK")
      File "<stdin>", line 2
        print("OK")
            ^
    IndentationError: expected an indented block

Unfortunately, we did not succeed.Python needs to know whether the instruction we wrote is a
continuation of :keyword:`if` or the next instruction not covered by condition. To this purpose we
need to indent our code:

    >>> if 2 > 1:
    ...  print("OK")
    ...
    OK

All you need is one space or TAB. However, all the lines that are supposed to be carried one after
another, should be indented the same::

    >>> if -1 > 0:
    ...  print("A")
    ...   print("B")
      File "<stdin>", line 3
        print("B")
        ^
    IndentationError: unexpected indent

    >>> if -1 > 0:
    ...     print("A")
    ...   print("B")
      File "<stdin>", line 3
        print("B")
                ^
    IndentationError: unindent does not match any outer indentation level

    >>> if -1 > 0:
    ...   print("A")
    ...   print("B")
    ...
    A
    B


To avoid chaos, most of the Python’ programmers use four spaces for each level of indentation. We will
continue to do so:

    >>> if 2 > 1:
    ...     if 3 > 2:
    ...         print("OK")
    ...     else:
    ...         print("FAIL")
    ...     print("DONE")
    OK
    DONE


What if not? 
------------

:keyword:`if` will be actually enough for us to write our program::

    if bmi < 18.5:
        print("underweight")
    if bmi >= 18.5:
        if bmi < 25.0:
            print("normal weight")
    if bmi >= 25.0:
        print("overweight")

However, we used :keyword:`else` and :keyword:`elif` o that we won’t have to repeat similar conditions
and increase readability. In more complex programs may not be obvious at first glance that another
condition is the opposite of the previous one.

Using :keyword:`else` we have guarantee that instructions will be executed only if other instructions
haven’t been printed under :keyword:`if`:

::

    if bmi < 18.5:
        print("underweight")
    else:
        # If your program executes this statement,
        # then for sure bmi >= 18.5 !
        if bmi < 25.0:
            print("normal weight")
        else:
            # now for sure bmi >= 25.0, so we don't have to
            # check it
            print("overweight")

Pay particular attention to the indentation ;) Every use of :keyword:`else` will cause bigger indentation of our code. It is very annoying when you have to check a few or several
mutually exclusive conditions. Therefore little language "streamline" was added in the form of
instructions  :keyword:`elif`which allows you to immediately see another condition::

    if n < 1:
        print("one")
    elif n < 2:
        # if it wasn’t n < 1, a jest n < 2
        print("two")
    elif n < 3:
        # if none of the previous condition was true, that's mean
        # n >= 1 i n>= 2, but n < 3
        print("three")
    else:
        # trolls can count only to three
        print("a lot")


Strings formatting
==================

The last issue which was mentioned it was too much of digits in a printed BMI. Out of the three this
one is the easiest to solve. That’s we left it for the end of our "adventure" with a BMI calculator. 

We already know that the labels can be added to each other and multiply integers. You can also format
on them. But first we will need another data type (except the strings and the numbers we already know).


.. _bmi-tuples:

Tuples 
------

At the outset we mentioned that we can not use commas in numbers, because we will need them later to
tuples. And here they are:

    >>> 1, 2, 3
    (1, 2, 3)
    >>> ("Alice", 15)
    ('Ala', 15)
    >>> x = 1,5
    >>> print(x)
    (1, 5)

A tuple is nothing more than a few values ​​grouped into one. The whole thing can be enclosed in
parentheses for clarity but it is not required. Except when we want to group none of the element (
however strange it may sound):

    >>> ()
    ()

Tuples can be combined:

    >>> names = ("Anne", "Smith")
    >>> details = (27, 1.70)
    >>> names + details
    ('Anne', 'Smith', 27, 1.7)

They may also contain other tuples. For example the informations about a point on the map can be
grouped as follows::

    >>> point = ("Name of point", (x, y))

where ``x`` and ``y`` are numbers.

To the grouped values we can refer by using their positions in the tuple (counting form zero), eg.:

    >>> p = (10, 15)
    >>> p[0]  # first value
    10
    >>> p[1]  # second value
    15


Formatting 
----------

Returning to our program: currently the result is reduced to a single line. Now we want to write both
BMI as the number and the interval in which it is located i.e..::

    Your BMI is equal: 21.39 (normal weight)

Modify the current program so that the calculated BMI was available under the name of ``bmi``, and the
name of the compartment under the  ``category``. For wanted result we can use:func:`print`:

.. testsetup::

    bmi = 21.387755102
    category = "normal weight"

.. testcode::

    print("Your BMI is:", bmi, "(" + category + ")")

.. testoutput::
    :hide:

    Your BMI is: 21.387755102 (normal weight)

It's almost it! Still we have too much numbers.  We would also have a problem  if we wanted to
generate a string and remember it in a name because we use :func:`print` to separate the elements.
Fortunately, there is a better way:

    >>> bmi = 21.387755102
    >>> category = "normal weight"
    >>> result = "Your BMI %f (%s)" % (bmi, category)
    >>> result
    'Your BMI: 21.387755 (normal weight\u0142owa)'
    >>> print(result)
    Your BMI: 21.387755 (normal weight)

We have here a string and a tuple connected by ``%``. The string is a template which will be full of
the values ​​from the tuple. Space to insert are marked with (``%``). The letter which follow (``%``)
determines what kind of value we want to insert in its place. 
Total numbers ``i`` like **integer** (or ``d`` like **decimal**), strings ``s`` jak **string**, and 
floating point numbers ``f`` like **float**:

    >>> "String: %s, Numbers: %d %f" % ("Alice", 10, 3.1415)
    'String: Alice, Numbers: 10 3.141500'

Admittedly, now we will get six not ten decimal places, but formating have this advantage that give us
more control by puting between ``%`` and ``f`` some extra information e.g.: if we would like to show
only two decimal places. 

    >>> "%.2f" % 3.1415
    '3.14'
    >>> "%.2f" % 21.387755102
    '21.39'

There are plenty of formatting options so we will not show them all here. One of the more useful is
compensating for a specific number of characters:

.. testcode::

    WIDTH = 28

    print("-" * WIDTH)
    print("| Name and last name |  Weight |")
    print("-" * WIDTH)
    print("| %15s | %6.2f |" % ("Lucas", 67.5))
    print("| %15s | %6.2f |" % ("Nowak", 123))
    print("-" * WIDTH)

.. testoutput::

    --------------------------------
    | Name and last name | Weight |
    --------------------------------
    |              Lucas |  67.50 |
    |              Nowak | 123.00 |
    --------------------------------

We can also compensate the string to the left with the ``-`` before the number of characters:

.. testcode::

    WIDTH = 28

    print("-" * WIDTH)
    print("| Name and last name |  Weight  |")
    print("-" * WIDTH)
    print("| %-15s | %6.2f |" % ("Łukasz", 67.5))
    print("| %-15s | %6.2f |" % ("Nowak", 123))
    print("-" * WIDTH)

.. testoutput::

    --------------------------------
    | Name and last name |  Weight |
    --------------------------------
    | Lucas              |  67.50  |
    | Nowak              | 123.00  |
    --------------------------------

Compensate to the center it could be an extra exercise for you ;)


Summary
=======

In this chapter we learned basics of Python syntax. We know how to print integers, floating point
numbers, strings and tuples.

We know the function :func:`print`, which is printing the informations for the user and function
:func:`raw_input`, which is loading it from him.

We also know that indentation can be important, especially when you want to use the instruction
:keyword:`if` (also in connection with :keyword:`else` and :keyword:`elif`).

We can create a file with a program and run it. Our program asks the user to answer a few simple
questions, performs calculations and presents everything in the useful form.

Quite a lot like for the first program. We still have a lot of work, but you can be proud of what we
have done so far!
