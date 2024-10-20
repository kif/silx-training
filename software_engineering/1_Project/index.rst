
.. raw:: html

   <!-- Patch landslide slides background color --!>
   <style type="text/css">
   div.slide {
       background: #fff;
   }
   </style>

1. Structure your project
=========================

#. Have a clean structure
#. A word about licenses
#. Coding convention

   #. PEP8
   #. PEP20

#. Version control system

   #. Git version control
   #. GitHub and alternatives
   #. Different types of workflow


----

Have a clean Structure
----------------------

- Separate library from scripts:

  * libraries are reuseable

- Separate GUI from calculation:

  *  Otherwise maintenance becomes a nightmare
  *  allows to change the front-end
  *  allows to access to core function without the GUI

- Separate I/O from calculation

- Define a license for your work.

----

A word about Licenses
---------------------

According to the French law, one should distinguish authorship from ownership:

 - Authorship is inalienable: your work becomes public domain 50 years after
   your death.
 - ESRF, your employer, owns the code you may have written during your contract
   (unless you can prove this development has no correlation with your work)

Licenses define how a piece of software can be used (and sometimes what for).
None of them claim any liability of the author.

----

One can define 2 categories:
----------------------------

- Proprietary licenses

  * Commercial licenses: one needs to purchase a license to use the code
  * Academic licenses: free for academic research

- Open source licenses:

  * GPL like which allows the distribution of modified code but enforces the
    publication of the modification
  * MIT/BSD which provides the name of the author for information
    (for scientific citation)

The Python scientific stack has a BSD-like licenses.
Defining licenses for your developments is important as the beamline can not
build code on top of unlicensed or proprietary work without explicit license
agreement.

DAU strongly recommends a MIT license.

----

Coding convention
=================

----

Transition to Python3
---------------------

By 2020, the support of Python2 will end.
Supporting Python3 is a must have today.

Look at the download statistics of projects like
`WinPython <https://sourceforge.net/projects/winpython/files/>`_: about 7000 downloads/week for Python_3.x vs 1200 for Python_2.7

Today, in 2017, one should not start a Python2 (only) project.
To ensure a smoother transition, and acquire the Python3 requested practices:

.. code-block:: python

   from __future__ import division, absolute_import, \
       print_function #, unicode_literals

Use the `six library <https://pypi.python.org/pypi/six>`_ to provide code that
runs both under Python2 and Python3.

----

Coding convention: `PEP8 <https://www.python.org/dev/peps/pep-0008/>`_
----------------------------------------------------------------------

- Wrap lines at 79 char.
- Indent with 4 spaces.
- Put spaces around arguments (except in function declaration).
- English docstrings and triple quoted.
- One single import per line.
- Variable, method, modules name should be lower_case
  (with underscore, only if needed).
- Constant should be UPPER_CASE (with underscores).
- Class names should be CamelCased.
- Single letter variable should be limited to loop indexes.
- One single statement per line
- Two empty lines between top-level objects, only one later.

`PEP 7 <https://www.python.org/dev/peps/pep-0007/>`_: Style Guide for C Code

----

Zen of Python: `PEP20 <https://www.python.org/dev/peps/pep-0020/>`_
...................................................................

.. code-block:: python

   import this

::

 Beautiful is better than ugly.
 Explicit is better than implicit.
 Simple is better than complex.
 Complex is better than complicated.
 Flat is better than nested.
 Sparse is better than dense.
 Readability counts.
 Special cases aren't special enough to break the rules.
 Although practicality beats purity.
 Errors should never pass silently.
 Unless explicitly silenced.
 In the face of ambiguity, refuse the temptation to guess.
 There should be one-- and preferably only one --obvious way to do it.
 Although that way may not be obvious at first unless you're Dutch.
 Now is better than never.
 Although never is often better than *right* now.
 If the implementation is hard to explain, it's a bad idea.
 If the implementation is easy to explain, it may be a good idea.
 Namespaces are one honking great idea -- let's do more of those!

----

Tools
-----

