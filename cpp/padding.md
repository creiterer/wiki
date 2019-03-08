<!-- TITLE: Padding -->
<!-- SUBTITLE: An Example for Padding -->

# Padding in a `struct`

```text
struct worker_score {																							with padding on 64 bit system				with padding on 32 bit system
    int thread_num;																		4						 4 + 4 = 8												4
#if APR_HAS_THREADS
    apr_os_thread_t tid;																  (8)							    8												4
#endif
    /* With some MPMs (e.g., worker), a worker_score can represent
     * a thread in a terminating process which is no longer
     * represented by the corresponding process_score.  These MPMs
     * should set pid and generation fields in the worker_score.
     */
    pid_t pid;																			 4								 4												4
    ap_generation_t generation;															4								 4		-> 24 -> 0x18						   4 		-> 16 -> 0x10
    unsigned char status;																  1						 1 + 7 = 8		-> 32 -> 0x20				   1 + 3 = 4		 -> 20 -> 0x14
    unsigned long access_count;															8								 8		-> 40 -> 0x28						   4		 -> 24 -> 0x18
    apr_off_t     bytes_served;															8
    unsigned long my_access_count;														 8
    apr_off_t     my_bytes_served;														 8
    apr_off_t     conn_bytes;															  8
    unsigned short conn_count;															 2
    apr_time_t start_time;																 8
    apr_time_t stop_time;																  8
#ifdef HAVE_TIMES
    struct tms times;																	 (8*4=32)
#endif
    apr_time_t last_used;																  8
    char client[32];		/* Keep 'em small... */									   32
    char request[64];		/* We just want an idea... */								64
    char vhost[32];	        /* What virtual host is being accessed? */				 32
};																					--------------
																					     247

```
