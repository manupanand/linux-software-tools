# Linux System Tools

A collection of high-performance command-line tools for Linux systems built with C and Rust, designed for system administration, automation, and daily operations.

## Overview

This repository contains custom-built CLI tools that leverage the power of C for low-level system operations and Rust for memory-safe, concurrent system utilities.

## Repository Structure

```
.
├── c/
│   └── cli-tool/           # C-based CLI tools
│       ├── src/            # Source files
│       ├── include/        # Header files
│       ├── Makefile        # Build configuration
│       └── README.md       # Tool-specific documentation
│
└── rust/
    └── cli-tool/           # Rust-based CLI tools
        ├── src/            # Source files
        ├── Cargo.toml      # Rust package configuration
        └── README.md       # Tool-specific documentation
```

## Prerequisites

### For C Tools (`/c`)
- GCC 9.0 or later (or Clang)
- GNU Make 4.0 or later
- Linux kernel headers
- Standard C library development files

```bash
# Debian/Ubuntu
sudo apt-get install build-essential linux-headers-$(uname -r)

# RHEL/CentOS/Fedora
sudo dnf groupinstall "Development Tools"
sudo dnf install kernel-devel

# Arch Linux
sudo pacman -S base-devel linux-headers
```

### For Rust Tools (`/rust`)
- Rust 1.70 or later
- Cargo (Rust package manager)

```bash
# Install Rust using rustup
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
source $HOME/.cargo/env
```

## Building the Tools

### C Tools
```bash
cd c/cli-tool
make                    # Build the tool
make clean              # Clean build artifacts
make install            # Install to /usr/local/bin (requires sudo)
make uninstall          # Uninstall the tool
```

### Rust Tools
```bash
cd rust/cli-tool
cargo build             # Build in debug mode
cargo build --release   # Build optimized release binary
cargo install --path .  # Install to ~/.cargo/bin
cargo clean             # Clean build artifacts
```

## Running the Tools

### C Tools
```bash
# After building
./c/cli-tool/bin/toolname [options]

# After installation
toolname [options]
```

### Rust Tools
```bash
# Debug build
./rust/cli-tool/target/debug/toolname [options]

# Release build
./rust/cli-tool/target/release/toolname [options]

# After installation
toolname [options]
```

## Tool Categories

### System Monitoring
- Process management utilities
- Resource usage monitors
- Performance profiling tools

### File Operations
- Advanced file manipulation
- Directory traversal utilities
- File system operations

### Network Utilities
- Network diagnostics
- Connection monitoring
- Protocol utilities

### Security Tools
- Permission management
- Security auditing
- Access control utilities

## Development Guidelines

### C Development Standards
- Follow C11 standard
- Use meaningful variable and function names
- Include comprehensive error handling
- Add proper memory management (no leaks)
- Document all public functions
- Use `const` where appropriate
- Check return values of system calls

### Rust Development Standards
- Follow Rust 2021 edition conventions
- Use `clippy` for linting: `cargo clippy`
- Format code with `rustfmt`: `cargo fmt`
- Write unit tests for all modules
- Use `Result` and `Option` types appropriately
- Avoid `unwrap()` in production code
- Document public APIs with doc comments

## Makefile Template (C)

Each C tool should include a Makefile with these targets:

```makefile
.PHONY: all clean install uninstall

CC = gcc
CFLAGS = -Wall -Wextra -O2 -std=c11
LDFLAGS = 
TARGET = toolname

all: $(TARGET)

$(TARGET): src/main.c
	$(CC) $(CFLAGS) -o bin/$(TARGET) src/*.c $(LDFLAGS)

clean:
	rm -f bin/$(TARGET)

install: $(TARGET)
	install -m 755 bin/$(TARGET) /usr/local/bin/

uninstall:
	rm -f /usr/local/bin/$(TARGET)
```

## Testing

### C Tools
```bash
cd c/cli-tool
make test               # Run test suite (if available)
./tests/run_tests.sh    # Run integration tests
```

### Rust Tools
```bash
cd rust/cli-tool
cargo test              # Run unit tests
cargo test --release    # Run tests in release mode
cargo test -- --nocapture  # Show test output
```

## Performance Considerations

### C Tools
- Minimize dynamic memory allocations
- Use stack allocation where possible
- Profile with `valgrind` and `gprof`
- Optimize critical paths

### Rust Tools
- Use `cargo build --release` for production
- Profile with `cargo flamegraph`
- Leverage zero-cost abstractions
- Use appropriate data structures

## Security Best Practices

- Validate all user inputs
- Never use unsafe system calls without validation
- Avoid buffer overflows (bounds checking)
- Use secure functions (`strncpy` instead of `strcpy`)
- Drop privileges when not needed
- Sanitize environment variables
- In Rust, minimize `unsafe` blocks and document them thoroughly

## Debugging

### C Tools
```bash
# Compile with debug symbols
make CFLAGS="-Wall -Wextra -g -std=c11"

# Debug with gdb
gdb ./bin/toolname

# Memory leak detection
valgrind --leak-check=full ./bin/toolname
```

### Rust Tools
```bash
# Debug with LLDB or GDB
rust-lldb ./target/debug/toolname
rust-gdb ./target/debug/toolname

# Backtrace on panic
RUST_BACKTRACE=1 cargo run
```

## Contributing

Contributions are welcome! Please:

1. Fork the repository
2. Create a feature branch
3. Follow coding standards for the respective language
4. Add tests for new functionality
5. Update documentation
6. Submit a pull request

### Code Review Checklist
- [ ] Code compiles without warnings
- [ ] All tests pass
- [ ] Memory leaks checked (C tools)
- [ ] Clippy warnings addressed (Rust tools)
- [ ] Documentation updated
- [ ] Error handling implemented
- [ ] Security considerations addressed

## License

This project is licensed under the MIT License - see the LICENSE file for details.

## Platform Support

- **Primary**: Linux (kernel 5.4+)
- **Tested on**: Ubuntu 20.04+, Debian 11+, RHEL 8+, Arch Linux
- **Architecture**: x86_64, ARM64

## Additional Resources

### C Programming
- [GNU C Library Documentation](https://www.gnu.org/software/libc/manual/)
- [Linux System Programming](http://man7.org/linux/man-pages/)
- [GNU Make Manual](https://www.gnu.org/software/make/manual/)

### Rust Programming
- [The Rust Book](https://doc.rust-lang.org/book/)
- [Rust by Example](https://doc.rust-lang.org/rust-by-example/)
- [The Cargo Book](https://doc.rust-lang.org/cargo/)
- [Command Line Apps in Rust](https://rust-cli.github.io/book/)

### Linux System Programming
- [Linux Kernel Documentation](https://www.kernel.org/doc/html/latest/)
- [man pages](https://linux.die.net/man/)
- [System Calls Reference](https://syscalls.kernelgrok.com/)

## Support

For bugs, feature requests, or questions:
- Open an issue on GitHub
- Check existing documentation
- Review man pages for system calls

## Roadmap

- [ ] Process management tools
- [ ] Network monitoring utilities
- [ ] File system tools
- [ ] Performance profiling utilities
- [ ] System automation scripts
- [ ] Container management tools