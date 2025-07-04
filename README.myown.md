# CPython Codebase Structure

This document provides an overview of the CPython codebase, explaining the purpose of its main directories and key files. CPython is the reference implementation of the Python programming language.

## Top-Level Directory Overview

The CPython repository is organized into several top-level directories. Here's a summary of their roles:

*   **`.azure-pipelines/`**: Contains configuration files for Azure Pipelines, Microsoft's CI/CD service. This is used for automated testing and builds on various platforms.
*   **`.devcontainer/`**: Holds configuration for development containers, allowing for a consistent development environment using tools like VS Code Remote - Containers.
*   **`.github/`**: Contains GitHub-specific files, including:
    *   `CODEOWNERS`: Defines individuals or teams responsible for code in different parts of the repository.
    *   `CONTRIBUTING.rst`: Guidelines for contributing to CPython.
    *   `ISSUE_TEMPLATE/`: Templates for bug reports, feature requests, etc.
    *   `PULL_REQUEST_TEMPLATE.md`: Template for pull requests.
    *   `workflows/`: Defines GitHub Actions workflows for CI/CD, linting, and other automated tasks.
*   **`Android/`**: Contains build scripts and related files for compiling CPython for the Android platform.
*   **`Doc/`**: Houses the source files for Python's official documentation. This is written in reStructuredText and built using Sphinx.
*   **`Grammar/`**: Contains the grammar files (`.gram`) that define the Python language syntax. These are used by the parser generator.
*   **`Include/`**: Contains public C header files (`.h`) for the Python interpreter. These are necessary for developers writing C extensions or embedding Python.
*   **`InternalDocs/`**: Contains internal documentation for CPython developers, covering aspects like the compiler, garbage collector, and interpreter internals.
*   **`Lib/`**: This is the Python standard library, containing Python modules that provide a wide range of functionalities.
*   **`Mac/`**: Contains files specific to building and packaging CPython for macOS, including build scripts and resources for creating installers.
*   **`Misc/`**: A collection of miscellaneous files, including:
    *   `ACKS`: Acknowledgments of contributors.
    *   `HISTORY`: A detailed changelog (older, now superseded by `NEWS.d`).
    *   `NEWS.d/`: Directory containing news snippets for changes in each version, used to generate the `NEWS` file.
    *   `README*`: Various README files for specific platforms or configurations.
*   **`Modules/`**: Contains the C source code for extension modules that are part of the standard library but implemented in C for performance or to access C-level APIs (e.g., `_socket.c`, `_json.c`).
*   **`Objects/`**: Contains the C source code defining Python's built-in object types (e.g., integers, lists, dictionaries). This is where the core data structures of Python are implemented.
*   **`PC/`**: Contains files for building CPython on Windows (historically "PC" referred to IBM PC compatibles). This includes project files for Visual Studio and other Windows-specific components.
*   **`PCbuild/`**: Contains the MSBuild project files (`.vcxproj`) used for compiling CPython on Windows with Visual Studio.
*   **`Parser/`**: Contains the source code for Python's parser, which takes Python source code and turns it into an Abstract Syntax Tree (AST). This includes the lexer and the PEG (Parsing Expression Grammar) based parser generator.
*   **`Programs/`**: Contains the source code for the main Python executable (`python.c`) and other small programs like `_freeze_module.c` (used for freezing modules into executables).
*   **`Python/`**: This is the heart of the CPython interpreter. It contains the source code for:
    *   The compiler (translating AST to bytecode).
    *   The evaluation loop (executing bytecode).
    *   Built-in functions and modules.
    *   Core runtime services like import mechanisms, garbage collection, and thread management.
*   **`Tools/`**: A collection of tools and scripts useful for Python development and maintenance. This includes:
    *   Build scripts.
    *   Test utilities.
    *   Code generation scripts (e.g., for opcodes, Unicode data).
    *   Scripts for internationalization (i18n).
*   **`iOS/`**: Contains build scripts and related files for compiling CPython for iOS platforms.

## Detailed Directory Descriptions

Here's a more in-depth look at some of the key directories:

### `Doc/`

This directory contains the source for Python's official documentation.

*   **`c-api/`**: Documentation for the Python/C API, which allows C/C++ developers to write extension modules or embed Python.
*   **`distributing/`**: Information on how to distribute Python modules.
*   **`extending/`**: Guides on extending Python with C/C++ modules and embedding Python in other applications.
*   **`faq/`**: Frequently Asked Questions about Python.
*   **`howto/`**: In-depth guides on specific topics (e.g., logging, Unicode, argument parsing).
*   **`library/`**: Reference documentation for the Python standard library modules. This is one of the most frequently consulted parts of the documentation.
*   **`reference/`**: The Python language reference, detailing syntax, data models, and execution models.
*   **`tutorial/`**: The official Python tutorial, a great starting point for learning the language.
*   **`using/`**: Information on using Python on different platforms and configuring the interpreter.
*   **`whatsnew/`**: Highlights new features, improvements, and changes in each Python release.
*   **`tools/`**: Scripts and extensions used to build the documentation (e.g., Sphinx extensions).
*   `Makefile`, `make.bat`: Build scripts for generating the documentation.
*   `conf.py`: The Sphinx configuration file for building the documentation.

