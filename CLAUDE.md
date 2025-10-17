# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Repository Purpose

This repository contains **Agent OS standards** - markdown files that define coding conventions, architectural patterns, and best practices for AI-driven development. These standards are compiled into Agent OS profiles and guide how AI agents generate code across all projects using those profiles.

## Architecture

The repository is organized into four categories of standards:

- **backend/**: API design, database migrations, data models, and query patterns
- **frontend/**: Accessibility, component design, CSS conventions, responsive design
- **global/**: Cross-cutting concerns like coding style, commenting, conventions, error handling, tech stack definitions, and validation
- **testing/**: Test writing standards and patterns

Each `.md` file contains specific guidelines that AI agents will follow when generating code in those domains.

## Critical Workflow: Two-Way Sync

**This repository is the source of truth**, but changes must be synced to the active Agent OS installation:

1. **Edit standards here** (in this repo)
2. **Commit and push** to GitHub
3. **Sync to Agent OS** using the `/sync` slash command, or manually:
   ```powershell
   Copy-Item -Path backend,frontend,global,testing -Destination "C:\Users\CalvinCraig\agent-os\profiles\default\standards\" -Recurse -Force
   ```

**Never edit files directly** in `C:\Users\CalvinCraig\agent-os\profiles\default\standards\` - they will be overwritten.

## Custom Slash Commands

- `/sync` - Sync standards from this repository to the Agent OS installation directory

## Making Changes to Standards

When modifying standards files:

1. **Understand the impact**: Changes here affect code generation across all projects using this Agent OS profile
2. **Be specific**: Standards should be actionable directives, not vague suggestions
3. **Use bullet points**: Keep standards as bulleted lists for easy parsing by AI agents
4. **Think holistically**: Consider how changes in one standard file might interact with others

## File Format

All standard files follow this pattern:
- Start with a `##` heading describing the standard category
- Use bullet points starting with bold labels (e.g., `**RESTful Design**:`)
- Keep descriptions concise but clear
- Include examples in brackets where helpful (e.g., `[e.g., React, Vue, Svelte]`)

## Editing Permissions

- **Markdown files**: Claude Code is authorized to edit any `.md` file in this repository without asking permission
- **Rationale**: Standards files are frequently refined during AI-assisted development sessions; requiring permission for each edit slows iteration

## Environment

- **OS**: Windows
- **Shell**: PowerShell (use PowerShell commands in documentation)
- **Git Branch**: `master` (not `main`)
- **Remote**: `origin`
