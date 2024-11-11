# llmcat

CLI tool to quickly select & copy files / dirs for LLMs.

Usage: https://x.com/azerkoculu/status/1855973784009777217

Manual: 
```
llmcat - Prepare files and directories for LLM consumption

Usage: llmcat [options] [path]
       llmcat (interactive mode with fzf)

Options:
    -h, --help              Show this help message
    -i, --ignore PATTERN    Additional ignore patterns (grep -E format)
    -v, --version          Show version
    -t, --tree-only        Only output directory tree
    -q, --quiet            Silent mode (only copy to clipboard)
    -p, --print            Print copied files/content (default: quiet)
    --debug                Enable debug output

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
    llmcat -i "*.log|*.tmp" ./src/

    # Print content while copying
    llmcat -p ./src/file.txt

Features:
    - Interactive fuzzy finder with file preview
    - Auto-copies output to clipboard
    - Respects .gitignore
    - Directory tree visualization
    - Multi-file selection
    - Cross-platform (Linux/OSX)
```
