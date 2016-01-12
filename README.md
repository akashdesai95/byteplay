# byteplay

* Originally created by Noah Raph
* Original code archived and frozen at http://code.google.com/p/byteplay
* This Repository automatically exported from code.google.com/p/byteplay

## What it is

For a full explanation with code examples, see https://pypi.python.org/pypi/byteplay/0.2.

This summary is extracted from the above pypi page:

byteplay is a module which lets you easily play with Python bytecode.
I (Noah Raph) wrote it because I needed to manipulate Python bytecode...

The basic idea is simple: define a new type, named Code,
which is equivalent to Python code objects,
but, unlike Python code objects, is easy to play with.
“Equivalent” means that every Python code object can be converted to a
Code object and vice-versa
without losing any important information on the way.

If you are interested in changing the behaviour of functions,
or in assembling functions on your own, you may find byteplay useful.
You may also find it useful if you are interested in how Python’s bytecode actually works;
byteplay lets you easily play with existing bytecode and see what happens.

## More info...

If you want to know more about Python code objects and bytecode,
the following blog series and video lectures are good orientations
to CPython internals:

* Ryan Kelly's short talk "Bytecode: What, Why, and How to Hack it",
  https://www.youtube.com/watch?v=ve7lLHtJ9l8, contains a demonstration
  of using BytePlay!

* Philip Guo's lecture series on Python internals takes you into every 
  important module of the CPython source:
  https://www.youtube.com/playlist?list=PLzV58Zm8FuBL6OAv1Yu6AwXZrnsFbbR0S
  Unfortunately that series is based on Python 2.7.

* Much the same ground is covered for Python 3.2 and in a very condensed
  way by Larry Hastings' "Architectural Tour" talk: 
  https://www.youtube.com/watch?v=XGF3Qu4dUqk

* Yanin Akniv's tour of bytecode execution and other topics:
  http://tech.blog.aknin.name/2010/04/02/pythons-innards-introduction/
  is well worth reading especially on the contents of a code object.

* Eli Benderski's notes on internals:
  http://eli.thegreenplace.net/tag/python-internals

* Brett Cannon's talk on how CPython compiles source to bytecode:
  https://www.youtube.com/watch?v=R31NRWgoIWM

* In the CPython source distro, see the files Doc/library/dis.rst and
  Doc/library/inspect.rst, then read the dis.py and inspect.py modules 
  themselves.

* The Byterun project (https://github.com/nedbat/byterun) is a Python
  bytecode executor written in Python.

See also the Bytecode Assembler and the ASTRoid modules on pypi,
but neither is well-documented and they aren't updated to Python 3.

## Why this fork?

I (tallforasmurf) would like to play with byteplay on Python 3,
which the original does not support.
I've made this fork (by export from code.google.com)
to investigate the possibility of converting it to Python 3.

The file byteplay3.py is my edited version for Python 3.
**At this time byteplay3 is a work in progress**.

The file byteplay.py is the original code by Noah.
It supports Python 2.7 and before.
It is probably identical to the code available on pypi (linked above)
but you should not depend on that.
Get the original when working with Python 2.x.

TODO: When/if byteplay works with Python3,
Ryan Kelly's Promise package (https://github.com/rfk/promise/)
which is based on byteplay,
could also be brought to Python 3, and possibly extended.

## Changes from the original...

I (tallforasmurf) am making the following changes in the API of
byteplay3 as compared to the original.

1. Only Python 3.x supported.

2. Class `Opcode.\_\_repr\_\_()` has different output than `Opcode.\_\_str\_\_()`.
   Previously they were identical; now `__repr__()` returns a string that
   could be eval'd to reproduce the Opcode object (if "Opcode" is defined).

3. `CodeList.\_\_str\_\_()` result is now a list of strings.
   Originally it returned a single big string of the disassembled bytecode
   sequence; now it is a list of lines. The `printcodelist()` method works
   as before to print a disassembly to a file or stdout.

4. I have added `stack\_effect(Opcode, arg) ==> net\_stack\_change\_int`,
   from the opcode module, which is passed in `\_\_all\_\_`.
   This stack effect routine is in fact the CPython routine from compile.c.
   As such it is fast, and maintained as part of CPython.

5. The function `getse(Opcode, arg) ==> (pop\_count\_int,push\_count\_int)`
   from byteplay2 is changed. Formerly it used a bunch of code modified from the
   Bytecode Assembler. Now it returns a minimal result based on calling
   stack\_effect(). The returned tuple will at least sometimes not be the
   same as in byteplay2, although the net of push\_count-pop\_count will
   be correct.




