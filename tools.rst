Tools
=====

This section describes how to install and use the tools you need to build the
guide.

Environment
-----------

Install pipenv:

.. code-block:: sh

   $ pip install --user pipenv

CD to the root of the git repo and create a venv for the tooling:

.. code-block:: sh

   how-to-kubernetes$ pipenv --python 3.5

Install project dependencies:

.. code-block:: sh

   how-to-kubernetes$ pipenv install --dev

Building
--------

Spawn the venv shell:

.. code-block:: sh

   how-to-kubernetes$ pipenv shell

Make the guide:

.. code-block:: sh

   how-to-kubernetes$ make html

The guide will be published in the *_build* directory. Use the following
command to launch the guide in your browser:

.. code-block:: sh

   how-to-kubernetes$ firefox _build/html/index.html
