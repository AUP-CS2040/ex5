# Exercise 5 - Exceptions and Text IO

## Learning Goals

This exercise targets the understanding of the following subjects:

* try/catch (12.2, 12.4.3)
* exceptions types and organization (12.3)
* declaring exceptions (12.4.1)
* throwing and creating exceptions (12.4.2, 12.9)
* getting information from exceptions (12.4.4)
* finally and automatically closing resources (12.5, 12.11.2)
* when to use exceptions (12.6)
* re-throwing and chaining exceptions (12.7,12.8)
* files and text IO (12.10-12.12)


## Description
In this exercise, we will implement a platform independent terminal for manipulating file systems.
The terminal will display to the user the current working directory and will expect an input line from the user.
The user can execute one of several supported commands and should expect informative error messages when a command fails.

## General Instructions

* Please use top-down design when writing your code
* Please refer to the java API for information of the `File`, `Scanner` and `Exception` constructors, methods and thrown exceptions
* When opening, implicitly or explicitly, a stream, make sure to close it
* Include in your `main` method thorough tests for all commands


## Instructions

Please complete the followings:

* Create a package `aup.cs.terminal` and a class `Terminal` containing a `main` method
* The `main` method calls a `start` method on `Terminal` which starts a loop. The loop prints the current directory and expect a command from the user, i.e.

```
/home/me/ex7 >
```

The user can enter one of the following commands

* `exit` - which terminates the program
* `cd <d>` - changes to another directory
* `rm <f>` - removes a file from the current directory
* `cat <f>` - prints the content of the file
* `mkdir <d>` - creates a new directory with name d
* rm -r <f>` - removes a directory and all its content (Optional)
* ls` - lists the content of the current directory which should contain: 1) the date when it was last modified, 2) its size in bytes, 3) distinguish files from directories

In addition

* Your loop in the terminal should call a method which will parse the user input and return an instance of the `Command` class
Please create each command in its own class inheriting from `Command`
* The commands override a method with the following signature `public File exec()` which returns the (possibly new) current directory after executing the command
* You should have a `try/catch` block around your code of parsing and executing the command

The catch section should print informative error messages according to the following checked exceptions:

* `TerminalParsingException` - which denotes an illegal command and contains the following subclasses:
  * `TerminalCommandParsingException` - illegal command
  * `TerminalFlagParsingException` - illegal flag to a command
  * `TerminalArgumentParsingException` - illegal number of arguments to a command

* `TerminalExecutionException` - which denotes an error on execution and should print the original exception message

And in addition

* The first group of exceptions should have one constructor accepting a string message argument and passing it to the super constructor
* The second exception should get a string message as well as another exception and pass both to super
* None of your methods should declare an exception other than the above ones
* Use try/catch in order to catch all other exceptions and re-throw them using your custom exceptions
