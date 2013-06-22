===========
Instllation
===========

During our workshops we will need an interpreter for Python language, version 3.2. or 3.3. There are 
some tips below how to easily check if we already have interpreter we need or how install it quickly:

Windows
=======

You can download it directly from python.org. After download of file ``*.exe``, please start the program 
and then follow the instructions. It is important to remember path of installation, because it will be 
helpful during the installation of tools :ref:`installation of tools <tools>`.


Linux (Ubuntu, Fedora, etc.) or Mac
===================================

Check in your Command Line by:

.. code-block:: sh

    $ python --version
    Python 3.3.1


If the command python is not available or if it prints the wrong version:

Ubuntu
------

Write in a command line type::

    sudo apt-get install python3

Fedora
------

Write in a command line type::

    sudo yum install python3

OS X
----

Download and install the package for your version from `python.org`_.


Others
------

Use the package system from your Linux distribution. If it dosen't exist or you can't find Python, 
then you can install it using the `python.org`_ sources. You should have a compiler and  readline 
library.

Silently we assume that users of less popular (not to say worse) distribution certainly will cope with 
this task :).



.. _tools:

Tools
=====

Windows command line
--------------------

Most of the work we will do from a command line. To run a command line in Windows please click on 
``Start`` and then ``Uruchom...``. In a open window type ``cmd`` and click ``OK``. New window will 
appear with a white text on black background:


.. code-block:: bat

    Microsoft Windows [Version 6.1.7601]
    Copyright (c) 2009 Microsoft Corporation. All rights reserved.

    C:\Users\Imie>

Text may be different depending on version of Windows you use.

``C:\Users\Imie>`` is a ``prompt``. It informs us of the directory in which we are currently in and 
waits for the command. Later ``C:\Users\Imie>`` we will cut to the  ``~$``, independently of your 
operating system (Windows, Linux, MacOS).

From the command line you can move up and down to drive (similarity as in "My computer"). There are
the commands for that:

``dir``
    Displays the contents of the current directory. For example, if the ``prompt``
    shows ``C:\Users\Imie``, the ``dir`` command displays the contents of our home directory.


``cd katalog``
    Change of the current directory. For example, while you’re in the ``C:\Users\Imie``,
    execute  ``cd Documents`` will access the directory with our data. You can now check what will 
    execute the ``dir`` command and see something familiar.

    The command ``cd..`` will move you to the upper directory.

``mkdir directory``
    Create a new directory.


The virtual environment
-----------------------

While we already have our well working Python, let’s install one more program which will simplify
installation of other programs and improve our work.


Download the script `virtualenv.py`_ o your home directory and open the console.

.. code-block:: bat

    :: Windows
    C:\Users\lrekucki> C:\Python33\python virtualenv.py workshops --system-site-packages --distribute

.. code-block:: sh

    # Linux i Mac
    ~$ python3.3 virtualenv.py workshops --system-site-packages --distribute --python=python3


In your home directory will appear directory ``workshops`` containing co-called virtual environment. 
For now, it is important for us that after it’s activation:

.. code-block:: bat

    :: Windows
    C:\Users\lrekucki> workshops\Scripts\activate

.. code-block:: sh

    # Linux i Mac
    ~$ source workshops/bin/activate

Python command will run good version of Python, so we will not have to type the full path to the 
beginning or to the end of version.

Run in a terminal

.. code-block:: bat

    :: Windows
    (workshops) C:\Users\lrekucki>where python
    C:\Users\lrekucki\workshops\Scripts\python.exe
    ...

    (workshops) C:\Users\lrekucki>python --version
    3.3.1

.. code-block:: sh

    # Linux i Mac
    (workshops) ~$ which python
    /home/lrekucki/workshops/bin/python.exe
    ...

    (workshops) ~$ python --version
    3.3.1


.. _python.org: http://python.org/download/releases/3.3.1/
.. _virtualenv.py: https://raw.github.com/pypa/virtualenv/c881ae56d34a578b3f61326ed7745ef2e6d269d0/virtualenv.py


IPython
-------

Install ``IPython``

.. code-block:: sh

    (workshops) ~$ pip install ipython
