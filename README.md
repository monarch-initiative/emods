# emods

| [Documentation](https://monarch-initiative.github.io/emods) |

Monarch and Linda Crrnic Center project on phenotype identification
**TODO: Add more detailed information about the project**

# Getting Started
To get started with development in the emods project first clone the repository and enter the new directory

```bash
git clone git@github.com:monarch-initiative/emods.git
cd emods
```

## Setup Python Environment and Install Poetry
To finish setting up the project first we'll need to set up a Python development environment. You can either use your system `poetry` or install it within a repository virtual environment.

### Use System Poetry
To use you're system `poetry`, install `poetry` if you haven't already.
```
pip install poetry
```

### Install Poetry in a Virtual Environment
To use poetry within a virtual environmen and install `poetry` to the environment use your system Python or install `pyenv` and select your python version with `pyenv local 3.13`. Then create a virtual environment and install poetry to it. You will also want to add `cruft` to the virtual environment to keep updated with this template.
```
pyenv 3.12
python -m venv .venv
. .venv/bin/activate
pip install poetry
pip install cruft
```

## Install Dependencies
Now that we have the basic repository set up and the background dependencies, we can set up the dependencies for the rest of the project. First, we'll use poetry to install project dependencies.
```
poetry install
```

### Add `poetry-dynamic-versioning` as a plugin
Our usage of poetry requires the dynamic versionining plugin.
```
poetry self add "poetry-dynamic-versioning[plugin]"
```
**Note**: If you are using a Linux system and the above doesn't work giving you the following error `Invalid PEP 440 version: ...`, you could alternatively run:
```
poetry add poetry-dynamic-versioning
```

## Set-up `pre-commit`
`pre-commit` runs hooks on every commit to automatically point out issues in code such as missing semicolons, trailing whitespace, and debug statements. For more information click [here](https://pre-commit.com).

```
poetry run pre-commit install
```
which will result in the message:
```
pre-commit installed at .git/hooks/pre-commit
```
This indicates that you have a successful `pre-commit` setup.

## Run `tox` to see if the setup works
```
poetry run tox
```

This should run all the bullets mentioned above under the `tox` configuration and ideally you should see the following at the end of the run:
```
  coverage-clean: OK (0.20=setup[0.05]+cmd[0.15] seconds)
  lint-fix: OK (0.40=setup[0.01]+cmd[0.30,0.09] seconds)
  codespell-write: OK (0.20=setup[0.02]+cmd[0.18] seconds)
  docstr-coverage: OK (0.29=setup[0.01]+cmd[0.28] seconds)
  py: OK (1.29=setup[0.01]+cmd[1.28] seconds)
  congratulations :) (2.55 seconds)
```

And as the last line says: `congratulations :)`!! Your project is ready to evolve!

> If you have an error running `tox` your python dependencies may be out of sync and you may be able to fix it by running `poetry lock` and then running `tox` again.

# Final test to see everything is wired properly

On the command line, type the `project_name`. In this example, `ABCD`:
```
poetry run emods run
```
Should return "Hello, World"

To run commands within the poetry environment either preface the command with `poetry run`, i.e. `poetry run /path-to/my-command --options` or open the poetry shell with `poetry shell`.

# Run Jupyter notebooks
To run the Jupyter notebooks in the `notebooks/` directory you will need to do so through poetry.
```
poetry run jupyter lab
```

# Requirements
- Python >= 3.12
- [Poetry](https://python-poetry.org/docs/#installation)
- [Cruft]

# Repository Structure
 - Github wokflows:
   - For code quality checks (`qc.yml`)
   - Documentation deployment (`deploy-docs.yml`)
   - PyPI deployment (`pypi-publish.yml`)
 - `docs` directory with `Sphinx` configuration files and an `index.rst`file.
 - `src` directory structure with the `project_name` directory within it.
   - Within the `project_name` directory, there are 2 python files:
     - `main_file.py`
     - `cli.py` for [`click`](https://click.palletsprojects.com) commands.
 - `tests` directory with a very basic test.
 - `poetry` compatible `pyproject.toml` file containing minimal package requirements.
 - `tox.ini` file containing configuration for:
   -  `coverage-clean`
   -  `lint`
   -  `codespell`
   -  `docstr-coverage`
   -  `pytest`
- `LICENSE` file based on the choice made during setup.
- `README.md` file containing `project_description` value entered during setup.

# Future updates to the project's boilerplate code

In order to be up-to-date with the template, first check if there is a mismatch between the project's boilerplate code and the template by running:
```
cruft check
```

This indicates if there is a difference between the current project's boilerplate code and the latest version of the project template. If the project is up-to-date with the template:
```
SUCCESS: Good work! Project's cruft is up to date and as clean as possible :).
```

Otherwise, it will indicate that the project's boilerplate code is not up-to-date by the following:
```
FAILURE: Project's cruft is out of date! Run `cruft update` to clean this mess up.
```

For viewing the difference, run `cruft diff`. This shows the difference between the project's boilerplate code and the template's latest version.

After running `cruft update`, the project's boilerplate code will be updated to the latest version of the template.

# Setting up PyPI release

For the first time, you'll need to just run the following commands:
```
poetry build
poetry publish -u YOUR_PYPI_USERNAME -p YOUR_PYPI_PASSWORD
```
This will release a 0.0.0 version of your project on PyPI.

## Automating this via Github Release
Use "[Trusted Publishers](https://docs.pypi.org/trusted-publishers/)" by PyPI

## Creating documentation
The documentation desired should be placed in the `docs` directory (markdown or reStructured format files).

Let's say the user has 2 more .rst files to add:
 - intro.rst
 - installation.rst

These two files should be placed in the docs directory and the `index.rst` file should be updated to read the following

```rst
Welcome to emods's documentation!
=========================================================

.. toctree::
   :maxdepth: 2
   :caption: Contents:

   intro
   installation

Indices and tables
==================

* :ref:`genindex`
* :ref:`modindex`
* :ref:`search`

```
This lets sphinx know to look for these rst files and generate equivalent HTML files.

Documentation is automatically built and deployed via the github workflow `deploy-docs.yml`.
When changes are added to the main branch, this workflow is triggered. For this to work, the user needs to
set-up the github repository of the project to enable documentation from a specific branch. In the `Settings` tab
of the repository, click the `Pages` section in the left bar. For the `Branch`, choose the `gh-pages` branch.

The full GitHub Pages documentation can be found [here](https://docs.github.com/en/pages/quickstart).

# Acknowledgements

This [cookiecutter](https://cookiecutter.readthedocs.io/en/stable/README.html) project was developed from the [monarch-project-template](https://github.com/monarch-initiative/monarch-project-template) template and will be kept up-to-date using [cruft](https://cruft.github.io/cruft/).
