<!-- TITLE: Debugging -->
<!-- SUBTITLE: Tips & Tricks for Debugging -->

# GDB
## `~/.gdbinit`
Put the following lines into the `.gdbinit` file in your home directory to
* set the prompt to look like ![gdb prompt](/uploads/gdb-prompt.png "gdb prompt") and 
* use intel assembly format
by default.
```text
set prompt \001\033[1;31m\002(gdb)\001\033[0m\002\040
set disassembly-flavor intel
```

## Printing the Type of a Variable
See https://stackoverflow.com/questions/8528979/how-to-determine-if-an-object-is-an-instance-of-certain-derived-c-class-from-a.

### Static Type
To print the *static* (declared) type of a pointer `ptr` use:
```text
(gdb) ptype ptr
type = class SuperClass {
  // various members
} *
```

### Dynamic Type
To print the *dynamic* (actual) type behind a pointer `ptr` use:
```text
(gdb) set print object on
(gdb) ptype ptr
type = /* real type = DerivedClass * */
class SuperClass {
  // various members
} *
```

## Trace Thrown Exceptions
`catch throw`

## Execute Commands at \*point
### General
Execute some commands when a certain breakpoint or catchpoint is reached. If no breakpoint or catchpoint is specified explicitly, then the last defined one is used.

```text
commands
some      
gdb
instructions
end
```

### Example

```text
set pagination off    # (1)
catch throw           # (2)
commands              # (3)
bt                    # (4)
c                     # (5)
end                   # (6)
```

1. Do not stop on full pages.
2. Catch all exception throws
3. Begin of the command block that should be executed for the above defined catchpoint.
4. Show backtrace for each thrown exception.
5. Continue program execution
6. End of the command block.

## Saving & Loading Breakpoints
### Save Breakpoints to a File
`save breakpoints <filename>`

### Load Breakpoints from a File
`source <path/to/breakpoint-file>`

If the shared library isn't already loaded to that point in time use the following command before loading the breakpoints:
`set breakpoint pending on`

## Print All Elements of an Array
This works also with vectors.
`set print elements unlimited`

## Log Output to a File
* `set logging on` (logs by default to *gdb.txt*).
* `set logging file <filename>` to specify a dedicated log file.

## Printing the Size of a Variable/Type
* `print sizeof(variable)`
* `print sizeof(type)`

## Disable a Breakpoint
`disable [breakpoints] [list...]`
For example, `disable 1` to disable breakpoint 1.

## Debugging multi-process Applications
Source: https://sourceware.org/gdb/onlinedocs/gdb/Forks.html
For example, the Apache *httpd* web server.

```text
set detach-on-fork off
set non-stop on
b file.c:line
commands
bt
end
run <args>
```

Afterwards, do the appropriate action so that the breakpoint is hit (e.g. send a request). This will trigger the `bt` command, which will print the inferior and thread number (e.g. Thread 4.3 "httpd" hit Breakpoint 1, ... -> inferior 4, thread 3). Now, switch to the appropriate thread (e.g. with `thread 4.3`) and do "normal" debugging.