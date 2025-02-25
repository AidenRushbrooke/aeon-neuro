# Installation

`aeon-neuro` currently supports Python versions 3.9, 3.10, 3.11 and 3.12. Prior to these
instructions, please ensure you have a compatible version of Python installed
(i.e. from https://www.python.org).

`aeon-neuro` is available for most well-known operating systems, and is frequently tested
on macOS, Ubuntu and Windows servers by our development CI.

When it comes to installing `aeon-neuro`, there are currently three primary options:
- [Install the latest release from PyPi.](#Install-the-latest-release-from-PyPi)
This is the recommended option for most users.
- [Install the latest release from conda-forge.](#Install-the-latest-release-from-conda-forge)
An alternative release installation using conda.
- [Install the latest development version from GitHub via pip.](#Install-the-latest-development-version-using-pip)
This will include the latest features and bug fixes, but can be more unstable than the
latest release.
- Building the package from source. This is a requirement for users who wish to
develop the `aeon-neuro` codebase and for most other contributions to the project.

```{note}
    While we try to keep output similar between OS and Python version. We cannot
    guarantee the estimators will output the same results for macOS ARM processors.
```

## Optional Dependencies

All installation options include the core dependencies required to run the framework
components of `aeon-neuro`. Some estimators and functionality require optional dependencies.
Without these dependencies, you may find that you will be prompted to install an
additional package when trying to use certain functionality.

For each installation option, we provide a method to install only the core dependencies
and a method to install all dependencies (barring certain unstable ones). Installing
all dependencies can take a while to process the installation and introduce limitations
on the versioning of other packages, but will allow all `aeon-neuro` functionality to be used
without impediment.

## Install the latest release from PyPi

We recommend creating a [virtual environment](#Using-a-pip-venv) for your `aeon-neuro`
installation. This will ensure that the dependencies of `aeon-neuro` do not conflict with
other packages you may have installed.

`aeon-neuro` releases are available via [PyPI](https://pypi.org/project/aeon-neuro/). To install
the latest `aeon-neuro` release with core dependencies via `pip` type:

```{code-block} powershell
pip install -U aeon-neuro
```

To install `aeon-neuro` with all stable dependencies, install with the `all_extras`
modifier. This will also install core dependencies, so the above command is not
required.

```{code-block} powershell
pip install -U aeon-neuro[all_extras]
```

```{note}
    If this results in a "no matches found" error, it may be due to how your shell
    handles special characters. Try surrounding the dependency portion with quotes i.e.

    pip install -U aeon-neuro"[all_extras]"
```

```{warning}
    Some dependencies included in `all_extras` may have installation issues for macOS
    with ARM processors. More details can be found in the troubleshooting section below.
```

After installation, you can verify that `aeon-neuro` has been installed correctly by
running the following commands:

```{code-block} powershell
pip show aeon-neuro  # see information about the installation i.e. version and file location
pip freeze  # see all installed packages for the current environment
```

For more information on the dependencies of `aeon-neuro` and more dependencies groups (such
as only dependencies for deep learning, or a list less stable dependencies excluded
from `all_extras`), see the
[`pyproject.toml`](https://github.com/aeon-toolkit/aeon-neuro/blob/main/pyproject.toml)
configuration file.

## Install the latest release from conda-forge

`aeon-neuro` releases are also available via [conda-forge](https://anaconda.org/conda-forge/aeon-neuro).
Run the following to create a new environment for `aeon-neuro` and install the package:

```{code-block} powershell
conda create -n aeon-neuro-env -c conda-forge aeon-neuro
conda activate aeon-neuro-env
```

Post-installation you can verify that `aeon-neuro` has been installed correctly by running
the following:

```{code-block} powershell
conda list aeon-neuro  # see information about the installation i.e. version and file location
conda list  # see all installed packages for the current environment
```

Currently for `conda` installations, optional dependencies must be installed separately.

## Install the latest development version using pip

Like the above method, we recommend creating a [virtual environment](#Using-a-pip-venv)
for your `aeon-neuro` installation.

If you already have the latest `aeon-neuro` release or the `aeon-neuro` GitHub `main` branch
installed, you will have to uninstall it prior to following these instructions:

```{code-block} powershell
pip uninstall aeon-neuro
```

The latest developments and bugfixes for `aeon-neuro` are available on the [`aeon-neuro`
GitHub](https://github.com/aeon-toolkit/aeon-neuro) `main` branch. The `main` branch can be
installed directly from GitHub using `pip install`:

```{code-block} powershell
pip install -U git+https://github.com/aeon-toolkit/aeon-neuro.git@main
```

To install `aeon-neuro` from GitHub `main` branch with all stable dependencies, the following
command can be used.

```{code-block} powershell
pip install -U "aeon-neuro[all_extras] @ git+https://github.com/aeon-toolkit/aeon-neuro.git@main"
```

The same warnings and information regarding the MacOS ARM processor,
checking install versioning and `pyproject.toml` dependencies given in the previous
section apply here as well.

## Using a pip venv

In order to avoid potential conflicts with other packages, we strongly recommended
using a [virtual environment (venv)](https://packaging.python.org/en/latest/guides/installing-using-pip-and-virtual-environments/)
or a fresh conda environment for the above installation options.

You can create a virtual environment using the following commands. The virtual
environment name `aeon-neuro-venv` can be replaced with a name of your choosing.

Windows and macOS:
```{code-block} powershell
python -m venv aeon-neuro-venv
```
Linux:
```{code-block} powershell
python3 -m venv aeon-neuro-venv
```

This environment can then be activated using the following commands:

Windows:
```{code-block} powershell
aeon-neuro-venv\Scripts\activate
```
macOS and Linux:
```{code-block} powershell
source aeon-neuro-venv/bin/activate
```

Note that this will only activate the environment for the current terminal session.
If you wish to use the environment in a different terminal session, you will need to
activate it again.

## Troubleshooting

If the common errors below do not help, it may be worth checking out the [scikit-learn
troubleshooting section](https://scikit-learn.org/stable/install.html#troubleshooting)

### `ModuleNotFoundError`

The most frequent reason for `ModuleNotFoundError` is installing `aeon-neuro` with
minimum dependencies (i.e. just `pip install aeon-neuro`) and using an estimator which
interfaces a package that has not been installed in the environment. To resolve this,
install the missing package, or install `aeon-neuro` with maximum dependencies (see above)
or install the individual packages as prompted by the error.

### `ImportError`

Import errors are often caused by an improperly linked virtual environment. Make sure
that your environment is activated and linked to whatever IDE you are using. You can
find the instructions for doing so in VScode
[here](https://code.visualstudio.com/docs/python/environments). If you are using
Jupyter Notebooks, follow
[these instructions](https://janakiev.com/blog/jupyter-virtual-envs/) for adding your
virtual environment as a new kernel for your notebook.

### Installing `all_extras` on Mac with an ARM processor

If you are using a Mac with an ARM processor, you may encounter an error when installing
`aeon-neuro[all_extras]`. This is due to the fact that some libraries included in `all_extras`
are not compatible with ARM-based processors. If you encounter this issue, you can try
installing soft dependencies separately.

We would appreciate if you could report any issues you encounter with the `all_extras`
installation on ARM-based processors to the [aeon-neuro GitHub issues page](https://github.com/aeon-toolkit/aeon-neuro/issues).

Also, ARM-based processors can have issues when installing packages distributed as
source distributions instead of Python wheels. To avoid this issue when installing a
package, you can try using a prior version of the package that was distributed as a wheel.

### `no matches found` when installing `all_extras`

Some shells (i.e. the commonly used [Zsh](https://en.wikipedia.org/wiki/Z_shell)) use
square brackets as a special character. If you are using such a shell, you may
encounter an error when installing `aeon-neuro[all_extras]`. This can be resolved by
surrounding the dependency portion with quotes i.e.

```{code-block} powershell
pip install -U aeon-neuro"[all_extras]"
```
