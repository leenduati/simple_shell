**This folder called allowed_functions_manual contains a description of all functions and system calls that we will use in this project.**

1.access

access command is used to check whether the calling program has access to a specified file.
Also used to check whether a file exists or not.
'int access(const char*pathname, int mode)`
Here, the first argument takes the path to the directory/file and the second argument takes flags R_OK, W_OK, X_OK or F_OK.

F_OK flag : Used to check for existence of file.
R_OK flag : Used to check for read permission bit.
W_OK flag : Used to check for write permission bit.
X_OK flag : Used to check for execute permission bit.
Note: If access() cannot access the file, it will return -1 or else it will be 0.

Use `int argc, const char *argv[]` to get the parameters and arguments

2. chdir

function call that is used to change the current working dir (cwd)

`int chdir(const char *path);`
Parameter: Here, the path is the Directory path which the user want to make the current working directory.

Return Value: This command returns zero (0) on success. -1 is returned on an error and errno is set appropriately.

Note: It is declared in unistd.h.

3. close/open/read/write

Tells the OS you are donw with a file descriptor and close the file pointed by fd

`#include <fcntl.h>`
`int close(inf fd);`

Returns 0 on success, -1 on error
How it works in the OS

Destroy file table entry referenced by element fd of file descriptor table
– As long as no other process is pointing to it!
Set element fd of file descriptor table to NULL

open - Used to Open the file for reading, writing or both.

Syntax in C language 
`#include<sys/types.h>
#include<sys/stat.h>
#include <fcntl.h>  
int open (const char* Path, int flags [, int mode ]);`
Parameters
Path: path to file which you want to use 
use absolute path begin with “/”, when you are not work in same directory of file.
Use relative path which is only file name with extension, when you are work in same directory of file.
flags : How you like to use
O_RDONLY: read only, O_WRONLY: write only, O_RDWR: read and write, O_CREAT: create file if it doesn’t exist, O_EXCL: prevent creation if it already exists

read - From the file indicated by the file descriptor fd, the read() function reads cnt bytes of input into the memory area indicated by buf. A successful read() updates the access time for the file.
Syntax in C language 
`size_t read (int fd, void* buf, size_t cnt);`
Parameters:
fd: file descriptor
buf: buffer to read data from
cnt: length of buffer
Returns: How many bytes were actually read

return Number of bytes read on success
return 0 on reaching end of file
return -1 on error
return -1 on signal interrupt
Important points

buf needs to point to a valid memory location with length not smaller than the specified size because of overflow.
fd should be a valid file descriptor returned from open() to perform read operation because if fd is NULL then read should generate error.
cnt is the requested number of bytes read, while the return value is the actual number of bytes read. Also, some times read system call should read less bytes than cnt.

write - Writes cnt bytes from buf to the file or socket associated with fd. cnt should not be greater than INT_MAX (defined in the limits.h header file).

`#include <fcntl.h>
size_t write (int fd, void* buf, size_t cnt);`

Parameters:

fd: file descriptor
buf: buffer to write data to
cnt: length of buffer
Returns: How many bytes were actually written

return Number of bytes written on success
return 0 on reaching end of file
return -1 on error
return -1 on signal interrupt

4. execve

The exec family of functions replaces the current running process with a new process
It can be used to run a C program by using another C program. It comes under the header file unistd.h. 
execve() system call loads a new program into a process memory
The existing process is discarded, and newly created process gets all new stack, data and heap
`int execv(const char *path, char *const argv[]);`
path: should point to the path of the file being executed. 
argv[]: is a null terminated array of character pointers.

5. exit

access return value can be accessed by echo $?
`#include <stdlib.h>`
`exit(0);`
`exit(EXIT_FAILURE)`
`exit(EXIT_SUCCESS)`

6. _exit

The _Exit() function in C/C++ gives normal termination of a program without performing any cleanup tasks. 
For example, it does not execute functions registered with atexit.
Return Value: The _Exit() function returns nothing.

