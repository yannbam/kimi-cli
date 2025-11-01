# Kimi CLI Quick Reference

## Essential Commands

```bash
# Start interactive mode
kimi

# Execute single command
kimi -c "list Python files"

# Use specific directory
kimi -w /path/to/project

# Continue session
kimi --continue

# Non-interactive mode
kimi --print -c "show README.md"
```

## Meta-Commands (Shell Mode)
```
/help          # Show all commands
/setup         # Configure API keys
/clear         # Reset conversation
/debug         # Show context info
/exit          # Quit
```

## Keyboard Shortcuts
- `Ctrl-X`: Toggle Agent/Shell mode
- `Ctrl-V`: Paste text/images
- `Ctrl-D`: Exit
- `@`: File completion

## Common Tools
```python
# File operations
ReadFile(path="/path/file.txt")
WriteFile(path="/path/file.txt", content="text")
Glob(pattern="*.py")
Grep(pattern="TODO", path="/path", type="py")

# System
Bash(command="ls -la")

# Web
SearchWeb(query="python tutorial", limit=5)
FetchURL(url="https://example.com")

# Tasks
Task(description="Fix bug", subagent_name="coder", prompt="details")
```

## Configuration
```bash
~/.kimi/config.json     # Main config
~/.kimi/sessions/       # Session files
```

## Help
```
kimi --help             # CLI options
kimi /help             # Meta-commands
kimi /feedback         # Report issues
```