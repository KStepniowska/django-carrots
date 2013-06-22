==================
  Christmas tree
==================

Christmas are coming (or not ;)), time for Christmas trees :) As an exercise, try to draw a tree in
the console.

We are going to start from the simpliest version of this exercise so that we can later extend it to a
more functional.

.. testcode::

    print("*")
    print("**")
    print("***")
    print("*")
    print("**")
    print("***")
    print("****")
    print("*")
    print("**")
    print("***")
    print("****")
    print("*****")
    print("******")

.. testoutput::

    *
    **
    ***
    *
    **
    ***
    ****
    *
    **
    ***
    ****
    *****
    ******

It doesn’t look bad but it required a lot of typing. But what if we would like to have smaller tree?
Or bigger, composed of hundreds of elements to be printed on paper A0? Still too much typing even if
we will use strings multiplication (``"*" * 100``, etc.). Obviously this is such repetitive activity
that the program can do it for us.



Lists and loop ``for``
======================

Loops will serve us to deal with such repetitive actions.
Staying in the Christmas convention, imagine for a moment that we are Santa Claus and we have to
provide all the gifts.

As you know, Santa has a list of people who deserve gifts. The simplest way, which guarantees to not
overlook anyone, will be running through the list and delivering presents to the consecutive people.
In abstraction from physical aspects of task [#speed]_, deliver gifts procedure could look like this::

    Let the People List contains people who should be gifted.

    For each person (known as the person), which is on the list of people:
        Provide a gift to person

Formatting of text above is not accidental. This is actually a disguised program in Python::

    gift_list = people_who_deserve_gifts()

    for person in gift_list:
        deliver_gift(person)
        print("Delivered gift for:", person)
    print("Delivered all gifts")

Most of the things should looks familiar for you. We are calling here two functions:
:func:`people_who_deserve_gifts` and :func:`deliver_gift` - How does they working? - that's only
Santa's know. Result of the first one can be named `gift_list`, to could use this value later (the
same as described above).

A new element is a loop itself, which comprises:

* Words :keyword:`for`
* The names we want to give to the next elements.
* Words :keyword:`in`
* value which is a list or name that refers to this.
* Content indented of one level (exactly the same as it was in the :keyword:`if` case)

Still we didn’t say anything about lists. We can easily think of lists in Python as we think of any
other list (shopping list, guest list, etc.) saved on a paper and numbered.

Let's start with a blank page (on interactive mode):

    >>> L = []
    >>> L
    []

At any time we can see how much items we saved on our list by using the function :func:`len`.

    >>> len(L)
    0

Let's make another list (which may be of the same name or different):

    >>> L = ["Alice", "Ola", "Jack"]
    >>> len(L)
    3

As in the case of tuples, another elements of lists are separated by commas. Unlike tuples, brackets ``
[`` i ``]`` are mandatory.

To preview a particular position of element on the list (remember that we count from 0 items):
    >>> L[0]
    'Alice'
    >>> L[1]
    'Ola'
    >>> L[2]
    'Jack'
    >>> L[3]
    Traceback (most recent call last):
     File "<stdin>", line 1, in <module>
    IndexError: list index out of range

We can also use a loop :keyword:`for`, to effectuate an instruction for every element from the list:

    >>> for name in L:
    ...     print("Name:", name)
    ...
    Name: Alice
    Name: Ola
    Name: Jack

In the same way, we can print the first part of our half-tree:

    >>> lst = [1, 2, 3]
    >>> for n in lst:
    ...     print("*"*n)
    ...
    *
    **
    ***

