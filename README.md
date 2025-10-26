# Claude Helpers

A collection of helpful commands, skills, and agents for Claude Code that streamline development workflows, particularly for Git and GitHub operations.

## Overview

This repository provides a plugin system for Claude Code with specialized agents and slash commands that automate common development tasks like creating commits and pull requests with proper formatting and conventions.

## Installation

### Prerequisites

- Claude Code CLI installed
- Git configured
- GitHub CLI (`gh`) installed and authenticated (for PR creation)

### Setup

Install this plugin by symlinking it to your Claude Code plugins directory:

```bash
# For project-level installation
cd your-project
mkdir -p .claude/plugins
ln -s /path/to/claude-helpers .claude/plugins/claude-helpers

# For user-level installation
mkdir -p ~/.claude/plugins
ln -s /path/to/claude-helpers ~/.claude/plugins/claude-helpers
```

## Repository Structure

```
claude-helpers/
├── .claude-plugin/
│   └── marketplace.json              # Plugin registry configuration
├── plugins/
│   └── development-workflows/        # Development workflow automation plugin
│       ├── .claude-plugin/
│       │   └── plugin.json          # Plugin metadata
│       ├── commands/                # Slash commands
│       │   ├── commit.md           # /development-workflows:commit
│       │   └── pr.md               # /development-workflows:pr
│       ├── agents/                 # Agent definitions
│       │   ├── git-commit-creator.md
│       │   └── pr-creator.md
│       └── hooks/
│           └── hooks.json          # Event handlers
└── README.md
```

## Features

### 1. Development Workflows Plugin

A comprehensive plugin for Git and GitHub workflows with intelligent automation.

#### Slash Commands

##### `/development-workflows:commit`

Creates a Git commit with Conventional Commit conventions.

**Usage:**
```
/development-workflows:commit
```

**Features:**
- Automatically analyzes staged and unstaged changes
- Generates descriptive commit messages following Conventional Commits format
- Reviews recent commit history to match repository style
- Handles git operations intelligently

##### `/development-workflows:pr`

Creates a GitHub pull request with comprehensive documentation.

**Usage:**
```
/development-workflows:pr
```

**Features:**
- Analyzes branch history and changes
- Uses repository PR templates if available
- Generates comprehensive PR descriptions with summary and test plan
- Automatically pushes branch to remote if needed
- Links related issues and commits
- Returns PR URL for easy access

#### Agents

##### `git-commit-creator`

An expert Git workflow agent that creates well-structured commits with proper conventions.

**Capabilities:**
- Protected branch detection (won't commit to `develop` or `master`)
- Automatic feature branch creation with intelligent naming
- Conventional Commit message generation (feat, fix, docs, etc.)
- Scope detection and appropriate commit type selection
- Thorough change analysis before committing

**Branch Naming Convention:**
- Format: `features/descriptive-name-here`
- Automatically generated based on change analysis
- Uses kebab-case, 2-4 words

**Commit Message Format:**
```
<type>(<scope>): <description>

[optional body]
```

**Example commits:**
- `feat(auth): add JWT token validation`
- `fix(api): resolve null pointer exception in user service`
- `chore(terraform): update provider versions to latest`

##### `pr-creator`

An expert GitHub specialist that creates informative, well-structured pull requests.

**Capabilities:**
- Repository and branch analysis
- Automatic build verification (runs `npm run build` if package.json exists)
- Proof generation (runs `npm run proof` and includes output in PR)
- PR template detection and usage
- Comprehensive PR descriptions with summary, changes, and testing info
- Automatic branch pushing to remote
- Handles existing PR scenarios (adds proof as comment)

**PR Structure:**
- Clear, descriptive title
- Summary of changes and rationale
- Bulleted list of specific modifications
- Testing instructions
- Proof section (when applicable)
- Links to related issues

## Configuration

### Plugin Metadata

The plugin system uses metadata files to configure behavior:

**marketplace.json** (repository root):
- Defines plugin registry
- Specifies plugin locations
- Sets version and ownership

**plugin.json** (per plugin):
- Plugin name and description
- Version information
- Author details
- Keywords for discovery

## Usage Examples

### Creating a Commit

```
User: I've finished implementing authentication. Can you commit these changes?
Claude: [Launches git-commit-creator agent]
       - Checks current branch (creates feature branch if on develop/master)
       - Analyzes changes
       - Stages files
       - Creates commit: "feat(auth): implement JWT authentication system"
```

### Creating a Pull Request

```
User: Let's create a PR for this feature
Claude: [Launches pr-creator agent]
       - Verifies all changes are committed
       - Runs build and proof scripts
       - Generates comprehensive PR description
       - Pushes branch and creates PR
       - Returns PR URL
```

## Best Practices

1. **Commit Frequently**: Use the commit command after completing logical units of work
2. **Protected Branches**: The agents automatically protect `develop` and `master` branches
3. **PR Templates**: Add a `.github/pull-request-template.md` for consistent PR structure
4. **Conventional Commits**: Follow the generated commit message patterns for consistency
5. **Build Verification**: Ensure your `package.json` includes `build` and `proof` scripts if applicable

## Development

### Adding New Commands

Create a `.md` file in `plugins/<plugin-name>/commands/`:

```markdown
---
description: Command description
tags:
  - tag1
  - tag2
---

Command instructions here...
```

### Adding New Agents

Create a `.md` file in `plugins/<plugin-name>/agents/`:

```markdown
---
name: agent-name
description: Agent description with usage examples
tools: Tool1, Tool2, Tool3
model: opus
color: blue
---

Agent system prompt and instructions...
```

## Requirements

- Claude Code CLI
- Git 2.0+
- GitHub CLI (gh) for PR operations
- Node.js (if using build/proof scripts)

## License

UNLICENSED

## Author

Luis Sotomayor (luis.sotomayor@gmail.com)

## Version

1.0.0