* `flake8 <https://pypi.python.org/pypi/flake8>`_
* `pylint <https://www.pylint.org/>`_
* `modernize <https://pypi.python.org/pypi/modernize>`_
* `autopep8 <https://pypi.python.org/pypi/autopep8>`_
* `landscape.io <https://landscape.io/>`_: `Example <https://landscape.io/github/silx-kit/silx/>`_
* IDE

  - `pyDev (eclipse) <http://www.pydev.org/>`_
  - `pycharm <https://www.jetbrains.com/pycharm/>`_

----

Version Control System
----------------------

.. image:: http://www.phdcomics.com/comics/archive/phd101212s.gif
   :alt: Why use a version control system?
   :align: center
   :width: 400

Image from http://phdcomics.com/comics/archive_print.php?comicid=1531


----

Git version control
...................

Git is the current (2017) standard, it has replaced RCS, CVS, SVN, Bazaar and Hg.
If you have heard of any of them, the concepts in Git are similar while offering a lot of flexibility.


The usual workflow when working with Git is the following:

1. initiate a project using *init* or *clone* to copy another (remote) project.
2. *add* files to the list of tracked files
3. *commit* the files, locally
4. *push* your changes to a remote repository

The cycle 2-3-4 is the normal development cycle for a local project.

Any git repository contains all the history of the project, i.e all
commits with authors, data time, file changed, and the chain of commits called *branch*

----

Interact with another repository
................................

To interact with a remote project, especially retrieve commits from a remote
project one uses:

#. *remote add name url* to define the remote project
#. *fetch* to retrieve the changes made on a remote repository
#. *merge* to merge changes from a remote branch into the current branch

The cycle 2-3 is the normal cycle for a remote project.

----

More on git
...........

* *status* show the working tree status (branch name, file modified, added...)
* *log* show commits logs
* *diff* show changes between commits
* *cherry-pick* apply the changes introduced by some existing commits

Tutorial on Git:
................

* `Comprehensive tutorial <http://gitref.org>`_
* `Cheat sheet from Github <https://services.github.com/on-demand/downloads/github-git-cheat-sheet.pdf>`_
* `simple Cheat sheet <http://rogerdudler.github.io/git-guide/files/git_cheat_sheet.pdf>`_

----

GitHub
......

The web service github.com provides free git-hosting for open-source project and
encourages collaboration using forks of projects.
The main advantages of GitHub are:

 - `Highest visibility compared to other hosting (in 2017) <http://software.ac.uk/resources/guides/choosing-repository-your-software-project>`_
 - `Offer a fixed pipeline based on *Pull request* <https://help.github.com/articles/using-pull-requests/>`_
 - `Many tutorials on GitHub <https://guides.github.com/>`_
 - Issue tracker
 - Web page hosting for projects
 - Download of releases

Github is actually a social network, but unlike Linked'in or Facebook it
focuses on code developers. Activities on Github are monitored by head-hunters
and can be useful for professional placement.


----

Alternatives
------------

The alternative to github for ESRF projects is
`GitLab <https://gitlab.esrf.fr>`_ which offers similar feature to GitHub.

You can select a privacy level for your projects.

.. image:: images/gitlab_privacy.png
    :align: center

Public projects can be seen from outside: https://gitlab.esrf.fr/public

----

Different types of workflow
...........................

They are different workflow with git:

* `Centralized Workflow <https://www.atlassian.com/git/tutorials/comparing-workflows#centralized-workflow>`_
* `Git Flow <https://www.atlassian.com/git/tutorials/comparing-workflows#gitflow-workflow>`_
* `GitHub Flow <http://scottchacon.com/2011/08/31/github-flow.html>`_

github facilitates a forking workflow.

----

Forking workflow
................

.. image:: images/github-workflow.png
   :align: center

----

Contribution in OSS
...................

If your project becomes popular, you may have external contributors...
or you might want to contribute to other projects.

How to contribute to an Open Source project is presented in
`this document <http://scikit-image.org/docs/stable/contribute.html>`_
for scikit-image.

----

Take home message
-----------------

#. Keep your code tidy so that you can still understand it in 6 month
#. Define a license so that it can be re-used.
#. Stick to the PEP8 so that it looks *Pythonic*
#. Use a VCS: GitHub made *git* useable for human beings.

