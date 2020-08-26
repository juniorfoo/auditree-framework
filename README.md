[![OS Compatibility][platform-badge]](#prerequisites)
[![Python Compatibility][python-badge]][python]
[![pre-commit][pre-commit-badge]][pre-commit]
[![Code validation](https://github.com/ComplianceAsCode/auditree-framework/workflows/format%20%7C%20lint%20%7C%20test/badge.svg)][lint-test]
[![Upload Python Package](https://github.com/ComplianceAsCode/auditree-framework/workflows/PyPI%20upload/badge.svg)][pypi-upload]

# auditree-framework

Tool to run compliance control checks as unit tests and build up a body of evidence.

This framework gives you the tools you need to create an auditable body of evidence, and is designed to be "DevSecOps" friendly. Collection & validation of evidence is modelled as python unit tests, evidence is stored & versioned in a git repository, notifications can be configured to send to Slack, create issues, contact PagerDuty, or just write files into git. The goal is to enable the digital transformation of compliance activities, and make these everyday operational tasks for the team managing the system.

## Installation

### Prerequisites

- Supported for execution on OSX and LINUX.
- Supported for execution with Python 3.6 and above.

If you haven't already you need to generate a new ssh key for your Github account as per [this guide](https://help.github.com/articles/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent/)

### Check out the code

```shell
git clone git@github.com:ComplianceAsCode/auditree-framework
cd auditree-framework
```

### For users

```shell
python3 -m venv venv
. venv/bin/activate
make install
```

### For developers

```shell
python3 -m venv venv
. venv/bin/activate
make develop
```

#### Code style and formatting

This repository uses [yapf][yapf] for code formatting and [flake8][flake8] for code styling.  It also
uses [pre-commit][pre-commit] hooks that are integrated into the development process and the CI.  When
you run `make develop` you are ensuring that the pre-commit hooks are installed and updated to their
latest versions for this repository.  This ensures that all delivered code has been properly formatted
and passes the linter rules.  See the [pre-commit configuration file][pre-commit-config] for details on
`yapf` and `flake8` configurations.

Since `yapf` and `flake8` are installed as part of the `pre-commit` hooks, running `yapf` and `flake8`
manually must be done through `pre-commit`.  See examples below:

```shell
make code-format
make code-lint
```

...will run `yapf` and `flake8` on the entire repo and is equivalent to:

```shell
pre-commit run yapf --all-files
pre-commit run flake8 --all-files
```

...and when looking to limit execution to a subset of files do similar to:

```shell
pre-commit run yapf --files compliance/*
pre-commit run flake8 --files compliance/*
```

#### Unit tests

To run the frameworks test suite, use:

```shell
make test
```

#### Build Documentation

Documentation sources live in `doc-source`, and are also auto-generated from the source codes doc strings. The auto-generated documentation (`compliance*rst, modules.rst`) is ignored by git & should not be modified directly - make changes in the python code.

To build the documentation locally run:

```shell
make docs
```

This will update the files in `doc` with the latest documentation. These files should not be modified by hand.

## Try it

First, create an empty [credentials file][]:

```shell
touch ~/.credentials
```

Go to the demo checks and install required dependencies:

```shell
cd doc/demo-checks
pip install -r requirements.txt
```

Run the fetchers:

```shell
compliance --fetch -v --evidence=local -C setup.json
```

And then run the checks of the demo accreditations:

```shell
compliance --check demo.accreditation1,demo.accreditation2 --evidence=local -v -C setup.json
```

See a more detailed [quick start guide][].

## Contribute

Help us to improve the Auditree framework. See [CONTRIBUTING][].

## Ecosystem

We are building a set of common fetchers/checks in [Arboretum](https://github.com/ComplianceAsCode/auditree-arboretum). If you have a library of checks, please let us know & we'll link here.

We have a data gathering and reporting tool called [Harvest](https://github.com/ComplianceAsCode/auditree-harvest) which lets you process your evidence locker and generate reports over the data held.

We have a tool called [Prune](https://github.com/ComplianceAsCode/auditree-prune) which lets you mark evidence as no longer being collected, in a suitably tracked manner.

We have a tool called [Plant](https://github.com/ComplianceAsCode/auditree-plant) which lets you add evidence to evidence lockers without the use of fetchers or checks.

[CONTRIBUTING]: https://github.com/ComplianceAsCode/auditree-framework/blob/master/CONTRIBUTING.md
[credentials file]: https://github.com/ComplianceAsCode/auditree-framework/blob/master/doc/design-principles.rst#credentials
[flake8]: https://gitlab.com/pycqa/flake8
[platform-badge]: https://img.shields.io/badge/platform-osx%20|%20linux-orange.svg
[pre-commit-badge]: https://img.shields.io/badge/pre--commit-enabled-brightgreen?logo=pre-commit&logoColor=white
[pre-commit]: https://github.com/pre-commit/pre-commit
[pre-commit-config]: https://github.com/ComplianceAsCode/auditree-framework/blob/master/.pre-commit-config.yaml
[python-badge]: https://img.shields.io/badge/python-v3.6+-blue.svg
[python]: https://www.python.org/downloads/
[quick start guide]: https://github.com/ComplianceAsCode/auditree-framework/blob/master/doc-source/quick-start.rst
[yapf]: https://github.com/google/yapf
[lint-test]: https://github.com/ComplianceAsCode/auditree-framework/actions?query=workflow%3A%22format+%7C+lint+%7C+test%22
[pypi-upload]: https://github.com/ComplianceAsCode/auditree-framework/actions?query=workflow%3A%22PyPI+upload%22