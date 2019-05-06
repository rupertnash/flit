Release history
===============

Version 1.3
-----------

- Fix for building sdists from a subdirectory in a Mercurial repository
  (:ghpull:`233`).
- Fix for getting the docstring and version from modules defining their encoding
  (:ghpull:`239`).
- Fix for installing packages with ``flit installfrom`` (:ghpull:`221`).
- Packages with requirements no longer get a spurious ``Provides-Extra: .none``
  metadata entry (:ghissue:`228`).
- Better check of whether ``python-requires`` includes any Python 2 version
  (:ghpull:`232`).
- Better check of home page URLs in ``flit init`` (:ghpull:`230`).
- Better error message when the description file is not found (:ghpull:`234`).
- Updated a help message to refer to ``pyproject.toml`` (:ghpull:`240`).
- Improve tests of ``flit init`` (:ghpull:`229`).

Version 1.2.1
-------------

- Fix for installing packages with ``flit install``.
- Make ``requests_download`` an extra dependency, to avoid a circular build
  dependency. To use ``flit installfrom``, you can install with
  ``pip install flit[installfrom]``. Note that the ``installfrom`` subcommand
  is deprecated, as it will soon be possible to use pip to install Flit projects
  directly from a VCS URL.

Version 1.2
-----------

- Fixes for packages specifying ``requires-extra``: sdists should now work, and
  environment markers can be used together with ``requires-extra``.
- Fix running ``flit installfrom`` without a config file present in the
  working directory.
- The error message for a missing or empty docstring tells you what file
  the docstring should be in.
- Improvements to documentation on version selectors for requirements.

Version 1.1
-----------

- Packages can now have 'extras', specified as ``requires-extra`` in the
  :doc:`pyproject.toml file <pyproject_toml>`. These are additional dependencies
  for optional features.
- The ``home-page`` metadata field is no longer required.
- Additional project URLs are now validated.
- ``flit -V`` is now equivalent to ``flit --version``.
- Various improvements to documentation.

Version 1.0
-----------

- The description file may now be written in reStructuredText, Markdown or
  plain text. The file extension should indicate which of these formats it is
  (``.rst``, ``.md`` or ``.txt``). Previously, only reStructuredText was
  officially supported.
- Multiple links (e.g. documentation, bug tracker) can now be specified in a
  new :ref:`[tool.flit.metadata.urls] section <pyproject_toml_urls>` of
  ``pyproject.toml``.
- Dependencies are now correctly installed to the target Python when you use
  the ``--symlink`` or ``--pth-file`` options.
- Dependencies are only installed to the Python where Flit is running if
  it fails to get the docstring and version number without them.
- The commands deprecated in 0.13—``flit wheel``, ``flit sdist`` and
  ``flit register``—have been removed.

Although version 1.0 sounds like a milestone, there's nothing that makes this
release especially significant. It doesn't represent a step change in stability
or completeness. Flit has been gradually maturing for some time, and I chose
this point to end the series of 0.x version numbers.

Version 0.13
------------

- Better validation of several metadata fields (``dist-name``, ``requires``,
  ``requires-python``, ``home-page``), and of the version number.
- New :envvar:`FLIT_ALLOW_INVALID` environment variable to ignore validation
  failures in case they go wrong.