Still we had to hand-write the entire contents of the list.
This problem can be solved by function :func:`range`.
If a description in ``help(range)`` seems you too difficult, here are a few examples:

    >>> range(2, 5, 1)
    [2, 3, 4]
    >>> range(1, 11, 2)
    [1, 3, 5, 7, 9]
    >>> range(1, 11)
    [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
    >>> range(1, 2)
    [1]
    >>> range(2)
    [0, 1]

This last form, with single argument which create the list from zero to labeled number (but always
without that number!), is used the most often. 

Let’s print our Christmas tree:

    >>> lst = range(1, 11)
    >>> lst
    [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
    >>> for i in lst:
    ...     print("*"*i)
    *
    **
    ***
    ****
    *****
    ******
    *******
    ********
    *********
    **********

:func:`range` saved our time. We can save even more apart from calling the same list:

    >>> for i in range(1, 5):
    ...     print(i*"#")
    #
    ##
    ###
    ####

Nothing stands in the way of the loop being in another loop. Just be aware of the appropriate
indentation and using other names (e.g.: ``i`` i ``j``, or some more adequate to the list content):

    >>> for i in range(1, 3):
    ...    for j in range(2, 4):
    ...        print(i, j)
    1 2
    1 3
    2 2
    2 3

Using this technique, we can repeat our piece of the Christmas tree:

    >>> for i in range(3): # repeat 3 times
    ...    for size in range(1, 4):
    ...        print(size*"*")
    *
    **
    ***
    *
    **
    ***
    *
    **
    ***

Before proceeding to the next chapter, create ``xmas.py`` file with this program and try to modify it
so that each of the three repetitions of the first (outer) loop, the second performed once more. In
this way, we should get our half-tree at the beginning of the chapter.


Defining a function
===================

We have already seen how functions solve many of our problems. However,they not solve them all. 
Then we must solve the problem on our own. If it occurs often in our program, it would be nice to have
a function that solves it.

Python gives us this opportunity:


    >>> def print_triangle(n):
    ...     for size in range(1, n+1):
    ...         print(size*"*")
    ...
    >>> print_triangle(3)
    *
    **
    ***
    >>> print_triangle(5)
    *
    **
    ***
    ****
    *****

Let's take a closer definition of the function :func:`print_triangle`:

    def print_triangle(n):
        for size in range(1, n+1):
            print(size*"*")

The definition of a function always starts with the word :keyword:`def`. Next, we give the name to our
function. In parentheses we give names of its arguments. In the following lines we provide
instructions to be executed when we will use a function.

As we can see on the examples, instructions in the function could include name, which we chose as a
argument names. The principle of operation is as follows - if you have created a function with three
arguments:

    >>> def foo(a, b, c):
    ...     print("FOO", a, b, c)

This is causing the need to specify values ​​for each of the arguments:

    >>> foo(1, "Ala", 2 + 3 + 4)
    FOO 1 Ala 9
    >>> x = 42
    >>> foo(x, x + 1, x + 2)
    FOO 42 43 44

Note that the name is just a label. If we move label with one value to another, other labels will not
change - it will also work well with the arguments:

    >>> def plus_five(n):
    ...     n = n + 5
    ...     print(n)
    >>> x = 43
    >>> plus_five(x)
    48
    >>> x
    43


Returning values
----------------

The functions which we have previously enjoyed had one important property that is missing in functions
created by ourselves - they returned value instead of immediately print it To achieve the same effect,
use the statement :keyword:`return`. This is a special instruction that can be found only in the
function.

We can now improve our BMI calculator by adding a function to compute BMI::

    def calc_bmi(height, weight):
        return weight / height ** 2

Finally, we solve the problem in an elegant way from the end of the previous chapter:


.. testcode::

    # xmas.py

    def print_triangle(n):
        for size in range(1, n+1):
            print(size * "*")

    for i in range(2, 5):
        print_triangle(i)


.. testoutput::

    *
    **
    *
    **
    ***
    *
    **
    ***
    ****


Objects and classes
===================

In fact, this chapter could be the subject of a series of activities, but we will focus on absolute
grounds which we will need when working with Django.


Values are objects 
------------------

Everything that we have been calling the value we can call it an object.
We saw an example of integers, when :func:`help` printed for us a dozens of additional lines of
information about :func:`int`.

Every object has class
----------------------

If you want to know how use function :func:`type`:

    >>> type(2)
    <type 'int'>
    >>> type(2.0)
    <type 'float'>
    >>> type(u"Gżegżółka")
    <type 'unicode'>
    >>> x = 1, 2
    >>> type(x)
    <type 'tuple'>
    >>> type([])
    <type 'list'>

GWhen we use in our program numbers, we expect that it will behave like a number - we rely on our
intuition. 

However, Python has to know exactly what it means to be an integer, for example, what happens when we
add the two numbers and when we divide it. Class provides all this information and more.

Check out what gives us class ``unicode`` by using :func:`help`.
Here are only a few interesting features:

    >>> help(unicode.lower)
    Help on method_descriptor:
    <BLANKLINE>
    lower(...)
        S.lower() -> unicode
    <BLANKLINE>
        Return a copy of the string S converted to lowercase.
    <BLANKLINE>
    >>> help(unicode.upper)
    Help on method_descriptor:
    <BLANKLINE>
    upper(...)
        S.upper() -> unicode
    <BLANKLINE>
        Return a copy of S converted to uppercase.
    <BLANKLINE>
    >>> help(unicode.ljust)
    Help on method_descriptor:
    <BLANKLINE>
    ljust(...)
        S.ljust(width[, fillchar]) -> int
    <BLANKLINE>
        Return S left-justified in a Unicode string of length width. Padding is
        done using the specified fill character (default is a space).
    <BLANKLINE>
    >>> help(unicode.center)
    Help on method_descriptor:
    <BLANKLINE>
    center(...)
        S.center(width[, fillchar]) -> unicode
    <BLANKLINE>
        Return S centered in a Unicode string of length width. Padding is
        done using the specified fill character (default is a space)
    <BLANKLINE>

All these are operations that each string can do. We can get to them by using dots and calling the
function:

    >>> x = u"Alice"
    >>> x.upper()
    u'ALICE'
    >>> x.lower()
    u'alice'
    >>> x.center(9)
    u'   Alice   '

And one more important function of each class - it can create an object with its attributes:

    >>> int()
    0
    >>> str()
    ''
    >>> list()
    []
    >>> tuple()
    ()


Define classes
--------------

Just as you can create your own functions, so you can create your own class. In fact, the class is
nothing but grouped functions:

.. testsetup:: simple-class

    class Dog(object):

        def bark(self):
            print(u"Woof! Woof!")

::

    class Dog(object):

        def bark(self):
            print(u"Woof! Woof!")

Classes begin with the word :keyword:`class`, after which we give the name of the new class. What is
``(object)`` will become clear later, when we will want to create a more complex class.

Draw attention to the fact that every function in the class must have at least one argument.  Its
value is an object from which we called this function ( before the dot):

.. testcode:: simple-class

    snoopy = Dog()
    snoopy.bark()

.. testoutput:: simple-class

    Woof! Woof!

This argument can be called arbitralily, but it is intuitive to call it ``self``.


Attributes of objects
---------------------

Objects besides functions can also have attributes:

.. testcode:: simple-class

    snoopy = Dog()
    snoopy.name = "Snoopy"

    print(snoopy.name)

.. testoutput:: simple-class

    Snoopy

Sometimes we want for every object of the class to have some attribute, such as every dog ​​should have
a name. We can add this requirement by defining a function with a special name ``__init__``:

.. testcode:: init-class

    class Dog(object):

        def __init__(self, name):
            self.name = name

        def bark(self):
            return "Woof! %s! Woof!" % (self.name,)

    snoopy = Dog(u"Snoopy")
    pluto = Dog(u"Pluto")
    print(snoopy.bark())
    print(pluto.bark())

.. testoutput:: init-class

    Woof! Snoopy! Woof!
    Woof! Pluto! Woof!


Full Christmas tree
===================

The previous chapter was fairly theoretical, so now we'll try to take at least part of this knowledge
by completing our program to display a Christmas tree.

For the record::

    # xmas.py

    def print_triangle(n):
        for size in range(1, n+1):
            print(size * "*")

    for i in range(2, 5):
        print_triangle(i)

How can we improve the function :func:`print_triangle`, to display the entire segment of tree, not
just half of it?

First of all, let’s determine how we want our result look like for the value of argument ``n``. It
seems to make sense that, ``n`` got to be the width.
Then for ``n = 5``, we would expect::

      *
     ***
    *****

It is worth noting that each line consists of two stars more than the previous one. So we can use the
third argument :func:`range`:

.. testcode::

    def print_segment(n):
        for size in range(1, n+1, 2):
            print(size * "*")

    print_segment(5)

.. testoutput::

    *
    ***
    *****

There is still a lack of alignment. With the help comes :func:`unicode.center` mentioned in the
previous section:

.. testcode::

    def print_segment(n):
        for size in range(1, n+1, 2):
            print((size * "*").center(n))

    print_segment(5)

.. testoutput::
    :options: +NORMALIZE_WHITESPACE

      *
     ***
    *****

Another problem appears:

.. testcode::

    def print_segment(n):
        for size in range(1, n+1, 2):
            print((size * "*").center(n))

    for i in range(3, 8, 2):
        print_segment(i)

.. testoutput::
    :options: +NORMALIZE_WHITESPACE

     *
    ***
      *
     ***
    *****
       *
      ***
     *****
    *******

Since know in advance what will be the widest segment size, we can add an additional argument to  :func:`print_segment`, to compensate for the width. Combining all of our current knowledge:

.. testsetup:: tree-final

    raw_input.queue.append("7")

.. testcode:: tree-final

    def print_segment(n, total_width):
        for size in range(1, n+1, 2):
            print((size * "*").center(total_width))

    def print_tree(size):
        for i in range(3, size+1, 2):
            print_segment(i, size)

    print(u"Enter size of tree:")
    n = int(raw_input())
    print_tree(n)

.. testoutput:: tree-final
    :options: +NORMALIZE_WHITESPACE

    Enter size of tree:
    7
       *
      ***
       *
      ***
     *****
       *
      ***
     *****
    *******


Task for willing 
----------------

Create a class ``XMASTree`` which for a given size and method ``draw``, will print the pictures below (
sizes 1, 2 and 3):

::

          *
         /|\
        /_|_\
          |

::

           *
          /|\
         /_|_\
          /|\
         / | \
        /__|__\
           |

::

            *
           /|\
          /_|_\
           /|\
          / | \
         /__|__\
           /|\
          / | \
         /  |  \
        /___|___\
            |



.. rubric:: Annotations

.. [#speed] In assumption that we have 24 h to drop off one gift to the eachperson in the world, then 
    it's 10 microsecond for each gift.
