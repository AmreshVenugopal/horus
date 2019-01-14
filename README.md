# Fastest
Creates unit tests from examples in the docstring and more

[![Build_Status](https://travis-ci.org/AmreshVenugopal/fastest.svg?branch=master)](https://travis-ci.org/AmreshVenugopal/fastest)
[![Coverage Status](https://coveralls.io/repos/github/AmreshVenugopal/fastest/badge.svg?branch=master)](https://coveralls.io/github/AmreshVenugopal/fastest?branch=master)

### Install

```
$ pip install fastest
```

### Usage
```
$ python main.py --path=$(pwd) --source=<source>
```
where `path` is the the project root, and [`source`](https://coverage.readthedocs.io/en/coverage-4.3.4/source.html#source) 
is same as the value passed to the command `coverage run -m unittest --source=$source test`


### Introduction
Things that happen when you run `python main.py --path=$(pwd) --source=<source>` in your
python project:

1. Checks for a `test` file at the project root, it creates if it doesn't find one.
2. Watches `.py` files for changes.
3. Creates unittests if a function has examples in its docstrings like so:

```python
# .
# ├──module_a
# ├──module_b
#    └── utils.py
#
def add(x, y):
    """
    example: add(3, 4) -> 7 #
    """
    return x + y
```

This will create a unittest in the `test` directory, `assertEqual(add(3, 4), 7)`
within `Class test_<file>_<function>(self)` 
(for the given directory, tree: `Class test_utils_add(self)`)

4. Runs all tests that are created.
5. Creates a coverage report (in html format).
6. Print the link to the coverage reports' index.html.


### How to make best use of Fastest
1. Keep your `functions` light:
    - Be paranoid about separations of concern.
    - Too many conditions are a hint that you might need another function
    - Complex loops and if else are not scalable code, a single mistake would 
    take that tower down and feature additions would involve someone going through 
    that brain-teaser.
2. Use libraries but wrap them with your own functions. Like: Use `requests` or the inevitable database? 
    wrap them with your own functions anyway.
    - Helps with adding customizations in one place (configuring things like base url, and similar configs)
    - Helps mocking so that entire code-base can be unit tested.
3. Docstrings may get outdated if your work pace is faster, but adding examples now 
    would help you create tests which prevents your descriptions from going stale,
    either the tests fail and the description is outdated else everything is good.


### Fun facts
1. Fastest uses itself for its nearly automated tests and documentation.
2. Excluding the files that are to be changed infrequently, Fastest has 100% code coverage.
3. Fastest has two of its 32 test cases still failing, a testimony to itself.