### `Include/`

This directory provides the header files for compiling CPython and developing C extensions.

*   **`Python.h`**: The main header file that should be included by most C extension modules. It pulls in many other necessary headers.
*   **`cpython/`**: Contains CPython-specific internal header files. These are not part of the stable ABI/API and should generally not be used directly by external extensions aiming for broad compatibility.
*   **`internal/`**: Contains even more internal header files, critical for the CPython runtime itself but highly unstable and not for public use.
*   Other files like `abstract.h`, `listobject.h`, `dictobject.h`, etc., define the C structures and functions for specific Python object types and core functionalities.

### `Lib/`

This is where the pure-Python modules of the standard library reside. It's a vast collection of modules. Some notable subdirectories and files:

*   **`asyncio/`**: Implementation of asynchronous I/O, coroutines, and event loops.
*   **`collections/`**: Provides specialized container datatypes (e.g., `deque`, `Counter`, `OrderedDict`).
*   **`concurrent/`**: Frameworks for concurrent execution, including:
    *   **`futures/`**: Asynchronous execution with `ThreadPoolExecutor` and `ProcessPoolExecutor`.
*   **`ctypes/`**: A foreign function library for Python, allowing calls to functions in DLLs/shared libraries.
*   **`distutils/`**: The original package for building and distributing Python modules (largely superseded by `setuptools` and `packaging` but still present).
*   **`email/`**: Library for managing and parsing email messages.
*   **`encodings/`**: Contains codecs for various text encodings.
*   **`ensurepip/`**: Infrastructure for bootstrapping `pip` into a Python installation.
*   **`html/`**: HTML parsing utilities (`html.parser`).
*   **`http/`**: HTTP client (`http.client`) and server (`http.server`) implementations.
*   **`importlib/`**: Implementation of Python's import mechanism.
*   **`json/`**: JSON encoder and decoder.
*   **`logging/`**: The logging facility for Python.
*   **`multiprocessing/`**: Process-based parallelism.
*   **`pydoc_data/`**: Data files used by `pydoc`.
*   **`sqlite3/`**: Python interface to SQLite.
*   **`test/`**: The regression test suite for the standard library. This is a very important directory, containing thousands of tests.
    *   `test_*.py`: Individual test files for modules.
    *   `libregrtest/`: The test execution framework.
*   **`tkinter/`**: Interface to the Tk GUI toolkit.
*   **`unittest/`**: The unit testing framework.
*   **`urllib/`**: Modules for working with URLs (e.g., `urllib.request`, `urllib.parse`).
*   **`venv/`**: Tools for creating virtual environments.
*   **`wsgiref/`**: WSGI (Web Server Gateway Interface) utilities.
*   **`xml/`**: XML processing modules (e.g., `xml.etree.ElementTree`, `xml.dom`).
*   **`zipfile.py`**: Module for working with ZIP archives.

### `Modules/`

This directory contains C source code for built-in modules and extension modules that are part of the standard library but require C for performance, system calls, or wrapping C libraries.

*   **`_abc.c`**: C implementation details for the `abc` module.
*   **`_asyncio.c`**: C helpers for the `asyncio` module.
*   **`_bz2module.c`**: Interface to the bzip2 compression library.
*   **`_ctypes/`**: C source code for the `ctypes` foreign function library.
*   **`_decimal/`**: C implementation of the `decimal` module for fixed and floating-point decimal arithmetic.
*   **`_elementtree.c`**: C accelerator for `xml.etree.ElementTree`.
*   **`_hashopenssl.c`**: Wraps OpenSSL's hashing algorithms for `hashlib`.
*   **`_io/`**: C implementation of the I/O system (`io` module).
*   **`_json.c`**: C accelerator for the `json` module.
*   **`_lzmamodule.c`**: Interface to the LZMA compression library (for `.xz` files).
*   **`_multiprocessing/`**: C components for the `multiprocessing` module.
*   **`_sqlite/`**: C source for the `sqlite3` module.
*   **`_ssl.c`**: C interface to OpenSSL for SSL/TLS support (`ssl` module).
*   **`zlibmodule.c`**: Interface to the zlib compression library.
*   `Setup`, `Setup.bootstrap.in`, `Setup.stdlib.in`: Files used during the build process to determine which modules to compile, especially on Unix-like systems.

### `Objects/`

This directory contains the C source code that defines Python's fundamental built-in object types.

