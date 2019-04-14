# byteplay

* Originally created by Noam Raph
* Original code archived and frozen at http://code.google.com/p/byteplay
* This Repository automatically exported from code.google.com/p/byteplay

## Stop! Changes!

As of Python 3.6, the format of bytecode has changed from 1-3 bytes, to all 16-bit words. 
Also, several new opcodes have been added.
(Documented: https://docs.python.org/3/whatsnew/3.6.html#cpython-bytecode-changes)

These changes pretty thoroughly invalidate most features of byteplay!
It could be fixed, no doubt, but I don't have the inclination to do it.
If you do, feel free to submit a pull request, or to clone this repo and do a new version.

In the meantime, all the following text and the rest of the files are of historical interest only!

## What it is

byteplay was a module that made it easy to tinker with the executable
bytecode of a Python function in Python 2.
The original code is still available from pypi
(https://pypi.python.org/pypi/byteplay/0.2) and is still functional with Python 2.7.

This is byteplay3 which brings that capability to Python 3.4+.

For a full explanation with code examples see the new "about" file at
https://github.com/tallforasmurf/byteplay/blob/master/about.md

**At this time byteplay3 is a work in progress**.

## Why Version 3.5.x?

I am setting the version number of byteplay3 to be the same as the
highest level of Python against which it has been tested,
plus a minor change number.
Thus the current `__version__` string is `"3.5.0"`,
first release tested on Python 3.5.

## Why this fork?

I (tallforasmurf) would like to play with byteplay on Python 3,
which the original does not support.
I've made this fork (by export from code.google.com)
to investigate the possibility of converting it to Python 3.

The file byteplay3.py is my edited version for Python 3.



