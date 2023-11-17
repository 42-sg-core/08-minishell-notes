# External Functions

## Input / Output

### free

Frees dynamically allocated memory.

```c
free(buffer);
```

### malloc

Dynamically allocates memory.

```c
char *buffer = malloc(size);
```

### printf

Outputs a formatted string to stdout.

```c
printf("Hello, World!\n");
```

### readline

Reads a line from the terminal.

```c
char *line = readline("prompt> ");
```

### write

Writes data to a file descriptor.

```c
write(fd, buffer, nbytes);
```

## File Operations

### access

Checks thes user's permissions for a file.

```c
access("filename", R_OK);
```

### close

Closes a file descriptor.

```c
close(fd);
```

### open

Opens a file descriptor.

```c
int fd = open("filename", O_RDONLY);
```

### read

Reads data from a file descriptor.

```c
read(fd, buffer, nbytes);
```

## File Descriptor Manipulation

### dup

Duplicates an existing file descriptor.

```c
int newfd = dup(oldfd);
```

Creates a copy of the file descriptor oldfd, assigning it the lowest-numbered available file descriptor. This is useful when you need to redirect output or input streams in a Unix-like environment. For instance, it's commonly used in shell implementations to handle redirections like duplicating file descriptors for stdin, stdout, or stderr.

### dup2

Duplicates an existing file descriptor to a specified file descriptor.

```c
int newfd = dup2(oldfd, targetfd);
```

Similar to dup, but it allows you to specify the file descriptor number (targetfd) for the duplicate. If targetfd is already open, dup2 will first close it before duplicating oldfd. This is particularly useful when you want to redirect output or input streams to or from specific file descriptors, offering more control compared to dup.

### pipe

Creates a pipe.

```c
int fds[2];
pipe(fds);
```

## Directory Operations

### closedir

Closes a directory stream.

```c
closedir(dir);
```

Used to close the directory stream. This is important for resource management, ensuring that any resources associated with the directory stream are released.

### opendir

Open a directory stream.

```c
DIR *dir = opendir("/path/to/directory");
```

Used to open a directory stream corresponding to the directory name provided. It returns a pointer to the directory stream, which can be used with readdir to read the directory's contents. It's essential for directory traversal operations.

### readdir

Reads a directory entry from a directory stream.

```c
struct dirent *entry;
while ((entry = readdir(dir)) != NULL) {
  printf("%s\n", entry->d_name);
}
```

Sequentially reads directory entries from the directory stream opened by opendir. It returns a pointer to a struct dirent representing the next directory entry in the directory stream. It's used for iterating over all files and directories within a directory.

## Directory and File Information

### chdir

```c
chdir("/path/to/dir");
```

### fstat

Obtains information about a file based on an open file descriptor.

```c
struct stat statbuf;
fstat(fd, &statbuf);
```

Operates on an open file descriptor rather than a pathname. This is useful for getting file information when you have the file descriptor from operations like open or socket, and it works with regular files, special files, pipes, and sockets.

### getcwd

Gets the current working directory.

```c
char cwd[1024];
getcwd(cwd, sizeof(cwd));
```

### lstat

Similar to `stat`, but does not follow symbolic links.

```c
struct stat statbuf;
lstat("linkname", &statbuf);
```

 Identical to stat in all respects except one: if the pathname is a symbolic link, lstat returns information about the link itself, not the file it points to. This is crucial for applications that need to distinguish between symbolic links and regular files.

### stat

Obtain information about the file pointed to by the path.

```c
struct stat statbuf;
stat("filename", &statbuf);
```

Retrieves detailed information about the file identified by the given pathname, such as size, permissions, and modification time. It follows symbolic links, meaning if the pathname is a symbolic link, it returns information about the file the link points to, not the link itself.

### unlink

Removes a file.

```c
unlink("filename");
```

## Process Control

### exit

Terminates the calling process.

```c
exit(EXIT_SUCCESS);
```

### fork

Creates a new process.

```c
pid_t pid = fork();
```

### kill

Send a signal to a process.

```c
kill(pid, SIGKILL);
```

### sigaction

More advanced and reliable way to handle signals.

```c
struct sigaction sa;
sa.sa_handler = signal_handler_function;
sigemptyset(&sa.sa_mask);
sa.sa_flags = 0;
sigaction(SIGINT, &sa, NULL);
```

Provides more control and reliability compared to signal. It allows specifying additional options (like blocking other signals during the execution of the signal handler) and is more consistent across different Unix-like systems. This makes it preferable for complex applications that require robust signal handling.

### sigaddset

Adds a specific signal to a signal set.

```c
sigset_t set;
sigemptyset(&set);
sigaddset(&set, SIGINT);
```

After initializing a signal set with sigemptyset, sigaddset is used to add individual signals (like SIGINT) to the set. It's useful when you want to block, unblock, or wait for multiple signals as a group. This function is essential for managing complex signal handling scenarios where multiple signals need to be considered together.

### sigemptyset

Initializes the signal set to be empty.

