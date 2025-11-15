# LunarOS API Reference

## System Calls

All system calls in LunarOS are optimized for LCC compilation and follow standard C calling conventions.

### Process Management

#### fork()
Create a new process by duplicating the calling process.

```c
#include <lunaros/process.h>

pid_t fork(void);
```

**Returns:**
- Child process: 0
- Parent process: PID of child
- Error: -1 (sets errno)

**Example:**
```c
pid_t pid = fork();
if (pid == 0) {
    // Child process
    exit(0);
} else if (pid > 0) {
    // Parent process
    wait(pid);
}
```

---

#### exec()
Replace current process with a new program.

```c
#include <lunaros/process.h>

int exec(const char* path);
int execv(const char* path, char* const argv[]);
int execve(const char* path, char* const argv[], char* const envp[]);
```

**Parameters:**
- `path` - Path to executable
- `argv` - Argument vector (NULL-terminated)
- `envp` - Environment vector (NULL-terminated)

**Returns:**
- Does not return on success
- -1 on error (sets errno)

**Example:**
```c
char* args[] = {"/bin/shell", "-c", "ls", NULL};
execv("/bin/shell", args);
// Only reached if execv fails
perror("exec failed");
```

---

#### exit()
Terminate the calling process.

```c
#include <lunaros/process.h>

void exit(int status);
```

**Parameters:**
- `status` - Exit status code (0-255)

**Example:**
```c
if (error_condition) {
    exit(1);
}
exit(0); // Success
```

---

#### wait()
Wait for a child process to change state.

```c
#include <lunaros/process.h>

pid_t wait(pid_t pid);
int waitpid(pid_t pid, int* status, int options);
```

**Parameters:**
- `pid` - Process ID to wait for, or -1 for any child
- `status` - Pointer to store exit status
- `options` - Wait options (WNOHANG, WUNTRACED)

**Returns:**
- PID of terminated child
- -1 on error

**Example:**
```c
int status;
pid_t child = waitpid(-1, &status, 0);
if (child > 0) {
    if (WIFEXITED(status)) {
        printf("Child exited with status %d\n", WEXITSTATUS(status));
    }
}
```

---

#### getpid()
Get process ID.

```c
#include <lunaros/process.h>

pid_t getpid(void);
pid_t getppid(void);  // Get parent PID
```

**Returns:** Current process ID (always succeeds)

---

### File Operations

#### open()
Open a file or device.

```c
#include <lunaros/io.h>

int open(const char* path, int flags);
int open(const char* path, int flags, mode_t mode);
```

**Flags:**
- `O_RDONLY` - Read-only
- `O_WRONLY` - Write-only
- `O_RDWR` - Read-write
- `O_CREAT` - Create if doesn't exist
- `O_TRUNC` - Truncate to zero length
- `O_APPEND` - Append mode

**Mode:**
- `0644` - rw-r--r--
- `0755` - rwxr-xr-x

**Returns:**
- File descriptor (≥0) on success
- -1 on error

**Example:**
```c
int fd = open("/tmp/test.txt", O_WRONLY | O_CREAT, 0644);
if (fd < 0) {
    perror("open failed");
    return -1;
}
```

---

#### read()
Read from a file descriptor.

```c
#include <lunaros/io.h>

ssize_t read(int fd, void* buf, size_t count);
```

**Parameters:**
- `fd` - File descriptor
- `buf` - Buffer to read into
- `count` - Maximum bytes to read

**Returns:**
- Number of bytes read
- 0 on EOF
- -1 on error

**Example:**
```c
char buffer[1024];
ssize_t n = read(fd, buffer, sizeof(buffer));
if (n > 0) {
    buffer[n] = '\0';
    printf("Read: %s\n", buffer);
}
```

---

#### write()
Write to a file descriptor.

```c
#include <lunaros/io.h>

ssize_t write(int fd, const void* buf, size_t count);
```

**Parameters:**
- `fd` - File descriptor
- `buf` - Buffer to write from
- `count` - Number of bytes to write

**Returns:**
- Number of bytes written
- -1 on error

**Example:**
```c
const char* msg = "Hello, LunarOS!\n";
ssize_t n = write(STDOUT, msg, strlen(msg));
if (n < 0) {
    perror("write failed");
}
```

---

#### close()
Close a file descriptor.

```c
#include <lunaros/io.h>

int close(int fd);
```

**Returns:**
- 0 on success
- -1 on error

---

#### lseek()
Reposition file offset.

```c
#include <lunaros/io.h>

off_t lseek(int fd, off_t offset, int whence);
```

**Whence values:**
- `SEEK_SET` - From beginning
- `SEEK_CUR` - From current position
- `SEEK_END` - From end

**Returns:**
- New offset on success
- -1 on error

**Example:**
```c
// Seek to beginning
lseek(fd, 0, SEEK_SET);

// Get current position
off_t pos = lseek(fd, 0, SEEK_CUR);

// Get file size
off_t size = lseek(fd, 0, SEEK_END);
```

---

### Memory Management

#### malloc()
Allocate memory.

```c
#include <lunaros/memory.h>

void* malloc(size_t size);
```

