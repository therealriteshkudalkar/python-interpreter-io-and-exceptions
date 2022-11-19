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

There are several ways to present the ouput of a program. There are two ways of writing values: expression statements and the print() function.

### Fancier Output Formatting

Often we want more control over the formatting of your output thatn simply printintg space-separated values. 

* Fomatted String literals being with `f` or `F` before the opening quotation mark.
  
```python
year = 2016
event = 'Referendum'
f'Results of the {year} {event}'
```

* Other way is to use str.format() method of strings. But it requires more manual effort.

```python
yes_votes = 42_534
no_votes = 43_132
percentage = yes_votes / (yes_votes + no_votes)
'{} YES VOTES  {}'.format(yes_votes, percentage)
```

* Finally, we can also use string slicing and concatenation operations to create any layout.

```python
name = 'Amol'
print("Hello, ", name)
```

Example on Formatted String Literals

```python
import math
print(f'The value of pi is approximately {math.pi:.3f}.')
```

Passing an integer after `:` will cause that field to be a minimum number of characters wide. This is useful for making columns line up.

```python
table = {'Sjored': 412, 'Jack': 4098, 'Dcab': 75, 'Jord': 3536}
for name, phone in table.items():
    print(f'{name:10} ===> {phone:10d}')
```

If you ever want to display the name of variable along with it's value, maybe while debugging. You can do so using `=` specifier.

```python
bugs = 'roaches'
count = 13
area = 'living room'
print(f'Debugging {bugs=} {count=} {area=}')
```

Examples on String format() method

```python
print('We are the {} who say "{}!"'.format('knights', 'Ni'))
```

The number in the brackets can be used to refer to the position of the object passed into the str.format() method.

```python
print('{0} and {1}'.format('spam', 'eggs'))
print('{1} and {0}'.formtat('spam', 'eggs'))
```

If keyword arguments are used in this method, then their values can be referred to by using the name of the argument.

```python
print('This {food} is {adjective}.'.format(food='spam', adjective='absolutely horrible'))
```

Positional and keyword arguments can be arbitrarily combined.

```python
print('The story of {0}, {1} and {other}.'.format('Bill', 'Manfred', other='George'))
```

We can access and print the items in a dictionary by specifying the keys in the `[]`.

```python
table = {'Sjored': 412, 'Jack': 4098, 'Dcab': 75, 'Jord': 3536}
for name, phone in table.items():
    print(f'Jack: {0[Jack]:d}; Sjored: {0[Sjored]:d}'.format(table))
```

It is not just limited to variables, we can also use expressions as a parameter to the format method.

```python
for x in range(1, 11):
    print('{0:2d} {1:3d} {2:4d}.format(x, x*x, x*x*x))
```

The `zfill(n)` is another important method for string formatting. Say you want to pad a value with zeroes instead of spaces, this method is used.

```python
'12'.zfill(5)
```

```python
'-3.14'.zfill(7)
```

```python
'3.14159265359'.zfill(5)
```

The old string formatting syntax is as follows. Here we used the `%` operator to provide values. This is known as string interpolation.

```python
import math
print('The value of pi is approximately %5.3f.' % math.pi)
```

### Reading and Writing Files

The `open()` method returns a file object is used with two positional argument and a key argument.
Filename and mode are the two positional arguments and encoding is a key argument.

```python
f = open('workfile', 'w', encoding='utf-8')
```

Some of the modes in which we can open the file:

* `r` - read only mode (default)
* `w` - write only mode
* `r+` - reading and writin mode
* appending `b` to the mode opens the file in binary mode. In binary mode, the data is read and written as byte objects.

The defacto encoding in which files are opened is `utf-8`.

It's a good practice to use the with keyword when dealing with file objects. The advantage is that the file is properly closed, with memory flushed after its suite finished, even if exception is raised. It is necessary to call `f.close()` if we are not opening files using the `with` keyword.

```python
with open('workfile', encoding='utf-8') as f:
    read_data = f.read()

f.closed
```

The method `f.read()` is used for reading the entire file at once. This is not recommended as the system may or may not be able to read it and depends on the availability of system memory.

```python
f.read()
```

The `readline()` method reads a single line from the file. The newline character `\n` is not stripped out of the line which is read. It returns an empty string if its the last line or if the file doesn't have a new line.