```c
sigset_t set;
sigemptyset(&set);
```

Used to initialize a signal set, which is a data type (sigset_t) that can hold multiple signals. This function ensures that the set is empty to start with, meaning no signals are currently part of the set. It is typically used before adding specific signals to the set with sigaddset.

### signal

Sets a function to handle a specific signal.

```c
signal(SIGINT, signal_handler_function);
```

Used to define a custom function (signal_handler_function) that will be executed when the specified signal (SIGINT in this case) is received. It's a simpler, older signal handling mechanism and its behavior can vary across different systems. This can lead to portability issues. Generally, it's used for basic signal handling needs.

### wait

Suspends execution of the calling process until one of its children terminates.

```c
pid_t child_pid = wait(&status);
```

Used to wait for any child process to end. It is not possible to specify a particular child process to wait for.

### wait3

Similar to `wait`, but also returns resource usage information about the child.

```c
pid_t child_pid = wait3(&status, options, &rusage);
```

Extends wait by allowing the calling process to obtain information about the child's resource usage (via rusage). It also supports the use of options like waitpid.

### wait4

Suspends execution of the calling process until a child specified by `pid` changes state, and additionally returns resource usage information about the child.

```c
pid_t child_pid = wait4(specific_pid, &status, options, &rusage);
```

Similar to waitpid, but it extends its functionality by also providing resource usage information about the child (similar to wait3). It allows for specific PID targeting and options usage.

### waitpid

Suspends execution of the calling process until a child specified by `pid` argument changes state.

```c
pid_t child_pid = waitpid(specific_pid, &status, options);
```
Provides more control than wait. It can wait for a specific child process (or any child process if pid is -1) and it supports additional options for non-blocking waits and more.

## Process Execution

### execve

Executes a program.

```c
char *args[] = {"program", "arg1", "arg2", NULL};
execve("program", args, envp);
```

## Error Handling

### perror

Print a human-readable error message to standard error.

```c
perror("Error occurred");
```

Serves a similar purpose to strerror but with a slight difference. It prints a custom message followed by a colon and the textual representation of the current errno value. perror is convenient for debugging and error logging, as it automatically includes the error description without requiring an explicit call to strerror.

### strerror

Convert an error number into a human-readable string.

```c
int errnum = errno;
printf("Error: %s\n", strerror(errnum));
```

Takes an error number (usually obtained from errno) and returns a pointer to the corresponding message string that describes the error. This is particularly useful for displaying error messages in a more user-friendly format, making it easier to understand what went wrong during program execution.

## Terminal Control

### getenv

Gets an environment variable.

```c
char *path = getenv("PATH");
```

### ioctl

Controls device.

```c
ioctl(fd, request, ...);
```

### isatty

Determines if a file descriptor refers to a terminal.

```c
if (isatty(STDIN_FILENO)) {
  printf("Standard input is a terminal.\n");
}
```

Checks if a file descriptor (like STDIN_FILENO, STDOUT_FILENO, or STDERR_FILENO) is associated with a terminal device. This function is often used to determine whether standard input/output/error are connected to a terminal, which can influence how a program behaves (e.g., whether to use terminal-specific operations).

### tcgetattr

Gets the current settings of the terminal.

```c
struct termios termSettings;
tcgetattr(STDIN_FILENO, &termSettings);
```

Fetches the current settings of the specified terminal. This includes various parameters such as input/output speed, control characters, local modes, etc. It's commonly used in conjunction with tcsetattr to modify terminal settings: first, get the current settings, modify them as needed, and then set them using tcsetattr.

### tcsetattr

Sets the parameters associated with the terminal.

```c
struct termios termSettings;
tcgetattr(STDIN_FILENO, &termSettings);
// Modify termSettings as needed
tcsetattr(STDIN_FILENO, TCSANOW, &termSettings);
```

Used to set the attributes of a terminal device, such as setting the input and output modes, control characters, etc. The changes can be applied immediately (TCSANOW), after all output has been transmitted (TCSADRAIN), or after all input has been received but not read (TCSAFLUSH). This function is essential for customizing the behavior of terminal input and output.

### ttyname

Gets the name of the terminal associated with a file descriptor.

```c
char *tty = ttyname(STDIN_FILENO);
if (tty) {
  printf("Standard input is connected to %s\n", tty);
}
```

Returns the name of the terminal device connected to a given file descriptor, such as /dev/tty for UNIX systems. It's useful for obtaining human-readable terminal device names, which can be used for logging, debugging, or displaying terminal-related information to the user.

### ttyslot

Finds the index of the current user's terminal in some system files.

```c
int slot = ttyslot();
if (slot > 0) {
  printf("Terminal slot number: %d\n", slot);
}
```

Less commonly used function that returns the index of the terminal associated with the current process in system files like /etc/ttys. This index can be used in certain system-level operations or for retrieving specific information about the user's terminal session.

rl_clear_history, rl_on_new_line,
rl_replace_line, rl_redisplay, add_history,
tgetent, tgetflag,
tgetnum, tgetstr, tgoto, tputs
