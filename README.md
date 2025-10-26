# Claude Helpers

A collection of helpful commands, skills, and agents for Claude Code.

## Installation

To install this plugin, add it to your Claude Code plugins directory:

```bash
# For project-level installation
cd your-project
mkdir -p .claude/plugins
ln -s /Users/lasl321/code/claude-helpers .claude/plugins/claude-helpers

# For user-level installation
mkdir -p ~/.claude/plugins
ln -s /Users/lasl321/code/claude-helpers ~/.claude/plugins/claude-helpers
```

## Structure

```
claude-helpers/
├── .claude-plugin/
│   └── plugin.json         # Plugin metadata and configuration
├── commands/               # Custom slash commands
│   └── (add your .md files here)
├── agents/                 # Custom agent definitions
│   └── (add your .md files here)
├── skills/                 # Agent Skills
│   └── (add your skill folders here)
├── hooks/                  # Event handlers
│   └── hooks.json
└── README.md               # This file
```

## Usage

### Commands

Add custom slash commands by creating `.md` files in the `commands/` directory. Each file becomes a command:

```
commands/
└── example.md  # Creates /example command
```

### Skills

Create skills by adding folders with `SKILL.md` files in the `skills/` directory:

```
skills/
└── my-skill/
    └── SKILL.md
```

### Agents

Define custom agents by creating `.md` files in the `agents/` directory.

## Contributing

Add your custom helpers to the appropriate directories and update this README with usage instructions.

## Version

1.0.0