- The list of valid classifiers is now fetched from Warehouse (https://pypi.org),
  rather than the older https://pypi.python.org site.
- Deprecated ``flit wheel`` and ``flit sdist`` subcommands: use
  :ref:`build_cmd`.
- Deprecated ``flit register``: you can no longer register a package separately
  from uploading it.

Version 0.12.3
--------------

- Fix building and installing packages with a ``-`` in the distribution name.
- Fix numbering in README.

Version 0.12.2
--------------

- New tool to convert ``flit.ini`` to ``pyproject.toml``::

      python3 -m flit.tomlify

- Use the PAX tar format for sdists, as specified by PEP 517.

Version 0.12.1
--------------

- Restore dependency on ``zipfile36`` backport package.
- Add some missing options to documentation of ``flit install`` subcommand.
- Rearrange environment variables in the docs.

Version 0.12
------------

- Switch the config to ``pyproject.toml`` by default instead of ``flit.ini``,
  and implement the PEP 517 API.
- A new option ``--pth-file`` allows for development installation on Windows
  (where ``--symlink`` usually won't work).
- Normalise file permissions in the zip file, making builds more reproducible
  across different systems.
- Sdists (.tar.gz packages) can now also be reproducibly built by setting
  :envvar:`SOURCE_DATE_EPOCH`.
- For most modules, Flit can now extract the version number and docstring
  without importing it. It will still fall back to importing where getting
  these from the AST fails.
- ``flit build`` will build the wheel from the sdist, helping to ensure that
  files aren't left out of the sdist.
- All list fields in the INI file now ignore blank lines (``requires``,
  ``dev-requires``, ``classifiers``).
- Fix the path separator in the ``RECORD`` file of a wheel built on Windows.
- Some minor fixes to building reproducible wheels.
- If building a wheel fails, the temporary file created will be cleaned up.
- Various improvements to docs and README.

Version 0.11.4
--------------

- Explicitly open various files as UTF-8, rather than relying on locale
  encoding.
- Link to docs from README.
- Better test coverage, and a few minor fixes for problems revealed by tests.

Version 0.11.3
--------------

- Fixed a bug causing failed uploads when the password is entered in the
  terminal.

Version 0.11.2
--------------

- A couple of behaviour changes when uploading to warehouse.

Version 0.11.1
--------------

- Fixed a bug when you use flit to build an sdist from a subdirectory inside a
  VCS checkout. The VCS is now correctly detected.
- Fix the rst checker for newer versions of docutils, by upgrading the bundled
  copy of readme_renderer.

Version 0.11
------------

- Flit can now build sdists (tarballs) and upload them to PyPI, if your code is
  in a git or mercurial repository. There are new commands:

  - ``flit build`` builds both a wheel and an sdist.
  - ``flit publish`` builds and uploads a wheel and an sdist.

- Smarter ways of getting the information needed for upload:

  - If you have the `keyring <https://github.com/jaraco/keyring>`_ package
    installed, flit can use it to store your password, rather than keeping it
    in plain text in ``~/.pypirc``.
  - If ``~/.pypirc`` does not already exist, and you are prompted for your
    username, flit will write it into that file.
  - You can provide the information as environment variables:
    :envvar:`FLIT_USERNAME`, :envvar:`FLIT_PASSWORD` and :envvar:`FLIT_INDEX_URL`.
    Use this to upload packages from a CI service, for instance.

- Include 'LICENSE' or 'COPYING' files in wheels.
- Fix for ``flit install --symlink`` inside a virtualenv.


Version 0.10
------------

- Downstream packagers can use the :envvar:`FLIT_NO_NETWORK` environment
  variable to stop flit downloading data from the network.

Version 0.9
-----------

- ``flit install`` and ``flit installfrom`` now take an optional ``--python`` argument,
  with the path to the Python executable you want to install it for.
  Using this, you can install modules to Python 2.
- Installing a module normally (without ``--symlink``) builds a wheel and uses
  pip to install it, which should work better in some corner cases.

Version 0.8
-----------

- A new ``flit installfrom`` subcommand to install a project from a source
  archive, such as from Github.
- :doc:`Reproducible builds <reproducible>` - you can produce byte-for-byte
  identical wheels.
- A warning for non-canonical version numbers according to `PEP 440
  <https://www.python.org/dev/peps/pep-0440/>`__.
- Fix for installing projects on Windows.
- Better error message when module docstring is only whitespace.

Version 0.7
-----------

- A new ``dev-requires`` field in the config file for development requirements,
  used when doing ``flit install``.
- Added a ``--deps`` option for ``flit install`` to control which dependencies
  are installed.
- Flit can now be invoked with ``python -m flit``.

Version 0.6
-----------

- ``flit install`` now ensures requirements specified in ``flit.ini`` are
  installed, using pip.
- If you specify a description file, flit now warns you if it's not valid
  reStructuredText (since invalid reStructuredText is treated as plain text on
  PyPI).
- Improved the error message for mis-spelled keys in ``flit.ini``.

Version 0.5
-----------

- A new ``flit init`` command to quickly define the essential basic metadata
  for a package.
- Support for :doc:`entrypoints`.
- A new ``flit register`` command to register a package without uploading it,
  for when you want to claim a name before you're ready to release.
- Added a ``--repository`` option for specifying an alternative PyPI instance.
- Added a ``--debug`` flag to show debug-level log messages.
- Better error messages when the module docstring or ``__version__`` is missing.

Version 0.4
-----------

- Users can now specify ``dist-name`` in the config file if they need to use
  different names on PyPI and for imports.
- Classifiers are now checked against a locally cached list of valid
  classifiers.
- Packages can be locally installed into environments for development.
- Local installation now creates a PEP 376 ``.dist-info`` folder instead of
  ``.egg-info``.
