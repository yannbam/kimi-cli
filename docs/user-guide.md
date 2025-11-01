# Kimi CLI User Guide

A comprehensive guide to using Kimi CLI - the AI-powered command-line interface for software engineering tasks.

## Table of Contents

- [Installation](#installation)
- [Quick Start](#quick-start)
- [Command Line Options](#command-line-options)
- [UI Modes](#ui-modes)
- [Interactive Features](#interactive-features)
- [Available Tools](#available-tools)
- [Configuration](#configuration)
- [Agent System](#agent-system)
- [Custom Agents](#custom-agents)
- [Session Management](#session-management)
- [Best Practices](#best-practices)
- [Troubleshooting](#troubleshooting)

## Installation

### Prerequisites
- Python 3.13 or higher
- `uv` package manager (recommended)

### Install with uv
```bash
# Install from PyPI
uv tool install kimi-cli

# Or install from source
uv sync
uv pip install -e .
```

### Verify Installation
```bash
kimi --version
```

## Quick Start

### Basic Usage
```bash
# Start interactive mode (default)
kimi

# Execute a single command
kimi -c "list all Python files in current directory"

# Use a specific working directory
kimi -w /path/to/your/project

# Continue previous session
kimi --continue
```

### First Time Setup
```bash
# Run setup wizard to configure API keys
kimi
# Then type: /setup
```

## Command Line Options

### Core Options
| Option | Short | Description | Default |
|--------|--------|-------------|---------|
| `--verbose` | | Print verbose information | `False` |
| `--debug` | | Enable debug logging | `False` |
| `--version` | | Show version and exit | |

### Agent Configuration
| Option | Short | Description | Default |
|--------|--------|-------------|---------|
| `--agent-file` | | Custom agent YAML file | Built-in default |
| `--model` | `-m` | LLM model to use | From config |

### Session Management
| Option | Short | Description | Default |
|--------|--------|-------------|---------|
| `--work-dir` | `-w` | Working directory | Current directory |
| `--continue` | `-C` | Continue previous session | `False` |

### UI Modes
| Option | Description | Default |
|--------|-------------|---------|
| `--ui` | Choose mode: `shell`, `print`, `acp` | `shell` |
| `--print` | Shortcut for `--ui print` | |
| `--acp` | Shortcut for `--ui acp` | |

### Command Execution
| Option | Short | Description | Default |
|--------|--------|-------------|---------|
| `--command` | `-c` | Execute command and exit | Interactive mode |
| `--query` | `-q` | Alias for `--command` | |

### Input/Output (Print Mode Only)
| Option | Description | Default |
|--------|-------------|---------|
| `--input-format` | Input format: `text`, `stream-json` | `text` |
| `--output-format` | Output format: `text`, `stream-json` | `text` |

### MCP Configuration
| Option | Description |
|--------|-------------|
| `--mcp-config-file` | Load MCP configs from JSON file (can be used multiple times) |
| `--mcp-config` | Load MCP configs from JSON string (can be used multiple times) |

### Action Approval
| Option | Short | Description | Default |
|--------|--------|-------------|---------|
| `--yolo` | `-y` | Auto-approve all actions | `False` |
| `--yes` | | Alias for `--yolo` | |
| `--auto-approve` | | Alias for `--yolo` | |

### Environment Variables
- `KIMI_MODEL_NAME`: Override model name
- `KIMI_API_KEY`: Override API key
- `KIMI_BASE_URL`: Override API base URL
- `KIMI_MODEL_MAX_CONTEXT_SIZE`: Override context size
- `OPENAI_API_KEY`: OpenAI provider API key
- `OPENAI_BASE_URL`: OpenAI provider base URL

## UI Modes

### Shell Mode (Default)
Interactive terminal interface with rich features:

```bash
# Start shell mode
kimi

# Or explicitly
kimi --ui shell
```

**Features:**
- Rich markdown rendering
- Interactive approval system
- Session history
- File autocompletion with `@`
- Meta-commands (`/help`, `/setup`, etc.)
- Image paste support (Ctrl-V)
- Dual mode: Agent (✨) and Shell ($)

### Print Mode
Non-interactive mode for scripting:

```bash
# Start print mode (auto-enables --yolo)
kimi --print

# Execute command and exit
kimi --print -c "show contents of README.md"

# Pipe input
echo "list Python files" | kimi --print
```

**Features:**
- Plain text output
- No approval prompts
- Suitable for automation
- JSON stream format support

### ACP Mode
Agent Client Protocol server:

```bash
# Start ACP server
kimi --acp
```

**Features:**
- JSON-RPC communication
- Tool streaming
- Permission-based execution
- IDE integration support

## Interactive Features

### Meta-Commands (Shell Mode)
Type `/` to see available commands:

| Command | Aliases | Description |
|---------|---------|-------------|
| `/help` | `h`, `?` | Show help information |
| `/version` | | Show version info |
| `/release-notes` | | Show release notes |
| `/feedback` | | Open GitHub issues |
| `/setup` | | Run setup wizard |
| `/reload` | | Reload configuration |
| `/init` | | Analyze codebase and generate AGENTS.md |
| `/clear` | `reset` | Clear conversation context |
| `/compact` | | Compact context for token management |
| `/debug` | | Show detailed context info |
| `/exit` | `quit` | Exit application |

### Keyboard Shortcuts
- `Ctrl-X`: Toggle between Agent/Shell mode
- `Ctrl-J` / `Alt-Enter`: Newline in multi-line input
- `Ctrl-V`: Paste text or images
- `Ctrl-D`: Exit
- `Tab`: Autocompletion
- `@`: File path completion

### Dual Mode System
- **Agent Mode** (✨): AI agent with full tool access
- **Shell Mode** ($): Direct shell command execution
- Toggle with `Ctrl-X`

## Available Tools

### File Operations
```python
# Read file with limits
ReadFile(path="/absolute/path/file.txt", line_offset=1, n_lines=100)

# Write or append to file
WriteFile(path="/absolute/path/file.txt", content="text", mode="overwrite")

# Search files
Glob(pattern="*.py", directory="/path", include_dirs=True)

# Search content
Grep(pattern="TODO.*", path="/path", type="py", output_mode="content", -n=True)

# Replace text
StrReplaceFile(path="/path/file.txt", edit={"old": "text", "new": "replacement"})

# Apply patch
PatchFile(path="/path/file.txt", diff="unified diff content")
```

### System Operations
```python
# Execute shell command
Bash(command="ls -la", timeout=60)

# Web search
SearchWeb(query="Python best practices", limit=5, include_content=True)

# Fetch web content
FetchURL(url="https://example.com")
```

### Task Management
```python
# Delegate to subagent
Task(description="Fix bug", subagent_name="coder", prompt="Detailed instructions")

# Manage todos
SetTodoList(todos=[{"title": "Task 1", "status": "Pending"}])

# Internal reasoning
Think(thought="Planning approach...")
```

### Tool Constraints
- **File operations**: Restricted to working directory
- **Bash commands**: No superuser privileges
- **Read limits**: 1000 lines, 2000 chars/line, 100KB total
- **Command timeout**: 5 minutes maximum
- **Approval required**: File writes, patches, bash commands

## Configuration

### Configuration File Location
```bash
~/.kimi/config.json
```

### Example Configuration
```json
{
  "default_model": "kimi-latest",
  "models": {
    "kimi-latest": {
      "provider": "kimi",
      "model": "kimi-latest",
      "max_context_size": 128000
    }
  },
  "providers": {
    "kimi": {
      "type": "kimi",
      "base_url": "https://api.kimi.moonshot.cn",
      "api_key": "your-api-key"
    }
  },
  "loop_control": {
    "max_steps_per_run": 100,
    "max_retries_per_step": 3
  },
  "services": {
    "moonshot_search": {
      "base_url": "https://search.example.com",
      "api_key": "search-api-key"
    }
  }
}
```

### Setup Wizard
```bash
# Run interactive setup
kimi
# Then type: /setup
```

## Agent System

### Built-in Agents
- **default**: General-purpose agent
- **sub**: Subagent for task delegation

### Agent Features
- YAML-based specifications
- System prompt templating
- Tool selection and exclusion
- Extension mechanism
- Subagent support

### System Prompt Variables
- `${KIMI_NOW}`: Current timestamp
- `${KIMI_WORK_DIR}`: Working directory
- `${KIMI_WORK_DIR_LS}`: Directory listing
- `${KIMI_AGENTS_MD}`: AGENTS.md content

## Custom Agents

### Basic Custom Agent
Create `my_agent.yaml`:
```yaml
version: 1
agent:
  name: "MyAgent"
  system_prompt_path: ./system.md
  tools:
    - "kimi_cli.tools.bash:Bash"
    - "kimi_cli.tools.file:ReadFile"
    - "kimi_cli.tools.web:SearchWeb"
```

### Extended Agent
```yaml
version: 1
agent:
  extend: "default"
  name: "ExtendedAgent"
  system_prompt_args:
    ROLE_ADDITIONAL: "You specialize in Python development."
  exclude_tools:
    - "kimi_cli.tools.task:Task"
```

### Using Custom Agents
```bash
# Use custom agent
kimi --agent-file my_agent.yaml

# With custom system prompt
kimi --agent-file my_agent.yaml -c "analyze this codebase"
```

### Subagents
Define subagents in your agent spec:
```yaml
subagents:
  coder:
    path: ./coder.yaml
    description: "Code analysis specialist"
  researcher:
    path: ./researcher.yaml
    description: "Web research specialist"
```

## Session Management

### Session Storage
```bash
~/.kimi/sessions/{work_dir_hash}/{session_id}.jsonl
```

### Session Commands
```bash
# Continue previous session
kimi --continue

# Start fresh session
kimi

# Session with specific directory
kimi -w /path/to/project --continue
```

### Session Features
- Per-working-directory isolation
- Automatic history replay
- Context compaction
- Checkpoint system

## Best Practices

### Safety
- Review all file operations before approval
- Use `--yolo` only for trusted automation
- Keep backups of important files
- Restrict working directory for safety

### Efficiency
- Use specific file patterns with Glob
- Limit search results with `head_limit`
- Use line offsets for large files
- Leverage subagents for complex tasks

### Organization
- Create custom agents for specific workflows
- Use todo management for complex projects
- Document your agents with clear system prompts
- Organize agent files in dedicated directories

### Troubleshooting
- Use `--debug` for detailed logging
- Check `~/.kimi/logs/kimi.log` for errors
- Use `/debug` meta-command for context info
- Verify configuration with `/setup`

## Troubleshooting

### Common Issues

**API Key Issues**
```bash
# Check configuration
kimi /setup

# Override with environment variable
KIMI_API_KEY="your-key" kimi
```

**Session Issues**
```bash
# Start fresh session
kimi

# Continue specific session
kimi --continue
```

**Tool Approval Issues**
```bash
# Auto-approve (use carefully)
kimi --yolo

# Or approve interactively
# Use arrow keys to navigate approval menus
```

**Configuration Issues**
```bash
# Reload configuration
kimi /reload

# Check debug logs
kimi --debug
```

### Getting Help
- Use `/help` in shell mode
- Check GitHub issues: `kimi /feedback`
- Review logs: `~/.kimi/logs/kimi.log`
- Community support through GitHub discussions

---

*This guide covers Kimi CLI version 0.27. For updates and additional features, check the release notes with `/release-notes`.*