# Agent OS Standards - Custom Configuration

This repository contains customized Agent OS standards for personal development projects. These standards define coding conventions, architectural patterns, and best practices that AI agents will use when generating code.

## Purpose

- **Version Control**: Track changes to Agent OS standards separately from the base installation
- **Customization**: Maintain personalized coding conventions and preferences
- **Synchronization**: Keep custom standards in sync with the active Agent OS profile

## Repository Structure

```
agent-os-standards/
├── backend/           # Backend-related standards
│   ├── api.md
│   ├── migrations.md
│   ├── models.md
│   └── queries.md
├── frontend/          # Frontend-related standards
│   ├── accessibility.md
│   ├── components.md
│   ├── css.md
│   └── responsive.md
├── global/            # Global coding standards
│   ├── coding-style.md
│   ├── commenting.md
│   ├── conventions.md
│   ├── error-handling.md
│   ├── tech-stack.md
│   └── validation.md
└── testing/           # Testing standards
    └── test-writing.md
```

## Workflow

### Making Changes

1. **Edit standards in this repository**
   ```powershell
   cd C:\Users\CalvinCraig\source\repos\agent-os-standards
   # Edit the relevant .md files
   ```

2. **Commit your changes**
   ```powershell
   git add .
   git commit -m "Description of changes"
   ```

3. **Push to GitHub**
   ```powershell
   git push origin main
   ```

4. **Sync to Agent OS installation**

   Using Claude Code slash command:
   ```
   /sync
   ```

   Or manually with PowerShell:
   ```powershell
   Copy-Item -Path backend,frontend,global,testing -Destination "C:\Users\CalvinCraig\agent-os\profiles\default\standards\" -Recurse -Force
   ```

### Important Notes

- **Source of Truth**: This repository is the authoritative source for your custom standards
- **Do NOT edit directly**: Never modify files in `C:\Users\CalvinCraig\agent-os\profiles\default\standards\` directly
- **Always sync**: After committing changes here, copy them back to the Agent OS installation directory
- **Backup**: GitHub serves as a backup and history of all standard modifications

## Initial Setup

This repository was created from the default Agent OS standards located at:
```
C:\Users\CalvinCraig\agent-os\profiles\default\standards
```

The baseline configuration represents the Agent OS defaults, which can now be customized to match personal preferences and project requirements.

## References

- [Agent OS Installation Guide](https://buildermethods.com/agent-os/installation)
- [Agent OS Documentation](https://buildermethods.com/agent-os/)
