<!-- TITLE: DBX -->
<!-- SUBTITLE: Tips & Tricks for DBX -->

# DBX
## GDB <-> DBX Mappings
* http://www.fortran-2000.com/ArnaudRecipes/CompGdbDbx.html
* https://docs.oracle.com/cd/E19059-01/wrkshp50/805-4948/6j4m9ice4/index.html

## Important Commands
```text
(dbx) run [args to your program]
(dbx) set $ignoreonbptrap           # I kept hitting a trace/bpt trap
(dbx) set $deferevents              # allows setting bp in not loaded shared library
(dbx) set $repeat                   # useful, repeat commands with <enter> tjust like gdb
(dbx) stop in MySharedLibraryFunc   # defers breakpoint
(dbx) cont
```

## Other Useful Things
* https://stackoverflow.com/questions/801423/how-to-runtime-debug-shared-libraries
