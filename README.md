# llmcat

<img src="https://github.com/user-attachments/assets/4354459f-be48-41f5-b6e4-2f00fa78d40d" width="200" />


Fast and flexible tool for copying files to large language models from command-line, supporting fuzzy search, multi-file selection and automatically respecting `.gitignore` rules.

```bash
# Copy specific file
$ llmcat path/to/file.txt

# Copy directory
$ llmcat ./src/

# Interactive mode (opens fuzzy finder)
$ llmcat
```

Output format:

```markdown
# Directory: src/state

[file tree]

## File: src/state/config.ts
---
[file contents]
```

See also: [Interactive Demo]() | [Blog](https://azerkoculu.com/posts/llmcat-copy-code-from-cli-to-llms)

## Install

```bash
# Download the script
curl -o llmcat https://raw.githubusercontent.com/azer/llmcat/main/llmcat

# Make it executable
chmod +x llmcat

# Move to your PATH
sudo mv llmcat /usr/local/bin/
```

Required dependencies:
* fd (for file discovery)
* ripgrep (for text operations)
* fzf (for interactive selection)
* bat (for file preview in interactive mode)

## Usage

#### Interactive

When no path provided, llmcat opens fzf where you can search and select files by just pressing `tab` key.

Keybindings:
* tab: Select file (moves up after selection)
* shift-tab: Unselect file
* ctrl-/: Toggle preview
* ctrl-d: Directory mode
* ctrl-f: File mode
* enter: Confirm
* esc: Exit

**Example:**

Search and select files directories in a Phoenix project:

![llmcat 3](https://github.com/user-attachments/assets/d53ee548-8900-4b1a-bbc7-69a0c01b72e8)

#### Command-line

```bash
# Copy a single file
$ llmcat src/main.rs

# Copy directory
$ llmcat src/

# Ignore specific files (uses fd glob patterns)
$ llmcat -i "*.log" ./src/

# Ignore multiple patterns
$ llmcat -i "*.log" -i "*.tmp" ./src/

# Don't respect gitignore files
$ llmcat -n ./src/

# Include hidden files/directories
$ llmcat -H ./src/

# Print output while copying
$ llmcat -p file.txt

# Print only the directory tree
$ llmcat -t ./src/
```

# Manual

```
llmcat - Prepare files and directories for LLM consumption

Usage: llmcat [options] [path]
       llmcat (interactive mode with fzf)

Options:
    -h, --help              Show this help message
    -i, --ignore PATTERN    Additional ignore patterns (fd exclude format: glob pattern)
    -v, --version           Show version
    -t, --tree-only         Only output directory tree
    -q, --quiet             Silent mode (only copy to clipboard)
    -p, --print             Print copied files/content (default: quiet)
    -n, --no-ignore         Don't respect gitignore/ignore files
    -H, --hidden            Include hidden files/directories
    --debug                 Enable debug output

Interactive Mode (fzf):
    tab          - Select/mark multiple files
    shift-tab    - Unselect/unmark file
    ctrl-/       - Toggle preview window
    ctrl-d       - Select directory mode
    ctrl-f       - Select file mode
    enter        - Confirm selection(s)
    esc          - Exit

Examples:
    # Interactive file selection
    llmcat

    # Process specific file
    llmcat path/to/file.txt

    # Process directory with custom ignore
    llmcat -i "*.log" -i "*.tmp" ./src/

    # Print content while copying
    llmcat -p ./src/file.txt

Features:
    - Interactive fuzzy finder with file preview
    - Auto-copies output to clipboard
    - Automatically respects .gitignore, .ignore, and .fdignore files
    - Directory tree visualization
    - Multi-file selection
    - Cross-platform (Linux/OSX)
```

## Behavior Changes from v1.x

- Uses `fd` instead of `find`, automatically respecting `.gitignore` files
- Hidden files/directories are excluded by default (unlike `find`)
- Match patterns now use fd's glob syntax instead of grep patterns
- Uses ripgrep for faster text operations
