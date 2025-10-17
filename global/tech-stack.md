## Tech stack

Define your technical stack below. This serves as a reference for all team members and helps maintain consistency across the project.

### Framework & Runtime
- **Language/Runtime:** C# / .NET
- **Target Framework:** .NET 9.0 or later
- **Package Manager:** NuGet

### Frontend
- **Framework:** Blazor (Server and WebAssembly)
- **UI Components:** Fluent UI Blazor components
- **JavaScript:** Vanilla JS (minimal usage; prefer Blazor C# for interactivity)
- **CSS Framework:** [e.g., custom CSS, Fluent UI theming]

### Database & Storage
- **Database:** SQL Server (localhost deployment)
- **Database Projects:** SDK-style SSDT projects in Visual Studio Code
- **Database Extensions:** SQL Database Projects, SQL Server (mssql)
- **Development Approach:** Database-First development using SSDT projects
- **ORM:** Entity Framework Core
  - Interact with database via Stored Procedures rather than accessing tables or views directly
  - Use EF Core to map and execute stored procedures for all CRUD operations
- **Unit Testing:** tSQLt framework in `[DatabaseName]Tests` databases
- **Caching:** IMemoryCache (ASP.NET Core in-memory), SQL Server query result caching

### Testing & Quality
- **Unit Test Framework:** xUnit
- **Component Testing:** bUnit (for Blazor components)
- **End-to-End Testing:** Playwright for .NET
  - Write tests in C# rather than TypeScript
  - Test across Chromium, Firefox, and WebKit
- **Database Testing:** tSQLt framework
- **Linting/Formatting:** EditorConfig, .NET analyzers
- **Code Analysis:** Roslyn analyzers

### Deployment & Infrastructure
- **Hosting:** Local hosting by default; when specifically instructed, may use Azure Storage Account static websites, Azure Static Web Apps, or Azure Web Apps (non-static)
- **CI/CD:** GitHub Actions

### Third-Party Services
- **Authentication:** Microsoft Entra ID (most sites), ASP.NET Core Identity (if specified)
- **Email:** Azure Communication Services
- **Monitoring:** Azure Application Insights
