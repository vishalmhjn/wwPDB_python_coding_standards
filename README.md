# wwPDB Python Code Development Best Practices

## Description

This document intends to document the coding standards and best practices that
should be employed when developing in Python for wwPDB projects.

In addition, there is a document describing some of the major differences in
Python 3 and the update process [here](docs/2to3.md).

Major foci of this document:

* [Using Git](#using-git)
* [Python Coding Standards](#python-coding-standards)
* [Unit Testing](#unit-testing)
* [Continuous Integration](#continuous-integration)

### Using Git

Using git provides many benefits over SVN. First and foremost, git is designed for
decentralized collaboration. This is a major benefit for teams of people in different
locations working together on a shared project. Other major benefits of git:

* Github website enables
  * Contributions from anyone in the open-source community via pull requests
  * Integrated bug tracking
  * Using free [continuous integration software](#continuous-integration)
* Lightweight branches
  * All new feature development should be done in branches
  
Most important things to keep in mind when developing using git:

* Create branches for all development
* Commit frequently
* Use descriptive commit messages
* Use pull requests to test code before merging to master repository. See 
more in [continuous integration](#continuous-integration) section.

More detailed best practices documents can be found [here](https://sethrobertson.github.io/GitBestPractices/)
and [here](https://www.git-tower.com/learn/git/ebook/en/command-line/appendix/best-practices).

### Python Coding Standards

Python code should be written following [PEP008](https://www.python.org/dev/peps/pep-0008/). A good IDE like
[PyCharm](https://www.jetbrains.com/pycharm/) will highlight issues automatically.

Most important:

* Use four spaces per indentation level - not tabs
* Use proper [casing for names](https://www.python.org/dev/peps/pep-0008/#prescriptive-naming-conventions)
* Be consistent in use of single or double quotes for string declarations
* Document classes, methods, and functions using appropriate [docstrings](https://www.python.org/dev/peps/pep-0257/)
* Keep lines to a reasonable length (79-100 characters per line - exact length TBD)
* A foolish consistency is the hobgoblin of little minds

If you don't use PyCharm, you can check your code for PEP0008 compliance using [pylint](https://www.pylint.org/).

Additional considerations:

Python 3.5 has built-in support for [optional typing](https://docs.python.org/3/library/typing.html).
Using type annotations is recommended for new code development.

#### Project folder layout

Each git repository should contain one logical unit of related code. This usually means one module
per repository. Within that repository, some or all of the following files should be present:

```
README.rst
LICENSE
setup.py
requirements.txt
docs/conf.py
docs/index.md
tests/test_modname.py
modname/__init__.py
modname/core.py
modname/helpers.py
```

or for simple modules, replace the modname folder with

```
modname.py
```

See more details on project layout [here](http://docs.python-guide.org/en/latest/writing/structure/) 
or at the [PEP0328](https://www.python.org/dev/peps/pep-0328/) page.


### Unit Testing


#### Overview

Unit testing provides some major benefits over ad-hoc testing:

* Enables you to discover bugs immediately
* Prevents regressions (when fixing a bug, always create a test for the case that triggered the bug)
* Improves code quality
* Facilitates changes and refactoring (you can be confident that you didn't break something during a refactor)

Furthermore, test-driven development (write tests that fail first, then write code until the tests stop failing)
has additional benefits. The primary one is that TDD guarantees that you write tests for all your code as opposed
to haphazardly inserting some tests later on, or even worse, writing tests for code that you don't fully understand.

Furthermore, the tests written during TDD serve as additional documentation of the project in that they
document the specification that the code is written to match.

#### Specifics

Testing in python is usually performed using the standard module `unittest`.

The basic idea is:

* Import unittest
* Create a class that subclasses the `TestCase` class of the unittest module
* In that class, define a series of methods that perform the tests against your code

See the example file [here](tests/test_fizzbuzz.py).

Run it from the root directory:

```bash
python3 tests/test_fizzbuzz.py
```

