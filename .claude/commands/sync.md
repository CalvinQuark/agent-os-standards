Sync the Agent OS standards from this repository to the active Agent OS installation directory.

First, delete all existing files in the target directory:
`C:\Users\CalvinCraig\source\repos\agent-os\profiles\default\standards\`

Then copy all standard files (backend/, frontend/, global/, testing/) to the target directory.

Use PowerShell commands:
1. Remove-Item to delete existing contents: `Remove-Item -Path "C:\Users\CalvinCraig\source\repos\agent-os\profiles\default\standards\*" -Recurse -Force`
2. Copy-Item to copy fresh standards: `Copy-Item -Path backend,frontend,global,testing -Destination "C:\Users\CalvinCraig\source\repos\agent-os\profiles\default\standards\" -Recurse -Force`

After syncing, confirm success by showing the user which directories were copied.