*   **`abstract.c`**: Implements the abstract object protocol (e.g., functions like `PyObject_GetItem`, `PyNumber_Add`).
*   **`boolobject.c`**: Implementation of the boolean type (`True`, `False`).
*   **`bytearrayobject.c`**: Implementation of the `bytearray` type.
*   **`bytesobject.c`**: Implementation of the `bytes` type.
*   **`call.c`**: Logic for calling Python objects.
*   **`classobject.c`**: Older style class implementation (largely historical, modern classes are in `typeobject.c`).
*   **`complexobject.c`**: Implementation of complex numbers.
*   **`dictobject.c`**: Implementation of dictionaries (hash maps).
*   **`enumobject.c`**: Support for enumeration types.
*   **`exceptions.c`**: Implementation of built-in exceptions and exception handling machinery.
*   **`fileobject.c`**: Older file object implementation (modern I/O is in `Modules/_io/`).
*   **`floatobject.c`**: Implementation of floating-point numbers.
*   **`frameobject.c`**: Implementation of frame objects, which represent execution frames.
*   **`funcobject.c`**: Implementation of function objects.
*   **`genericaliasobject.c`**: Implementation of PEP 585 generic aliases (e.g., `list[int]`).
*   **`genobject.c`**: Implementation of generator objects.
*   **`iterobject.c`**: Implementation of iterator objects.
*   **`listobject.c`**: Implementation of lists.
*   **`longobject.c`**: Implementation of arbitrary-precision integers.
*   **`memoryobject.c`**: Implementation of `memoryview` objects.
*   **`methodobject.c`**: Implementation of method objects.
*   **`moduleobject.c`**: Implementation of module objects.
*   **`object.c`**: Core object allocation and type machinery (`PyObject`, `PyTypeObject`). This is fundamental.
*   **`obmalloc.c`**: Python's specialized object memory allocator (pymalloc).
*   **`setobject.c`**: Implementation of set and frozenset types.
*   **`sliceobject.c`**: Implementation of slice objects.
*   **`structseq.c`**: Utilities for creating sequence types similar to `namedtuple`.
*   **`tupleobject.c`**: Implementation of tuples.
*   **`typeobject.c`**: Implementation of type objects and the type system (metaclasses, inheritance, etc.). This is a cornerstone of Python's object model.
*   **`unicodeobject.c`**: Implementation of Unicode string objects (`str`).

### `Parser/`

This directory is responsible for turning Python source code into a usable internal representation.

*   **`Python.asdl`**: Defines the Abstract Syntax Tree (AST) nodes using the ASDL (Abstract Syntax Definition Language).
*   **`asdl.py`, `asdl_c.py`**: Scripts to process ASDL files and generate C code or Python classes for AST nodes.
*   **`lexer/`**: Contains the C code for the lexer (tokenizer), which breaks down the source code into a stream of tokens.
*   **`pegen.c`, `pegen.h`**: Core components of the PEG (Parsing Expression Grammar) based parser generator.
*   **`parser.c`**: The main parser logic that uses the generated tables from `pegen` to build an AST.
*   **`tokenizer/`**: The actual C code for the tokenizer (lexer), which is distinct from the `lexer/` directory that seems to contain more abstract lexer state.

### `Python/`

This directory contains the core interpreter logic, including the compiler, the bytecode evaluator, and many built-in functionalities.

*   **`Python-ast.c`**: Generated C code for working with AST nodes (from `Parser/Python.asdl`).
*   **`Python-tokenize.c`**: C interface to the tokenizer.
*   **`_warnings.c`**: Implementation of the `warnings` module.
*   **`ast.c`**: Functions for manipulating and validating ASTs.
*   **`bltinmodule.c`**: Implementation of the `builtins` module (e.g., `len()`, `print()`, `Exception`).
*   **`ceval.c`**: The **C**ode **Eval**uation loop. This is the heart of the interpreter, responsible for executing Python bytecode.
*   **`ceval_gil.c`**: GIL (Global Interpreter Lock) management code for the default CPython build.
*   **`compile.c`**: The Python bytecode compiler, which translates ASTs into sequences of bytecode instructions.
*   **`context.c`**: Implementation of context variables (`contextvars` module).
*   **`errors.c`**: Error reporting and exception handling utilities.
*   **`fileutils.c`**: Low-level file and path utilities.
*   **`frozen.c`**: Support for frozen modules (modules compiled into the interpreter).
*   **`future.c`**: Handling of `from __future__ import ...` statements.
*   **`gc.c`**: The garbage collector implementation (handles cyclic garbage).
*   **`import.c`**: Implementation of the import mechanism.
*   **`importdl.c`**: Dynamic loading of extension modules on systems that use `dlopen`.
*   **`marshal.c`**: Functions for serializing and de-serializing Python code objects and other data (`marshal` module).
*   **`moduleobject.c`**: (Also found in `Objects/`) Defines module type, but this might contain more runtime aspects.
*   **`mystrtoul.c`, `mystrtoff.c`**: String to number conversion utilities.
*   **`pathconfig.c`**: Logic for determining Python's path configuration (e.g., `sys.path`).
*   **`pyarena.c`**: An arena allocator used by the compiler.
*   **`pylifecycle.c`**: Python interpreter initialization and finalization.
*   **`pystate.c`**: Manages interpreter and thread state.
*   **`pythonrun.c`**: Higher-level functions for running Python code and interacting with the interpreter.
*   **`structmember.c`**: Utilities for defining members of C structures that are exposed to Python.
*   **`symtable.c`**: Symbol table generation (used by the compiler to understand scopes and variables).
*   **`sysmodule.c`**: Implementation of the `sys` module.
*   **`traceback.c`**: Functions for creating and manipulating traceback objects.
*   **`peephole.c`**: The peephole optimizer, which performs minor optimizations on the generated bytecode.

