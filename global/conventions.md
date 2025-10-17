## General development conventions

- **Consistent Project Structure**: Organize files and directories in a predictable, logical structure that team members can navigate easily
- **Clear Documentation**: Maintain up-to-date README files with setup instructions, architecture overview, and contribution guidelines
- **Version Control Best Practices**: Use clear commit messages, feature branches, and meaningful pull/merge requests with descriptions
- **Environment Configuration**: Use environment variables for configuration; never commit secrets or API keys to version control. For .NET projects, store local development secrets in User Secrets cache (not environment variables)
- **Dependency Management**: Keep dependencies up-to-date and minimal; document why major dependencies are used
- **Code Review Process**: Establish a consistent code review process with clear expectations for reviewers and authors
- **Testing Requirements**: Define what level of testing is required before merging (unit tests, integration tests, etc.)
- **Feature Flags**: Use feature flags for incomplete features rather than long-lived feature branches
- **Changelog Maintenance**: Keep a changelog or release notes to track significant changes and improvements

### C# Project Conventions

- **Namespace organization**: Use namespace structure that mirrors folder structure for consistency
- **File naming**: Name files to match the primary class/interface they contain (e.g., `CustomerOrderProcessor.cs`)
- **One class per file**: Generally maintain one public class or interface per file for better organization and discoverability
- **Project structure**: Organize code into logical folders (e.g., Models, Services, Controllers, Utilities)
- **EditorConfig usage**: Use `.editorconfig` files to enforce consistent formatting across team members and IDEs
- **Async naming**: Suffix asynchronous methods with `Async` (e.g., `ProcessOrderAsync`, `GetCustomerDataAsync`)
- **Interface naming**: Prefix interface names with `I` (e.g., `IOrderProcessor`, `ICustomerRepository`)
- **Configuration files**: Use `appsettings.json` for configuration with environment-specific overrides (e.g., `appsettings.Development.json`)
- **Secret management**: Store local development secrets in User Secrets cache using `dotnet user-secrets` CLI or Visual Studio. Never use environment variables for sensitive data in .NET projects. Access secrets through `IConfiguration` like other config values
- **Dependency injection**: Prefer constructor injection for dependencies and register services in `Program.cs` or startup configuration
