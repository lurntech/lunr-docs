# LunarOS

**A Lightweight Operating System Compatible with LCC**

## Overview

LunarOS is a minimalist operating system designed with full compatibility for the LCC (Local C Compiler) toolchain. Built with simplicity and efficiency in mind, LunarOS provides a clean environment for C development using lcc.

## Key Features

- **LCC Native Support**: Full compatibility with lcc compiler toolchain
- **Minimal Footprint**: Designed to run efficiently on limited hardware
- **POSIX-like Interface**: Familiar system calls and APIs for C developers
- **Modular Architecture**: Clean separation between kernel and userspace
- **Educational Focus**: Clear, readable codebase for learning OS development

## System Requirements

### Minimum Hardware
- **CPU**: x86 or ARM processor
- **RAM**: 64 MB minimum, 128 MB recommended
- **Storage**: 100 MB for base installation
- **Display**: VGA-compatible graphics (640x480)

### Software Requirements
- **Compiler**: LCC 4.2 or later
- **Build Tools**: GNU Make or compatible
- **Assembler**: NASM (for x86) or GNU AS

## Architecture

LunarOS follows a microkernel-inspired design with the following components:

### Kernel Layer
- **Memory Manager**: Paging and virtual memory support
- **Process Scheduler**: Preemptive multitasking
- **Device Drivers**: Minimal driver framework
- **System Call Interface**: Clean syscall API for userspace

### Userspace
- **Standard Library**: libc implementation optimized for lcc
- **Shell**: Lightweight command interpreter
- **Core Utilities**: Basic file and process management tools
- **Init System**: Simple initialization and service management

## LCC Compatibility

LunarOS is specifically designed to work seamlessly with lcc:

### Supported LCC Features
- Standard C89/C90 language features
- LCC-specific extensions and optimizations
- Native code generation without external dependencies
- Direct compilation to executable format

### Build System Integration
```c
// Example: Compiling for LunarOS with lcc
lcc -target=lunaros -O2 -o program program.c
```

### System Headers
LunarOS provides lcc-compatible system headers:
- `<lunaros/syscall.h>` - System call wrappers
- `<lunaros/io.h>` - I/O operations
- `<lunaros/process.h>` - Process management
- `<lunaros/memory.h>` - Memory operations

## Getting Started

### Building LunarOS

```bash
# Clone the repository
git clone https://github.com/lunaros/lunaros.git
cd lunaros

# Configure for your target architecture
./configure --arch=x86 --compiler=lcc

# Build the kernel and system
make all

# Create bootable image
make iso
```

### Running LunarOS

#### On Real Hardware
```bash
# Write to USB drive (Linux)
dd if=lunaros.iso of=/dev/sdX bs=4M

# Write to USB drive (Windows - use Rufus or similar tool)
```

#### In a Virtual Machine
```bash
# Using QEMU
qemu-system-i386 -cdrom lunaros.iso -m 128M

# Using VirtualBox
VBoxManage createvm --name "LunarOS" --ostype Linux_64 --register
VBoxManage storagectl "LunarOS" --name "IDE" --add ide
VBoxManage storageattach "LunarOS" --storagectl "IDE" --port 0 --device 0 --type dvddrive --medium lunaros.iso
```

## Development with LCC

### Hello World Example

```c
#include <lunaros/io.h>

int main(void) {
    write(STDOUT, "Hello, LunarOS!\n", 16);
    return 0;
}
```

### System Call Example

```c
#include <lunaros/syscall.h>
#include <lunaros/process.h>

int main(void) {
    pid_t pid = fork();
    
    if (pid == 0) {
        // Child process
        exec("/bin/shell");
    } else {
        // Parent process
        wait(pid);
    }
    
    return 0;
}
```

## API Documentation

### System Calls

| Syscall | Number | Description |
|---------|--------|-------------|
| `exit` | 1 | Terminate process |
| `fork` | 2 | Create child process |
| `read` | 3 | Read from file descriptor |
| `write` | 4 | Write to file descriptor |
| `open` | 5 | Open file |
| `close` | 6 | Close file descriptor |
| `exec` | 7 | Execute program |
| `wait` | 8 | Wait for child process |

### Memory Management

```c
void* malloc(size_t size);
void free(void* ptr);
void* sbrk(intptr_t increment);
```

### Process Management

```c
pid_t fork(void);
int exec(const char* path);
void exit(int status);
pid_t wait(pid_t pid);
```

## File System

LunarOS uses a simple hierarchical file system:

```
/
├── bin/          # System binaries
├── dev/          # Device files
├── etc/          # Configuration files
├── home/         # User directories
├── lib/          # System libraries
├── tmp/          # Temporary files
└── usr/          # User programs
    ├── bin/
    ├── lib/
    └── include/
```

## Configuration

System configuration is stored in `/etc/lunaros.conf`:

```ini
[system]
hostname=lunaros
timezone=UTC

[kernel]
scheduler=preemptive
max_processes=256

[memory]
page_size=4096
heap_size=16M
```

## Contributing

We welcome contributions to LunarOS! Please see our contribution guidelines:

1. Fork the repository
2. Create a feature branch
3. Ensure all code compiles with lcc
4. Submit a pull request

### Coding Standards
- Follow K&R C style
- Use tabs for indentation
- Keep functions under 50 lines when possible
- Comment complex algorithms

## License

LunarOS is released under the MIT License. See LICENSE file for details.

## Resources

- **Website**: https://lunaros.org
- **Documentation**: https://docs.lunaros.org
- **Source Code**: https://github.com/lunaros/lunaros
- **Community Forum**: https://forum.lunaros.org
- **IRC**: #lunaros on irc.freenode.net

## Support

For bug reports and feature requests, please use our issue tracker:
https://github.com/lunaros/lunaros/issues

## Acknowledgments

- LCC compiler by Chris Fraser and David Hanson
- Inspiration from Plan 9, Minix, and early Unix systems
- The open source community

---

*LunarOS - Simple, Fast, Compatible*
