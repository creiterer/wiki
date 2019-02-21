<!-- TITLE: Debugging -->
<!-- SUBTITLE: Tips & Tricks for Debugging -->

# GDB
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