**Returns:**
- Pointer to allocated memory
- NULL on failure

**Example:**
```c
int* array = malloc(100 * sizeof(int));
if (array == NULL) {
    return -1;
}
// Use array...
free(array);
```

---

#### free()
Free allocated memory.

```c
#include <lunaros/memory.h>

void free(void* ptr);
```

**Parameters:**
- `ptr` - Pointer returned by malloc/calloc/realloc

---

#### calloc()
Allocate and zero memory.

```c
#include <lunaros/memory.h>

void* calloc(size_t nmemb, size_t size);
```

**Returns:**
- Pointer to zeroed memory
- NULL on failure

---

#### realloc()
Resize allocated memory.

```c
#include <lunaros/memory.h>

void* realloc(void* ptr, size_t size);
```

**Returns:**
- Pointer to resized memory
- NULL on failure (original pointer still valid)

---

#### sbrk()
Change data segment size.

```c
#include <lunaros/memory.h>

void* sbrk(intptr_t increment);
```

**Parameters:**
- `increment` - Bytes to add (positive) or remove (negative)

**Returns:**
- Previous program break
- (void*)-1 on error

---

### Directory Operations

#### chdir()
Change current directory.

```c
#include <lunaros/io.h>

int chdir(const char* path);
```

**Returns:**
- 0 on success
- -1 on error

---

#### getcwd()
Get current working directory.

```c
#include <lunaros/io.h>

char* getcwd(char* buf, size_t size);
```

**Returns:**
- `buf` on success
- NULL on error

**Example:**
```c
char cwd[256];
if (getcwd(cwd, sizeof(cwd)) != NULL) {
    printf("Current directory: %s\n", cwd);
}
```

---

#### mkdir()
Create a directory.

```c
#include <lunaros/io.h>

int mkdir(const char* path, mode_t mode);
```

**Returns:**
- 0 on success
- -1 on error

---

#### rmdir()
Remove an empty directory.

```c
#include <lunaros/io.h>

int rmdir(const char* path);
```

**Returns:**
- 0 on success
- -1 on error

---

### Time Functions

#### time()
Get current time.

```c
#include <lunaros/time.h>

time_t time(time_t* tloc);
```

**Returns:** Seconds since Unix epoch

---

#### sleep()
Sleep for specified seconds.

```c
#include <lunaros/time.h>

unsigned int sleep(unsigned int seconds);
```

**Returns:** 0 if slept fully, remaining seconds if interrupted

---

## Standard Library

### String Functions

```c
#include <string.h>

size_t strlen(const char* s);
char* strcpy(char* dest, const char* src);
char* strncpy(char* dest, const char* src, size_t n);
int strcmp(const char* s1, const char* s2);
int strncmp(const char* s1, const char* s2, size_t n);
char* strcat(char* dest, const char* src);
char* strchr(const char* s, int c);
char* strstr(const char* haystack, const char* needle);
```

### Memory Functions

```c
#include <string.h>

void* memcpy(void* dest, const void* src, size_t n);
void* memmove(void* dest, const void* src, size_t n);
void* memset(void* s, int c, size_t n);
int memcmp(const void* s1, const void* s2, size_t n);
```

### I/O Functions

```c
#include <stdio.h>

int printf(const char* format, ...);
int sprintf(char* str, const char* format, ...);
int snprintf(char* str, size_t size, const char* format, ...);
int scanf(const char* format, ...);
int sscanf(const char* str, const char* format, ...);

int putchar(int c);
int puts(const char* s);
int getchar(void);
char* gets(char* s);  // Deprecated - use fgets
```

### File I/O

```c
#include <stdio.h>

FILE* fopen(const char* path, const char* mode);
int fclose(FILE* stream);
size_t fread(void* ptr, size_t size, size_t nmemb, FILE* stream);
size_t fwrite(const void* ptr, size_t size, size_t nmemb, FILE* stream);
int fseek(FILE* stream, long offset, int whence);
long ftell(FILE* stream);
void rewind(FILE* stream);
int feof(FILE* stream);
int ferror(FILE* stream);
```

## Error Handling

### errno
Global error variable set by system calls.

```c
#include <errno.h>

extern int errno;
```

**Common Error Codes:**
- `ENOENT` - No such file or directory
- `EACCES` - Permission denied
- `EEXIST` - File exists
- `EINVAL` - Invalid argument
- `ENOMEM` - Out of memory
- `ENOSPC` - No space left on device

### perror()
Print error message.

```c
#include <stdio.h>

void perror(const char* s);
```

**Example:**
```c
if (open("/nonexistent", O_RDONLY) < 0) {
    perror("open");  // Prints: "open: No such file or directory"
}
```

## Compilation with LCC

### Basic Compilation

```bash
lcc -o program program.c
```

### With System Libraries

```bash
lcc -o program program.c -L/usr/lib/lunaros -llunaros
```

### Optimization

```bash
lcc -O2 -o program program.c
```

### Header Search Path

```bash
lcc -I/usr/include/lunaros -o program program.c
```

---

For more examples, see the `/usr/share/doc/lunaros/examples/` directory.
