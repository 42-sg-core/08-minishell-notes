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

rl_clear_history, rl_on_new_line,
rl_replace_line, rl_redisplay, add_history,
fork, wait, waitpid, wait3, wait4, signal,
sigaction, sigemptyset, sigaddset, kill, exit,
getcwd, chdir, stat, lstat, fstat, unlink, execve,
dup, dup2, pipe, opendir, readdir, closedir,
strerror, perror, isatty, ttyname, ttyslot, ioctl,
getenv, tcsetattr, tcgetattr, tgetent, tgetflag,
tgetnum, tgetstr, tgoto, tputs
