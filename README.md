# Python Demo

Covered chapters 2, 7 and 8 from official Python Documentation.

## Using Python Interpreter

On mac and linux machines, the Python interpreter is usually installed in `/usr/local/bin`. Putting this path in Shell's search path makes it possible to start it by using

```bash
python3
```

Typing EOF (End of File) Character i.e. Ctrl + Dat the shell causes the interpreter to exit.
Another way to exit the interpter is to type `exit()`.

Just like CLI, the python interpreter also support interactive editing, history substitution (with UP and DOWN arrow key) and code completion (with TAB).

[comment]: # (Type a simple command like a + b and recall it using up and down arrow key. Type a simple function and using tab try to complete it's name for calling it.)

Another way to start the interpreter is as follows.

```bash
python3 -c command [arg]
```

Here command is executed like any other python code and the arguments provided can be accesssed using `sys` module.

For example:

```bash
python3 -c 'import sys; print("Hello, ", sys.argv[1])' Ritesh
```

After executing the command if we want to enter interactive mode also known as REPL (Read Evalution Print Loop), we can use the `-i` flag before the script.

### Interactive Mode

When commands are read from a terminal (tty - teletype), the interpreter is said to be in interactive mode In this mode it prompts for the next command with tht primary prompt (>>>) and constructs that take multiple lines, a secondary prompt (...)

```bash
python3
```

### Source encoding

By default, Python source files are treated as UTF-8. In this, the characters of most languages in the world can be used simultaneously in string literals.

But if your source code is in some different encoding then we must use a special comment to be the first line of the file. Syntax is as follows

```python
# -*- coding: <encoding_name> -*-
```

For example if the source file is encoded in cp1252 then the first line in the file should be the following comment.

```python
# -*- coding: cp1252 -*-
```

## Input and Output

There are several ways to present the ouput of a program.

### Fancier Output Formatting

### Reading and Writing Files

## Errors and Exceptions

### Syntax Errors

### Exceptions

### Handling Exceptions

### Raising Exceptions

### Exception Chaining

### User Defined Exceptions

### Defining Clean-up Actions

### Predefined Clean-up Actions
