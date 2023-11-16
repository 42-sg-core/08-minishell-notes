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

rl_clear_history, rl_on_new_line,
rl_replace_line, rl_redisplay, add_history,
dup, dup2, pipe, opendir, readdir, closedir,
strerror, perror, isatty, ttyname, ttyslot, ioctl,
getenv, tcsetattr, tcgetattr, tgetent, tgetflag,
tgetnum, tgetstr, tgoto, tputs
