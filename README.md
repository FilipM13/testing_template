# FILES AND STRUCTURE DESCRIPTION

## For making package installable

### pyproject.toml

Tells how to set up project.

### setup.py

Contains instalation script for a package. Allows installation of package in editable mode.

!!! seen as security risk because script is executable

### setup.cfg

Stores metadata of a project.

`[metadata]` contains: <br>
- title
- description
- author
- license
- license file
- platforms (windows, linux etc)
- classifiers (i.e. programming language)

`[options]` contains: <br>
- packages (list of packages - names of src subfolders)
- install_requirements (requirements for packages, copy of requirements.txt)
- python_requires (boundry versions of python)
- package_dir (src)
- zip_safe

### requirements.txt

Standard python requirements file.

## Test configuration

### requirements_dev.txt

Contains only dependencies required for testing.

## setup.cfg - appending for test configuration

To configure tests append previously created file with:

`[options.extras_require]` contains: <br>
- testing (copy of requirements_dev.txt)

`[options.package_data]` contains information about typy hinting of package, for example: <br>
project_name = py.typed

To make typing work create blank file `py.typed` next to `__init__.py` file inside package.

`[flake8]` contains configuration of flake8 checks for example:
max-line-length = 160

## pyproject.toml - appending for test configuration

To configure tests append previously created file with:

`[tool.pytest.ini_options]`

`[tool.mypy]`

## Multiple enviroments with tox

### tox.ini

Allows creating new enviroments, installs package into these enviroments, runs all tests in fresh enviroment (i.e. pytest, flake8, mypy).

List of enviroments is stored in envlist field. "py36" and similar are predefined and you don't have to configure them. Configuration of these is in `[testenv]` section of the file. You can create new enviroments by adding `[testenv:my_env_name]` sections.

Fields in enviroments sections: <br>
- setenv
- deps
- commands - important! list of commands to be executed in enviroments
- basepython

## GITHUB ACTIONS

### catalog structure

To enable automation of tests and running jobs, there must be `.github` directory with `workflows` subdirectory containing workflowss in form of yaml files, for example `.github/workflows/tests.yaml`.

### yaml file

Sections of yaml file: <br>
- `name` - this will apear in badge indicating workflow status
- `on` - indicates when to run jobs
- `jobs` - lists all job, fields

Fields in jobs may be: `runs-on`,`strategy`,`steps`

### badge

Example of line to put in file to get badge: <br>
`![Tests](https://github.com/FilipM13/automated_testing/actions/workflows/tests.yml/badge.svg)`<br>
So in simplification:<br>
`![name_of_badge](link_to_project/actions/workflows/job_file.yaml/badge.svg)`
