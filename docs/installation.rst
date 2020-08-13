============
Installation
============

There are plans to release Saturn on pip. Until that happens, you will need to install things manually.

Currently, this project only works on Windows. Cross-platform support is planned.

Getting the dependencies
------------------------

Install llvmlite with pip::

    > pip install llvmlite

Install rply with pip::

    > pip install rply

To get the latest version of the language, clone the Github repository.

A ``main.sat`` is provided in the repository. The language design and standard library have not been finalized, so 
please keep this in mind when writing code. All of the packages currently available are included in the
repository.

A syntax-higlighting extension for Visual Studio Code is being worked on.

To compile, type this command::

    > python main.py --clean

Then run your program. That's all there is to it!