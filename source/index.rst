
.. Python 3# slides file, created by
   hieroglyph-quickstart on Fri Jul 31 10:02:18 2015.


Python 3
========

Ian Ozsvald, Graham Markall


Matrix Multiplication
---------------------

Using the :code:`@` operator

.. math::

   MM^TNv

Old "syntax":

.. code-block:: python

   M.dot(M.T).dot(N.dot(v))

New syntax:

.. code-block:: python

   (M @ M.T) @ N @ v

