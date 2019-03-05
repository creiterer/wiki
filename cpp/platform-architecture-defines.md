<!-- TITLE: Platform & Architecture Defines -->
<!-- SUBTITLE: Preprocessor Defines for Various Platforms and Architectures -->

# Preprocessor Defines Table
| Define                                    | Description                                   |
|:------------------------------------------|:----------------------------------------------|
| `_WIN32`                                  | Both 32 bit and 64 bit windows                |
| `_WIN64`                                  | 64 bit windows only                           |
| `__unix__`                                | Unix systems (Linux, BSD, Mac OS X, AIX, Solaris SPARC, Solaris x86) |
| `__APPLE__`, `__MACH__`                   | Mac OS X                                      |
| `__linux__`                               | Linux                                         |
| `__FreeBSD__`                             | FreeBSD                                       |
| `_AIX`                                    | IBM AIX                                       |
| `__sun__`                                 | Solaris SPARC, Solaris x86                    |
| `__svr4__`                                | Solaris SPARC, Solaris x86                    |
| `__i386__`                                | 32-bit systems                                |
| `__x86_64__`                              | 64-bit systems                                |
| `__s390__`                                | linux-s390                                    |
| `__powerpc__`                             | linux-ppc                                     |

# Listing Predefined Preprocessor Defines
Sources:
* https://stackoverflow.com/questions/2224334/gcc-dump-preprocessor-defines
* https://stackoverflow.com/questions/142508/how-do-i-check-os-with-a-preprocessor-directive/8249232

List all predefined preprocessor defines on a particular system:
* `gcc -dM -E - < /dev/null`.
* `gcc -m32 -dM -E - < /dev/null` to show the defines for 32-bit.

# Additional Notes
* Prefer the defines with two underscores as prefix and suffix. For instance, prefer `__unix__` over `unix` and `__unix`, or `__linux__` over `linux` and `__linux`.
* According to https://stackoverflow.com/questions/142508/how-do-i-check-os-with-a-preprocessor-directive/8249232, `linux` and `__linux` are obsolete (not POSIX compliant).