7. fflush

fflush() is typically used for output stream only. Its purpose is to clear (or flush) the output buffer and move the buffered data to console (in case of stdout) or disk (in case of file output stream)

8. fork

fork is a system call used to ceate a new prcoess, which runs concurrently with the process that makes the original call
 A child process uses the same pc(program counter), same CPU registers, same open files which use in the parent process
 It takes no parameters and returns an integer value
 Negative Value: creation of a child process was unsuccessful.
Zero: Returned to the newly created child process.
Positive value: Returned to parent or caller. The value contains process ID of newly created child process.
Example:
`#include <stdio.h>`
`#include <sys/types.h>`
`#include <unistd.h>`
`int main()`
`{`
  
    `// make two process which run same`
    `// program after this instruction`
    `fork();`
  
    `printf("Hello world!\n");`
    `return 0;`
`}`

Output
`Hello world!`
`Hello world!`

Example
`#include <stdio.h>`
`#include <sys/types.h>`
`int main()`
`{`
    `fork();`
    `fork();`
    `fork();`
    `printf("hello\n");`
    `return 0;`
`}`

Output

*NB: The fork system call creates a new process.*
*The new process created by fork() is a copy of the current process except for the returned value.*
*The exec() system call replaces the current process with a new program.*

9. free / malloc

“malloc” or “memory allocation” method in C is used to dynamically allocate a single large block of memory with the specified size.
 It returns a pointer of type void which can be cast into a pointer of any form. 
 It doesn’t Initialize memory at execution time so that it has initialized each block with the default garbage value initially. 
`ptr = (int*) malloc(100 * sizeof(int));`
“calloc” or “contiguous allocation” method in C is used to dynamically allocate the specified number of blocks of memory of the specified type. it is very much similar to malloc() but has two different points and these are:
It initializes each block with a default value ‘0’.
It has two parameters or arguments as compare to malloc().
`ptr = (float*) calloc(25, sizeof(float));`
This statement allocates contiguous space in memory for 25 elements each with the size of the float.
“free” method in C is used to dynamically de-allocate the memory. 
The memory allocated using functions malloc() and calloc() is not de-allocated on their own

10. getcwd
`#define _POSIX_SOURCE`
`#include <unistd.h>`

`char *getcwd(char *buffer, size_t size);`
Determines the path name of the working directory and stores it in buffer.
size - The number of characters in the buffer area.
buffer- The name of the buffer that will be used to hold the path name of the working directory. buffer must be big enough to hold the working directory name, plus a terminating NULL to mark the end of the name.
Returned value
If successful, getcwd() returns a pointer to the buffer, else a NULL pointer

11. getline
The latest and most trendy function for reading a string of text is getline().
`getline(&buffer,&size,stdin);`
&buffer is the address of the first character position where the input string will be stored. It’s not the base address of the buffer, but of the first character in the buffer
&size is the address of the variable that holds the size of the input buffer, another pointer.
stdin is the input file handle. So you could use getline() to read a line of text from a file, but when stdin is specified, standard input is read.

12. getpid
Getpid() is the function used to get the process ID of the process that calls that function
The PID for the initial process is 1, and then each new process is assigned a new Id.
It is a simple approach to getting the PID. This function only helps you in getting the unique processes ids.

13. isatty
Determines if a file descriptor, fildes, is associated with a terminal.
works in an environment where either a controlling terminal exists, or stdin and stderr refer to tty devices. 
Specifically, it does not work in a TSO environment.

14. kill

sends a signal to a process or process group specified by pid
`int kill( pid_t pid, int sig );`   
pid
(Input) The process ID or process group ID to receive the signal.

sig
(Input) The signal to be sent.

15. opendir/closedir/readdir

`#include <dirent.h>
int closedir(DIR *dirp);`

closedir() function shall close the directory stream referred to by the argument dirp.

The opendir() function shall open a directory stream corresponding to the directory named by the dirname argument.

