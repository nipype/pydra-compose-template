# Intent of this template

The intent of this repository is to help you get started with implementing new Pydra
compose, within the `pydra.compose.<yourworkerpackagename>` namespace.

# To use this template

1. Click on new repo.
1. Select this template from the repository template drop down list.
1. Give your repo a name.
1. Once the repo is created and cloned, search for CHANGEME (`grep -rn CHANGEME . `) and
   replace with appropriate name.
1. Rename the namespace package root directory to replace `CHANGEME` with the name of the package:
   * `pydra/compose/CHANGEME`
1. Add your new worker class to `pydra/compose/<package-name>/__init__.py`
1. You may want to initialize a [Sphinx] docs directory.
1. Review the workflow in `.github/workflows/pythonpackage.yml`. Testing editable installations
   is probably not useful unless you are reconfiguring namespace packages.
1. **Update this README after creating the new repository.**

[Sphinx]: https://www.sphinx-doc.org/en/master/usage/quickstart.html

# Features of this template

## Tag-based versioning

The [setuptools_scm](https://github.com/pypa/setuptools_scm) tool allows for versioning based
on the most recent git tag. The release process can thus be:

```Shell
git tag -a 1.0.0
python -m build
twine upload dist/*
```

Note that uploading to PyPI is done via [Continuous integration](#continuous-integration) when
a tag is pushed to the repository, so only the first step needs to be donne manually.

Note also that we assume tags will be version numbers and not be prefixed with `v` or some other
string. See `setuptools_scm` documentation for alternative configurations.

## Namespace packages

[Namespace packages] allow multiple packages to be installed in such a way that they can be
imported from a common namespace. In this case, the base namespace is `pydra.compose`, and each
worker package installs a new module, such as `pydra.compose.afni`.

To do correctly, worker packages **must not** interfere with files higher in the hierarchy.
This includes adding `__init__.py` files in either `pydra` or `pydra/compose`.

[Namespace packages]: https://www.python.org/dev/peps/pep-0420/

## Tests

This package comes with a default set of test modules, and we encourage users to use pytest.
Tests can be discovered and run using:

```
pytest --doctest-modules pydra/compose/*
```

## Continuous integration

This template uses [GitHub Actions](https://docs.github.com/en/actions/) to run tests. To simulate
several plausible development or installation environments, we test over all Python versions
supported by Pydra, and install Pydra and the current package in both standard and
[editable](https://pip.pypa.io/en/stable/reference/pip_install/#editable-installs) modes.

The combination of standard/editable is in particular designed to ensure that namespace packaging
does not break. We strongly recommend keeping these tests in place for this reason, as one
non-compliant package can potentially affect Pydra or other worker packages.

In addition to verifying installations do not break or conflict, pytest is run on the package,
including all tests found in `test/` directories and [doctests].

Finally, packages are built and uploaded as artifacts for inspection. When a tag is pushed,
the packages are uploaded to PyPI if a valid [API token](https://pypi.org/help/#apitoken) is placed
in the [repository secrets](https://docs.github.com/en/actions/reference/encrypted-secrets).

[doctests]: https://docs.python.org/3/library/doctest.html

# Contributing to this template

This template repository is periodically updated as we establish and best practices for worker
packages. We welcome contributions from the community to help set a solid baseline for all
worker packages.

# Sample post-setup README contents

## For developers

Install repo in developer mode from the source directory. It is also useful to
install pre-commit to take care of styling via [black](https://black.readthedocs.io/):

```
pip install -e .[dev]
pre-commit install
```
