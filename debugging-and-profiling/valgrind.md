<!-- TITLE: Valgrind -->
<!-- SUBTITLE: Valgrind Tools and Options -->

# General
## Synopsis
`valgrind [valgrind-options] [your-program] [your-program-options]`

## Examples
* `valgrind --child-silent-after-fork=yes --error-exitcode=0 --leak-check=full --show-reachable=yes`
* `valgrind --log-file=valgrind_varnish%p.txt --num-callers=50 --max-threads=3000 --read-inline-info=yes --trace-children=yes --error-markers=begin,end --time-stamp=yes`

### Additional `-v` Flag
`valgrind -v --log-file=valgrind_varnish%p.txt --num-callers=50 --max-threads=3000 --read-inline-info=yes --trace-children=yes --error-markers=begin,end --time-stamp=yes`

### Without Log File
`valgrind --num-callers=50 --max-threads=3000 --read-inline-info=yes --trace-children=yes --error-markers=begin,end --time-stamp=yes`

### Without Tracing Children
*Note: This only affects children created with `exec`, not with `fork`!*
`valgrind --log-file=valgrind_varnish%p.txt --num-callers=50 --max-threads=3000 --read-inline-info=yes --error-markers=begin,end --time-stamp=yes`

# Memcheck
## General
Documentation: http://valgrind.org/docs/manual/mc-manual.html
> Memcheck is a memory error detector.

*All default options are sane.*

## Additional Options
`--malloc-fill=<hexnumber>`  
           Fills blocks allocated by malloc, new, etc, but not by calloc, with the specified byte. This can be useful when trying to shake out obscure memory corruption problems. The allocated area is
           still regarded by Memcheck as undefined -- this option only affects its contents. Note that --malloc-fill does not affect a block of memory when it is used as argument to client requests
           VALGRIND_MEMPOOL_ALLOC or VALGRIND_MALLOCLIKE_BLOCK.

`--free-fill=<hexnumber>`  
           Fills blocks freed by free, delete, etc, with the specified byte value. This can be useful when trying to shake out obscure memory corruption problems. The freed area is still regarded by
           Memcheck as not valid for access -- this option only affects its contents. Note that --free-fill does not affect a block of memory when it is used as argument to client requests
           VALGRIND_MEMPOOL_FREE or VALGRIND_FREELIKE_BLOCK.
					 
# Helgrind
## General
Documentation: http://valgrind.org/docs/manual/hg-manual.html
> Helgrind is a Valgrind tool for detecting synchronisation errors in C, C++ and Fortran programs that use the POSIX pthreads threading primitives.

*All default options are sane.*

# DRD
## General
Documentation: http://valgrind.org/docs/manual/drd-manual.html
> DRD is a Valgrind tool for detecting errors in multithreaded C and C++ programs. The tool works for any program that uses the POSIX threading primitives or that uses threading concepts built on top of the POSIX threading primitives.

## Options
`--trace-alloc=<yes|no> [default: no]`  
           Trace all memory allocations and deallocations. May produce a huge amount of output.

`--trace-fork-join=<yes|no> [default: no]`  
           Trace all thread creation and all thread termination events.

`--trace-mutex=<yes|no> [default: no]`  
           Trace all mutex activity.

`--trace-rwlock=<yes|no> [default: no]`  
           Trace all reader-writer lock activity.

`--trace-semaphore=<yes|no> [default: no]`  
           Trace all semaphore activity.
