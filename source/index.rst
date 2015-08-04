
.. Python 3 slides file, created by
   hieroglyph-quickstart on Fri Jul 31 10:02:18 2015.


Move to Python 3!
=================


Graham Markall - `@gmarkall <https://twitter.com/gmarkall>`_

Ian Ozsvald - `@ianozsvald <https://twitter.com/ianozsvald>`_, `ianozsvald.com <http://ianozsvald.com>`_

|
|

.. image:: /_static/ccby.svg


`https://github.com/gmarkall/py3lightning <https://github.com/gmarkall/py3lightning>`_


Py3 Improvements over Py2
-----------------------------------

An (incomplete) list:

- Unicode improvements, Exception chaining, unpacking generalisations, asyncio,
  :code:`async`/:code:`await`, fine-grained :code:`OSError` subclasses,
  :code:`yield from`, fault handlers, unorderable types, type hints, iterators
  everywhere...

Brief demos of:

- Matrix multiplication :code:`@` operator
- Advanced unpacking
- Keyword-only args


Matrix Multiplication - :code:`@` operator
------------------------------------------

.. image:: /_static/matexpr.png
   :align: center
   :width: 200

Old "syntax":

.. code-block:: python

   M.dot(M.T).dot(N.dot(v))

New syntax:

.. code-block:: python

   (M @ M.T) @ N @ v

Defining matrix multiplication for your own classes:

.. code-block:: python

   def __matmul__(self, other)  # @
   def __rmatmul__(self, other) # @
   def __imatmul__(self, other) # @=


Advanced Unpacking
------------------

Get "everything else" from an iterable:

.. code-block:: python

   >>> a, b, *rest = range(10)
   >>> a
   0
   >>> b
   1
   >>> rest
   [2, 3, 4, 5, 6, 7, 8, 9]

Get the first and last lines of a file:

.. code-block:: python

   >>> with open('using_python_to_profit.txt') as f:
           first, *_, last = f.readlines()
   >>> first
   'Step 1: Use Python 3\n'
   >>> last
   'Step 10: Profit!\n'


Keyword-only Args
-----------------

.. code-block:: python

   def cleanup(folder, *, extreme=False):
       if extreme:
           shutil.rmtree('/')
       else:
           shutil.rmtree(folder)

.. code-block:: python

   >>> cleanup('/home/gmarkall/tmp', '/home/gmarkall/tmp2')
   Traceback (most recent call last):
   File "<stdin>", line 1, in <module>
   TypeError: cleanup() takes 1 positional argument but 2 were given


.. image:: /_static/drmkwargs.png
   :align: center
   :width: 500

Compatibility with common libraries
-----------------------------------

.. image:: /_static/py3liblogos.png

Py3-only libraries
------------------

.. image:: /_static/whymovenow.png

“Ubuntu 15.10 (Wily Werewolf) to Switch to Python 3.5 Ahead of Ubuntu 16.04 LTS”


How to upgrade
--------------

- **2to3**: mechanical conversion of Py2 code to Py3 code
- **six** / **future**: compatibility layers for both 2 and 3

  - use Python 3 features, keep compatibility with Python 2

- **conda** package manager: Easily switch between Python 2 and 3 environments

  - :code:`conda create -n py34 python=3.4 anaconda`

- **Resource**:: `python3porting.com <http://python3porting.com>`_
- **Unit tests**: have lots of them!

  - Talk to `Dave MacIver <https://twtiter.com/drmaciver>`_ about this (and
    Hypothesis)!

- **Use CI**: e.g. Travis for testing with multiple versions

- **New projects**: Start in Py3, backport only if necessary