### `Tools/`

This directory contains various scripts and tools for CPython development, building, and maintenance.

*   **`build/`**: Scripts related to the build process, code generation (e.g., `generate_opcode_h.py`, `generate_stdlib_module_names.py`), and checks.
*   **`c-analyzer/`**: Tools for static analysis of CPython's C code.
*   **`cases_generator/`**: Scripts for generating parts of the bytecode evaluation loop (`ceval.c`) and optimizer from a higher-level description. This is a key part of the new "specializing adaptive interpreter."
*   **`clinic/`**: Argument Clinic tool, used to auto-generate argument parsing code for C functions exposed to Python.
*   **`freeze/`**: Tools for freezing Python scripts into executables.
*   **`gdb/`**: GDB (GNU Debugger) extensions for inspecting Python processes.
*   **`i18n/`**: Tools for internationalization and localization (e.g., `pygettext.py`, `msgfmt.py`).
*   **`jit/`**: Experimental JIT (Just-In-Time) compiler components. (Note: CPython does not have a full JIT by default; this is likely for research or specific builds).
*   **`msi/`**: Scripts and configuration for creating Windows MSI installers.
*   **`peg_generator/`**: Tools related to the PEG parser generator used in `Parser/`.
*   **`scripts/`**: A collection of miscellaneous utility scripts (e.g., `pydoc3`, `idle3`).
*   **`ssl/`**: Scripts for generating SSL data used by the `ssl` module.
*   **`unicode/`**: Scripts for generating Unicode database tables used by Python's Unicode implementation.
*   **`wasm/`**: Tools and configurations for building CPython for WebAssembly (Wasm) targets.

## Key Root-Level Files

Beyond the directories, several files in the root of the CPython repository are crucial for its configuration, build process, and general information:

*   **`README.rst`**: The main README file for the CPython project, providing a general overview, build instructions, and links to further resources.
*   **`LICENSE`**: The official license for CPython (Python Software Foundation License Version 2).
*   **`configure`**: (Unix-like systems) An executable shell script generated by Autoconf (`configure.ac`). It checks system capabilities and configures the build parameters, producing a `Makefile`.
*   **`configure.ac`**: (Unix-like systems) The input file for Autoconf, containing macros and tests to generate the `configure` script.
*   **`Makefile.pre.in`**: (Unix-like systems) A template for the `Makefile` used to build CPython. The `configure` script processes this file to generate the final `Makefile`.
*   **`pyconfig.h.in`**: A template file that `configure` (on Unix) or manual configuration (on other platforms like Windows) uses to generate `pyconfig.h`. This header file contains many platform-specific definitions and macros that control how Python is compiled.
*   **`.gitattributes`**: Defines attributes for paths in the Git repository, such as line ending normalization.
*   **`.gitignore`**: Specifies intentionally untracked files that Git should ignore (e.g., build artifacts, editor temporary files).
*   **`.mailmap`**: Helps normalize author names and emails in Git history.
*   **`.pre-commit-config.yaml`**: Configuration for pre-commit hooks, used to run linters and formatters before code is committed.
*   **`setup.py`**: While less central than in typical Python packages (as CPython's build is more complex), this file is still used for some build operations, particularly for extension modules and for tasks like `python setup.py install`. It interacts with `distutils` or `setuptools`.
*   **`AGENTS.md`**: (If present) Provides instructions or tips specifically for AI agents working with the codebase.
*   **`SECURITY.md`**: Outlines the security policy and how to report vulnerabilities.
*   **`tox.ini`**: Configuration file for `tox`, a tool for automating testing in multiple environments (though GitHub Actions are more commonly used for CI now).
*   **`run_tests.py`**: (Often found in older versions or specific test setups) A script to run the Python test suite. The primary way to run tests now is usually `python -m test` or via `Makefile` targets.
