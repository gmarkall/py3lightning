
.. Python 3# slides file, created by
   hieroglyph-quickstart on Fri Jul 31 10:02:18 2015.


Move to Python 3!
=================

Ian Ozsvald, Graham Markall


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


Py3-only libraries
------------------

The flip side of the compatibility coin: Python 2 is getting left behind/moving
to paid support for new libraries:

- Geophysical data: `SegPy <https://github.com/sixty-north/segpy>`_
- Anything using :code:`asyncio`, see `aio-libs Github
  <https://github.com/aio-libs>`_

  - Python 3.5 has :code:`async`/:code:`await` - more movement in this direction

- `viewflow.io <http://viewflow.io>`_ Python 2 is paid-for support

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
