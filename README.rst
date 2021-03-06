=============
UnitTest mode
=============

Unittest mode is a minor mode enabling running python unit tests within
emacs. It is intended to be used alongside python-mode in emacs.


Installing
==========

The mode is distributed as a pack for emacs-live. To install it as an
emacs-live pack, add this to your ``.emacs-live.el`` file::

    (live-add-packs '("/path/to/unittest-pack"))


Alternatively, to install without emacs-live, put ``unittest.el`` on you
emacs load path and add the following to the init file::

    (require 'unittest)
    (add-hook 'python-mode-hook 'unittest-mode)


Usage
=====

The folling commands are available:

- ``C-x t r`` executes ``unittest-execute-current-file``

  - Executes the file for the current buffer with ``python -u <FILE_PATH>``

- ``C-x t m`` executes ``unittest-execute-current-module``

  - Executes the module for the current buffer with ``python -u -m <DOTTED_MODULE_NAME>``

  - The module name is determined by walking up the filesystem tree
    until a ``setup.py`` file is found.

  - The last module executed in this way is recorded in the ``custom``
    variable ``unittest-last-executed-module``

- ``C-x t l`` executes ``unittest-execute-last-module``

  - Executes the last module (stored in the ``custom``
    variable ``unittest-last-executed-module``)

- ``C-x t f`` executes ``unittest-run-test-case``

  - Executes the test file for the current buffer ``python -u <TEST_FILE_PATH>``

  - If the current file name starts with ``test_``, run that file, otherwise
    attempt to run a file name ``<DIRNAME>/tests/test_<FILENAME>``. If this
    file doesn't exist, it fails.

- ``C-x t t`` executes ``unittest-run-tests-in-directory``

  - Prompts for a directory in which to execute ``python -u -m unittest discover``

  - The default directory is the direcory of the first ``setup.py``
    found when walking up the filesystem tree.

- ``C-x t d`` executes ``unittest-run-tests-in-current-directory``

  - Executes ``python -u -m unittest discover`` in the direcory of the
    current buffer's file.


Configuring for use in Windows
==============================

To use this in Windows, you need to ``customize`` the the
``unittest-shell-exec`` variable to have the (exact) value of ``cmd /S
/C``.  This will make scripts and tests execute under a cmd.exe
subshell, and set up ``unittest.el`` to correctly quote paths with
space, and cmd.exe to correctly parse the quoting.


Changelog
=========

Version 0.3.0
-------------

 * Changed repository structure to that of an emacs-live pack


Version 0.2.0
-------------

 * Added ``customize`` options
   * unittest-run-tests-command
   * unittest-discover-tests-command
   * unittest-discover-module
   * unittest-run-tests-directory
 * Added inferior-python-mode to python-exec-mode


Version 0.1.2
-------------

 * Reverted to compilation-mode derived mode for executing modules


Version 0.1.1
-------------

 * Use comint-mode for python-exec
