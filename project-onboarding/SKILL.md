---
name: project-onboarding
description: Explore and understand unfamiliar codebases by analyzing project structure, components, and entry points. Use when starting work on a new project, joining a codebase, or when the user asks to understand a project's architecture or where to begin.
---

# Project Onboarding

Help users quickly understand a new codebase by providing a structured overview of the project architecture, key components, and recommended starting points.

## Workflow

### Step 1: Identify Project Type

Examine the root directory for key indicators:

| File | Project Type |
|------|--------------|
| `package.json` | Node.js / JavaScript / TypeScript |
| `Cargo.toml` | Rust |
| `go.mod` | Go |
| `pyproject.toml`, `setup.py`, `requirements.txt` | Python |
| `pom.xml`, `build.gradle` | Java |
| `*.sln`, `*.csproj` | .NET |
| `flake.nix`, `default.nix` | Nix |

Also look for:
- `README.md` - Project description and setup instructions
- `AGENTS.md`, `CLAUDE.md`, `CURSOR.md` - AI agent guidelines
- `CONTRIBUTING.md` - Contribution guidelines
- `.env.example` - Environment configuration hints

### Step 2: Analyze Project Structure

Use the explore subagent or file listing to map the directory structure. Identify:

1. **Source directories**: `src/`, `lib/`, `app/`, `packages/`
2. **Test directories**: `test/`, `tests/`, `__tests__/`, `spec/`
3. **Config files**: Build configs, linter configs, CI/CD workflows
4. **Documentation**: `docs/`, `README.md`, inline documentation
5. **Infrastructure**: `infra/`, `deploy/`, `docker/`, `.github/`

### Step 3: Identify Key Components

For each major directory or module, determine:

- **Purpose**: What does this component do?
- **Dependencies**: What does it depend on? What depends on it?
- **Entry points**: Main files, exported APIs, CLI commands

### Step 4: Generate Overview Report

Present findings in this format:

```markdown
# Project Overview: [Project Name]

## Summary
[1-2 sentence description of what this project does]

## Tech Stack
- Language: [Primary language]
- Framework: [If applicable]
- Build tool: [Build system]
- Package manager: [npm/yarn/bun/pip/cargo/etc.]

## Project Structure

### Core Components

#### `[directory/]`
**Purpose**: [What this component does]
**Key files**:
- `file.ts` - [Brief description]
- `other.ts` - [Brief description]

[Repeat for each major component]

### Supporting Infrastructure
- `[config file]` - [Purpose]
- `[CI workflow]` - [Purpose]

## Where to Start

### 1. Read First
- `README.md` - Project overview and setup
- `[main entry point]` - Application entry point
- `[key config]` - Configuration understanding

### 2. Core Logic
- `[primary source file]` - [Why this is important]
- `[key module]` - [Why this is important]

### 3. Examples/Tests
- `[example or test file]` - See how the code is used

## Architecture Notes
[Any important architectural patterns, conventions, or decisions observed]
```

## Tips for Different Project Types

### Monorepos
- Check for `packages/`, `apps/`, or workspace configuration
- Identify shared libraries vs applications
- Look for root-level scripts that orchestrate builds

### Web Applications
- Identify frontend vs backend separation
- Look for routing configuration
- Find API endpoints or handlers

### CLI Tools
- Find the main command entry point
- Look for subcommand definitions
- Identify configuration parsing

### Libraries
- Focus on the public API surface
- Find exported types/functions
- Look for usage examples

## Example Questions to Answer

When onboarding, aim to answer:

1. What does this project do?
2. How do I run it locally?
3. Where is the main entry point?
4. How is the code organized?
5. What are the key abstractions?
6. Where should I make changes for [common task]?
