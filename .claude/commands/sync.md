Sync the Agent OS standards from this repository to the active Agent OS installation directory.

Copy all standard files (backend/, frontend/, global/, testing/) to:
`C:\Users\CalvinCraig\source\repos\agent-os\profiles\default\standards\`

Use PowerShell's Copy-Item cmdlet with -Recurse and -Force flags to overwrite existing files.

After syncing, confirm success by showing the user which directories were copied.