```python
f.readline()
f.readline()
```

Reading files line by line is memory efficient, fast and leads to simple code.

```python
for line in f:
    print(line, end = ' ')
```

The `f.write(str)` writes the contents of `str` to the file, returning the number of characters written.

```python
f.write('This is a test\n')
```

The other type of objects need to be converted either to string (in text mode) or bytes (in binary mode) before writing them.

```python
value = ('the answer', 42)
s = str(value)
f.write(s)
```

The `f.tell()` returns an integer giving the file object's current position in the file represented as number of bytes form beginning of the file when in binary mode and an opaque number when in text mode.

The `f.seek(offset, whence)` method is used to change the file object's position. The position is computed from adding offset to reference point and the reference is selected by the whence argument.

```python
f = open('workfile', 'rb+')
f.write(b'0123456789abcdef')
f.seek(5)
f.read(1)
f.seek(-3, 2)
f.read(1)
```

We can save data in file using a structured format called JSON (JavaScript Object Notation). The standard module for it is called `json` and it can take Python Data hierarchies and convert them to string representations. This process is called serializing. Reconstructing these Python Data hierarchies from the string representation is called deserializing.

We view a data structure's string representation in JSON format using the `json.dumps(data)` method.

```python
import json
data = {"fname": "Ritesh", "lname": "Kudalkar", age: 24}
json.dumps(data)
```

To decode an object again, we used `json.load(f)`

```python
with open('hey.json', encoding='utf8') as f:
    x = json.load(f)
    print(x)
```

## Errors and Exceptions

There are two distingusihable kinds of errors: syntax errors and exceptions.

### Syntax Errors

These are also known as parsing errors. Ocurrs when we don't follow proper python syntax.

```python
while True print("Hello World")
```

### Exceptions

Even if a statement or expression is syntactically correct, it may cause an error whe an attempt is made to execute it.

```python
10 * (1/0)
```

```python
4 + spam * 3
```

```python
'2' + 2
```

```python
ar = [1, 2, 3, 4]
ar[5]
```

```python
d = {"hello": "hola", "milk": "leche"}
d["thanks"]
```

### Handling Exceptions

It is possible to write programs that handle selected exceptions. We use the try, except and finally block to handle exceptions.

```python
while True:
    try:
        x = int(input("Please enter a number: "))
        break
    except ValueError:
        print("Oops!! That was not a valid number. Try again")
```

The flow is as follows:

* First the `try` clause is executed
* If no exception occur then the except clause is skipped after the execution of `try` caluse.
* If an exception occurs which does not match the exception named in the except clause, it is first passed to the next except block and if absent, then it is passed on to outer try statements. If no handler is found, it is an unhandled exception and the execution stops.

A `try` statement can have more than one except clause to specify how to handle different exceptions differently. Handlers only handle exceptions that occur in the corresponding try clause and not in other handlers of same try statement.
An except clause may also name multiple exceptions as paranthesized tuple.

```python
try:
    a = x[15] / 0
except (ZeroDivisionError, IndexError):
    print("A yo error occurred!!")
```

### Raising Exceptions

The `raise` statement allows the programmer to force a specified exception to occur.

```python
raise NameError('HiThere')
```

The argument to raise should be an instance of exception or a class derived from Exception or one its subclasses.

### User Defined Exceptions

Programs may name their own exception by creating a new exception class derived from the `Exception` class; directly or indirectly.

### Defining Clean-up Actions

The `try` statement has another optional clause which is intended to define clean up actions that must be executed under all circumstances.

```python
try:
    raise KeyboardInterrupt
except Exception:
    print("Error!")
finally:
    print("Goodbye world")
```

The `finally` clause if present will execute as the last task before the try statments completes. The finally clause runs whether or not the try statement produces an exception.

```python
def bool_return():
    try:
        return True
    finally:
        return False

bool_return()
```

If the `try` statement reaches a `break`, `continue` or `return` statement, the finally clause will execute just prior to it's execution.

If a `finally` clause includes a `return` statement, the returned value will be the one from the finally clause's `return` statement and not the value from `try` clause's `return` statement.

```python
def divide(x, y):
    try:
        result = x / y
    except ZeroDivisionError:
        print("division by zero!")
    else:
        print("result is", result)
    finally:
        print("executing finally clause")
```
