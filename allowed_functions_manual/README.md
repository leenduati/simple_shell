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

2.chdir

function call that is used to change the current working dir (cwd)

`int chdir(const char *path);`
Parameter: Here, the path is the Directory path which the user want to make the current working directory.

Return Value: This command returns zero (0) on success. -1 is returned on an error and errno is set appropriately.

Note: It is declared in unistd.h.

3. close

Tells the OS you are donw with a file descriptor and close the file pointed by fd

`#include <fcntl.h>`
`int close(inf fd);`

Returns 0 on success, -1 on error
How it works in the OS

Destroy file table entry referenced by element fd of file descriptor table
– As long as no other process is pointing to it!
Set element fd of file descriptor table to NULL

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
