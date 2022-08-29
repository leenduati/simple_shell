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
