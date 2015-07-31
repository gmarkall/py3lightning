
.. Python 3# slides file, created by
   hieroglyph-quickstart on Fri Jul 31 10:02:18 2015.


Python 3
========

Ian Ozsvald, Graham Markall


Python 3 Improvements over Python 2
-----------------------------------

An incomplete list:

- Unicode improvements, Exception chaining, unpacking generalisations, asyncio,
  :code:`async`/:code:`await`, fine-grained :code:`OSError` subclasses,
  :code:`yield from`, fault handlers, unorderable types, type hints, ...

We'll briefly demo now:

- Matrix multiplication :code:`@` operator
- Advanced unpacking
- Keyword-only args
- Iterators everywhere


Matrix Multiplication - :code:`@` operator
------------------------------------------

.. math::

   MM^TNv

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

.. code-block:: python

   >>> a, b, *rest = range(10)
   >>> a
   0
   >>> b
   1
   >>> rest
   [2, 3, 4, 5, 6, 7, 8, 9]

:code:`*rest` can go anywhere:

.. code-block:: python

   >>> a, *rest, b = range(10)
   >>> a
   0
   >>> b
   9
   >>> rest
   [1, 2, 3, 4, 5, 6, 7, 8]


Advanced Unpacking - example
----------------------------

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

Problem: pass too many arguments to a function, one gets swallowed by a kwarg.

.. code-block:: python

   def cleanup(folder, extreme=False):
       if extreme:
           shutil.rmtree('/')
       else:
           shutil.rmtree(folder)

OK:

.. code-block:: python

   >>> cleanup('/home/gmarkall/tmp')

Not OK:

.. code-block:: python

   >>> cleanup('/home/gmarkall/tmp', '/home/gmarkall/tmp2')


Keyword-only Args (2)
---------------------

Solution: use a Keyword-only arg

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


Iterators Everywhere
--------------------

Python 2:

.. code-block:: python

   >>> for i in range(100000000000):
           print(i)
       Traceback (most recent call last):
         File "<stdin>", line 1, in <module>
       MemoryError

Python 3:

.. code-block:: python

   >>> for i in range(100000000000):
           print(i)
   1 ...
   99999999999

Benfits: consistent API, no accidental performance hits from not using
iterators!

Compatibility
-------------

`py3readiness.org <http://py3readiness.org>`_

.. image:: /_static/py3readiness.png
   :align: center


Compatibility - 2
-----------------

- Pretty much all data science packages Python 3 compatible
- e.g. numpy, scikit-learn, pandas, ipython pymongo, PyMySQL, numba, flask,
  django, awscli, redis, Pillow, bs4, matplotlib, etc, ...
- One (eroding) exception, Scrapy:

  - Python 3 support getting there: https://github.com/scrapy/scrapy/issues/263
  - Europython sprint for Python 3 removed blockers: Request / Response objects
  - Get involved!


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

- 2to3: mechanical conversion of Python 2 code to Python 3 code
- six / future: compatibility layers for Python 2 and 3

  - use Python 3 features, keep compatibility with Python 2

- conda package manager: Easy switching between Python 2 and 3 environments
- Use `python3porting.com <http://python3porting.com>`_ as a resource
- Have lots of unit tests!

  - Talk to `Dave MacIver <https://twtiter.com/drmaciver>`_ about this!

- Use CI, e.g. Travis for testing with multiple versions


Conclusion
----------

- The time to move is now!