readdir() function returns a pointer to a structure representing the directory entry at the current position in the directory stream specified by the argument dirp, and positions the directory stream at the next entry. 
It returns a null pointer upon reaching the end of the directory stream.

16. perror

displays the description of the error that corresponds to the error code stored in the system variable errno 
errno is a system variable that holds the error code referring to the error condition. A call to a library function produces this error condition.
`void perror(const char *str)`

17. signal

A signal is an event which is generated to notify a process or thread that some important situation has arrived
When a process or thread has received a signal, the process or thread will stop what its doing and take some action. 
Signal may be useful for inter-process communication.

Signal Name	Description
SIGHUP	Hang-up the process. The SIGHUP signal is used to report disconnection of the user’s terminal, possibly because a remote connection is lost or hangs up.
SIGINT	Interrupt the process. When the user types the INTR character (normally Ctrl + C) the SIGINT signal is sent.
SIGQUIT	Quit the process. When the user types the QUIT character (normally Ctrl + \) the SIGQUIT signal is sent.
SIGILL	Illegal instruction. When an attempt is made to execute garbage or privileged instruction, the SIGILL signal is generated. Also, SIGILL can be generated when the stack overflows, or when the system has trouble running a signal handler.
SIGTRAP	Trace trap. A breakpoint instruction and other trap instruction will generate the SIGTRAP signal. The debugger uses this signal.
SIGABRT	Abort. The SIGABRT  signal is generated when abort() function is called. This signal indicates an error that is detected by the program itself and reported by the abort() function call.
SIGFPE	Floating-point exception. When a fatal arithmetic error occurred the SIGFPE signal is generated.
SIGUSR1 and SIGUSR2	The signals SIGUSR1 and SIGUSR2 may be used as you wish. It is useful to write a signal handler for them in the program that receives the signal for simple inter-process communication.

18. stat/lstat/fstat

These functions return information about a file. No permissions are required on the file itself, but — in the case of stat() and lstat() — execute (search) permission is required on all of the directories in path that lead to the file.

stat() stats the file pointed to by path and fills in buf.

lstat() is identical to stat(), except that if path is a symbolic link, then the link itself is stat-ed, not the file that it refers to.

fstat() is identical to stat(), except that the file to be stat-ed is specified by the file descriptor filedes.

19. strtok

Splits str[] according to given delimiters and returns the next token. It needs to be called in a loop to get all tokens. It returns NULL when there are no more tokens
`char * strtok(char str[], const char *delims);`

`// C/C++ program for splitting a string
// using strtok()
#include& lt; stdio.h & gt;
#include& lt; string.h & gt;

int main()
{
	char str[] = "Geeks-for-Geeks"
	;

	// Returns first token
	char* token = strtok(str, " - ");

	// Keep printing tokens while one of the
	// delimiters present in str[].
	while (token != NULL) {
		printf(" % s\n & quot;, token);
		token = strtok(NULL, " - ");
	}

	return 0;
}`

20. wait/waitpid/wait3/wait4

Waits for a child process to stop or end.

`#include <sys/wait.h>
pid_t wait (StatusLocation)
int *StatusLocation;
pid_t wait ((void *) 0)

#include <sys/wait.h>
pid_t waitpid (ProcessID,StatusLocation,Options)
int *StatusLocation;
pid_t ProcessID;
int Options;

#include <sys/time.h>
#include <sys/resource.h>
#include <sys/wait.h>
pid_t wait3 (StatusLocation, Options,ResourceUsage)
int *StatusLocation;
int Options; struct rusage *ResourceUsage;

pid_t wait364 (StatusLocation, Options,ResourceUsage)
int *StatusLocation;
int Options;
struct rusage64 *ResourceUsage;

pid_t wait4 (ProcessID,(StatusLocation, Options,ResourceUsage)
pid_t ProcessID;
int *StatusLocation;
int Options;
struct rusage64 *ResourceUsage;`



