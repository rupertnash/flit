Flit command line interface
===========================

All operations use the ``flit`` command, followed by one of a number of
subcommands.

Common options
--------------

.. program:: flit

.. option:: -f <path>, --ini-file <path>

   Path to a config file specifying the module to build. The default is
   ``pyproject.toml`` or ``flit.ini``

.. option:: --repository <repository>

   Name of a repository to upload packages to. Should match a section in
   ``~/.pypirc``. The default is ``pypi``. See :doc:`upload`.

.. option::  --version

   Show the version of Flit in use.

.. option:: --help

   Show help on the command-line interface.

.. option:: --debug

   Show more detailed logs about what flit is doing.

.. _build_cmd:

``flit build``
--------------

.. program:: flit build

Build a wheel and an sdist (tarball) from the package.

.. option:: --format <format>

   Limit to building either ``wheel`` or ``sdist``.


``flit publish``
----------------

.. program:: flit publish

Build a wheel and an sdist (tarball) from the package, and upload them to PyPI
or another repository.

.. option:: --format <format>

   Limit to publishing either ``wheel`` or ``sdist``.
   You should normally publish the two formats together.

.. seealso:: :doc:`upload`

``flit install``
----------------

.. program:: flit install

Install the package on your system.

.. option:: -s, --symlink

   Symlink the module into site-packages rather than copying it, so that you
   can test changes without reinstalling the module.

.. option:: --pth-file

   Create a ``.pth`` file in site-packages rather than copying the module, so
   you can test changes without reinstalling. This is a less elegant alternative
   to ``--symlink``, but it works on Windows, which typically doesn't allow
   symlinks.

.. option:: --deps <dependency option>

   Which dependencies to install. One of ``all``, ``production``, ``develop``,
   or ``none``. ``all`` and ``develop`` install the extras ``test``, ``doc``,
   and ``dev``. Default ``all``.

.. option:: --extras <extra[,extra,...]>

   Which named extra features to install dependencies for. Specify ``all`` to
   install all optional dependencies, or a comma-separated list of extras.
   Default depends on ``--deps``.

.. option:: --user

   Do a user-local installation. This is the default if flit is not in a
   virtualenv or conda env (if the environment's library directory is
   read-only and ``site.ENABLE_USER_SITE`` is true).

.. option:: --env

   Install into the environment. This is the default in a virtualenv or conda
   env (if the environment's library directory is writable or
   ``site.ENABLE_USER_SITE`` is false).

.. option:: --python <path to python>

   Install for another Python, identified by the path of the python
   executable. The default is to install the module for the copy of Python
   that is running Flit. Using this option, you can install a module for Python
   2, for instance.

.. note::

   Flit calls pip to do the installation. You can set any of pip's options
   `using its environment variables
   <https://pip.pypa.io/en/stable/user_guide/#environment-variables>`__.

   When you use the :option:`--symlink` or :option:`--pth-file` options, pip
   is used to install dependencies. Otherwise, Flit builds a wheel and then
   calls pip to install that.


``flit init``
-------------

.. program:: flit init

Create a new ``pyproject.toml``  config file by prompting for information about
the module in the current directory.

Environment variables
---------------------

.. envvar:: FLIT_NO_NETWORK

   .. versionadded:: 0.10

   Setting this to any non-empty value will stop flit from making network
   connections (unless you explicitly ask to upload a package). This
   is intended for downstream packagers, so if you use this, it's up to you to
   ensure any necessary dependencies are installed.

.. envvar:: FLIT_ROOT_INSTALL

   By default, ``flit install`` will fail when run as root on POSIX systems,
   because installing Python modules systemwide is not recommended. Setting
   this to any non-empty value allows installation as root. It has no effect on
   Windows.

.. envvar:: FLIT_USERNAME
            FLIT_PASSWORD
            FLIT_INDEX_URL

   .. versionadded:: 0.11

   Set a username, password, and index URL for uploading packages.
   See :ref:`uploading packages with environment variables <upload_envvars>`
   for more information.

.. envvar:: FLIT_ALLOW_INVALID

   .. versionadded:: 0.13

   Setting this to any non-empty value tells Flit to continue if it detects
   invalid metadata, instead of failing with an error. Problems will still be
   reported in the logs, but won't cause Flit to stop.

   If the metadata is invalid, uploading the package to PyPI may fail. This
   environment variable provides an escape hatch in case Flit incorrectly
   rejects your valid metadata. If you need to use it and you believe your
   metadata is valid, please `open an issue <https://github.com/takluyver/flit/issues>`__.

.. envvar:: SOURCE_DATE_EPOCH

   To make reproducible builds, set this to a timestamp as a number of seconds
   since the start of the year 1970 in UTC, and document the value you used.
   On Unix systems, you can get a value for the current time by running::

       date +%s


   .. seealso::

      `The SOURCE_DATE_EPOCH specification
      <https://reproducible-builds.org/specs/source-date-epoch/>`__

