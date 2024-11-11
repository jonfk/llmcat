# llmcat

Fast and flexible tool for copying files to language models from command-line, supporting fuzzy search, multi-file selection and respecting .gitignore rules.

```bash
# Copy specific file
llmcat path/to/file.txt

# Copy directory
llmcat ./src/

# Interactive mode (opens fuzzy finder)
llmcat
```

Output format:

```md
# File: src/main.rs
---
[content]

# File: lib/utils.rs
---
[content]
```

## Install

```bash
# Download the script
curl -o llmcat https://raw.githubusercontent.com/azer/llmcat/main/llmcat

# Make it executable
chmod +x llmcat

# Move to your PATH
sudo mv llmcat /usr/local/bin/
```

Required for interactive mode:
* fzf
* bat

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

#### Command-line

```bash
# Copy a single file
$ llmcat src/main.rs

# Copy directory
$ llmcat src/

# Ignore specific files
$ llmcat -i "*.log" ./src/

# Print output while copying
$ llmcat -p file.txt

# Print only the directory tree
$ llmcat -t ./src/
```
