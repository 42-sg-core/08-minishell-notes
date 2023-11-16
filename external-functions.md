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

## Process Control

### fork

Creates a new process.

```c
pid_t pid = fork();
```

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





rl_clear_history, rl_on_new_line,
rl_replace_line, rl_redisplay, add_history,
signal,
sigaction, sigemptyset, sigaddset, kill, exit,
getcwd, chdir, stat, lstat, fstat, unlink, execve,
dup, dup2, pipe, opendir, readdir, closedir,
strerror, perror, isatty, ttyname, ttyslot, ioctl,
getenv, tcsetattr, tcgetattr, tgetent, tgetflag,
tgetnum, tgetstr, tgoto, tputs
