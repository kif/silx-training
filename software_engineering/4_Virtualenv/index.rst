
.. raw:: html

   <!-- Patch landslide slides background color --!>
   <style type="text/css">
   div.slide {
       background: #fff;
   }
   </style>

Virtual environments for Python
===============================

What is a virtual environment
-----------------------------

A Virtual Environment is a tool to keep the dependencies required by different projects in
separate places, by creating virtual Python environments for them.

Each can have a different version of Python, and a different set of libraries.

It's main purpose is to create an isolated environment.

----


Specific purposes
-----------------

Users and production servers
****************************

- installing new software with modern library dependencies, without breaking older software relying on older versions of the same libraries
- sharing an environment, isolated from the system and users libraries, between different users

Using virtual environments is becoming our preferred way of installing new python software for users.

Developers
**********

- testing installer scripts: are all necessary dependencies correctly installed on a blank system?
- testing that your software works with different sets of libraries (e.g PyQt4, PyQt5, PySide), or different versions of a single library

Testing usages can be automated with *continuous integration*.


----

Installing:
-----------

Python 2
********

.. code-block:: shell
    
    pip install virtualenv --user

.. note::

    On Debian 8 and some Ubuntu versions, ``virtualenv`` is provided by the package *python-virtualenv*.

Python 3
********

Already shipped as a standard library (Python >= 3.3): ``venv``

.. note::

    The package  *python3-venv* is required on Debian 8 for ``venv`` to work properly.

----

Creating a virtualenv
---------------------

This will create a new directory ``myvenv`` in the current directory,
containing the python interpreter with its standard library, *pip*,
and a *site-packages* directory for installing additional libraries.

Python 2
********

.. code-block:: shell
    
    virtualenv myvenv

Python 3
*********

.. code-block:: shell
    
    python3 -m venv myvenv


----

Creating a virtualenv (alternatives)
------------------------------------

Alternative using Python 2's virtualenv for Python3 environment:

.. code-block:: shell

    # pip install virtualenv --user
    virtualenv --python=/usr/bin/python3.4 myvenv

Alternative by installing pip separately from ``myvenv``, if the regular method
causes an error (try installing *python3-venv* first, if you can):

.. code-block:: shell

    python3 -m venv --without-pip myvenv
    source myvenv/bin/activate
    # install pip
    curl https://bootstrap.pypa.io/get-pip.py | python

----

Activating a virtual env
------------------------

.. code-block:: shell
    
    source myvenv/bin/activate

While this virtual environment is active:

- the command ``python`` calls the python installed in ``myvenv``, and it is not aware of user libraries outside the environment.
- the command ``pip`` installs new libraries inside the environment

To deactivate the environment later, use the following command:

.. code-block:: shell

    deactivate


----
        
Upgrade pip, setuptools and wheel
---------------------------------

The *pip* command and the *setuptools* and *wheel* libraries in your new virtual environment
are copies (or links to) the system's *pip*, *setuptools* and *wheel*.  They might be outdated.



This step ensures that you will be able to install modern software and libraries.

.. code-block:: shell

   python -m pip install --upgrade pip
   pip install setuptools --upgrade
   pip install wheel --upgrade

    
----

Installing libraries
--------------------

As an exercise, let's install *silx* and its dependencies.

Some dependencies can simply be installed from pypi:

.. code-block:: shell

    pip install numpy cython
    pip install matplotlib fabio h5py qtconsole pyopencl mako


PyQt5 wheels are provided for some Python version (OK for Python 3.5 & 3.6):

.. code-block:: shell

    pip install PyQt5

----

Installing from sources
-----------------------

``pip`` preferably installs pre-compiled wheels when they are available for your platform.
Wheels remove the burden of having to install a compiler (great for Mac and Windows).

On linux, *manylinux1 wheels* are available and simplify the installation of packages.
These wheels are compiled with old tools and libraries, trading performances (~20% slower) for compatibility with any linux distributions.

When performance matters, you should install packages by compiling their
sources. This can be tricky.

Example for *numpy* (https://pypi.python.org/pypi/numpy#downloads):

.. code-block:: shell

    unzip numpy-1.12.1rc1.zip
    cd numpy-1.12.1rc1/
    pip install .

Easier alternative (recent ``pip`` required):

.. code-block:: shell

    pip install --no-binary :all: numpy


----

Symbolic link to library (linux)
--------------------------------

**This is a hack!**

If no wheel is available for your environment, and compiling from scratch is too complicated, it can be simpler to
just add symbolic links in the virtual environment, pointing to the libraries already installed on the system
**and to their dependencies**.

Example for *PyQt4* (depends on *sip*):

Python 2.7
**********

.. code-block:: shell

    ln -s /usr/lib/python2.7/dist-packages/PyQt4 \
        myvenv/lib/python2.7/site-packages/
    ln -s /usr/lib/python2.7/dist-packages/sip.so \
        myvenv/lib/python2.7/site-packages/


Python 3.4
**********

.. code-block:: shell

    ln -s /usr/lib/python3/dist-packages/PyQt4 \
        myvenv/lib/python3.4/site-packages/
    ln -s /usr/lib/python3/dist-packages/sip.cpython-34m-x86_64-linux-gnu.so \
        myvenv/lib/python3.4/site-packages/


----

Installing silx
---------------

Distribution
************

.. code-block:: shell

    pip install silx

From sources
************

.. code-block:: shell

    cd /path/to/silx
    pip install .

Test it
*******

.. code-block:: python

    >>> import silx
    >>> print(silx.version)
    0.5.0-dev0

..    >>> import silx.test
..    >>> silx.test.run_tests()

----


Managing multiple environments
------------------------------

`Python Env Wrapper (pew) <https://pypi.python.org/pypi/pew>`_  is a tool for managing
multiple virtual environments.

.. code-block:: shell

    $ pew new venv3
    $ pew ls
    venv1 venv2 venv3
    $ pew workon venv1
    Launching subshell in virtual environment. Type 'exit'
    or 'Ctrl+D' to return.
    $ which python
    /home/arthur/.virtualenvs/venv1/bin/python

Run a program that depends on a particular environment:

.. code-block:: shell

    $ pew in venv2 myscript.py


More than 20 commands available:

*help, inall, show, rm, cp, rename, mktmpenv, lssitepackages, restore, wipeenv, mkproject* ...



----

Alternatives: Anaconda
----------------------

`Anaconda <https://www.continuum.io/downloads>`_

Includes over 100 of the most popular Python, R and Scala packages for data science.

Uses its own package manager (``conda install``), but can use ``pip`` as well for packages
not managed by conda.

Separating different environments: ``conda create -n myenv python``

License issue: Anaconda is installed with `mkl <https://software.intel.com/en-us/intel-mkl>`_,
which cannot be included if you want to package your application as a fat binary.

.. code-block:: shell

    conda install nomkl numpy scipy scikit-learn numexpr
    conda remove mkl mkl-service


`Miniconda <https://conda.io/miniconda.html>`_

Smaller version of Anaconda with Python, conda and essential packages (numpy)

----

Alternatives: WinPython
-----------------------

`WinPython <http://winpython.github.io/>`_

Python distribution for scientific and educational usage

Only for Windows 7/8/10

Install as many isolated and self-consistent environments as needed.










