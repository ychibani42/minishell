```
.
├── .vscode/                # VSCode settings and launch configurations
├── .gitignore              # Excludes build artifacts, objects, executables
├── .gitkeep                # Keeps empty directories in Git
├── Makefile                # Compilation rules: all/clean/fclean/re
├── libft/                  # Libft library dependency
├── lines/                  # Line reading utilities
├── silent_valgrind_readline # Valgrind-compatible readline
├── valgrind.sh             # Valgrind testing script
├── includes/               # Main header: structs, prototypes, macros
└── srcs/                   # Source code by functionality
    ├── clean/              # Memory and resource cleanup
    ├── errors/             # perror, custom errors
    ├── executor/           # execve, pipes, redirections
    ├── expander/           # $USER, $?, parameter expansion
    ├── here_doc/           # << LIMITER implementation
    ├── init/               # envp parsing, signals setup
    ├── lexer/              # Split by spaces, quotes, operators
    ├── minishell/          # Read-eval loop
    ├── parser/             # Command trees, pipes, redirections
    ├── token/              # Token creation, validation
    └── utils/              # Quote removal, path joining, etc
```

## Minishell - 42 School Project

Minishell is a complete Bash-like shell implementation in C, featuring a custom readline, lexer, parser, variable expansion, pipes, redirections, and built-in commands. It matches Bash 4.1 behavior exactly.

## Features

- **Built-ins**: `echo`, `cd`, `pwd`, `export`, `unset`, `env`, `exit`
- **Pipes**: `ls | grep a | wc -l`
- **Redirections**: `< > >> <<` with multiple files
- **Variable expansion**: `$USER`, `$?`, `$PATH`, `${var}`
- **Quotes**: Single/double quote handling, quote removal
- **Here-docs**: `cat << EOF`
- **Signals**: Ctrl+C (SIGINT), Ctrl+D (EOF), SIGQUIT
- **Wildcards**: `*` globbing (bonus)
- **Exit codes**: Proper `$?` status propagation

## Usage

```
make              # Build minishell
./minishell       # Launch shell (prompt: $ )
make valgrind     # Test with valgrind script
```

**Examples**:
```bash
$ echo "hello world"          # Built-in echo
$ ls -la | grep Makefile      # Pipe execution  
$ cat << EOF > file.txt       # Here-document
$ export USER=42student       # Environment variables
$ ls $PATH                    # Variable expansion
```

## Compilation

```
make          # Build with libft
make clean    # Remove objects
make fclean   # Full clean + libft
make re       # Rebuild
```
Flags: `-Wall -Wextra -Werror -lreadline -g3 -fsanitize=address`

## Allowed Libraries

- **Readline**: Custom wrapper for interactive input
- **Libft**: String manipulation, memory management
- **System calls**: `fork`, `execve`, `pipe`, `dup2`, etc.

## Return Codes Match

| Minishell | Bash  | Meaning |
|-----------|-------|---------|
| 0         | 0     | Success |
| 1         | 1     | General error |
| 126       | 126   | Command found, cannot execute |
| 127       | 127   | Command not found |

## Testing Scripts

- `valgrind.sh`: Memory leak detection
- `silent_valgrind_readline`: Readline leak suppression
- Multi-pipe tests, signal handling, edge cases

This structure ensures 42 Norm compliance (25 lines max per function) while maintaining modularity for debugging complex shell logic.

[1](https://42-cursus.gitbook.io/guide/2-rank-02/pipex)
[2](https://github.com/dpetrosy/42-Pipex)
