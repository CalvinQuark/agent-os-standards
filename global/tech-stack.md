## Tech stack

Define your technical stack below. This serves as a reference for all team members and helps maintain consistency across the project.

### Framework & Runtime
- **Language/Runtime:** C# / .NET
- **Target Framework:** .NET 8.0 or later
- **Package Manager:** NuGet

### Frontend
- **JavaScript Framework:** [e.g., React, Vue, Svelte, Alpine, vanilla JS]
- **CSS Framework:** [e.g., Tailwind CSS, Bootstrap, custom]
- **UI Components:** [e.g., shadcn/ui, Material UI, custom library]

### Database & Storage
- **Database:** SQL Server (localhost deployment)
- **Database Projects:** SDK-style SSDT projects in Visual Studio Code
- **Database Extensions:** SQL Database Projects, SQL Server (mssql)
- **Query Tools:** ADO.NET for data access, optional Dapper for simple queries
- **Unit Testing:** tSQLt framework in `[DatabaseName]Tests` databases
- **ORM:** Entity Framework Core (when applicable)
- **Caching:** [e.g., Redis, MemoryCache, SQL Server in-memory tables]

### Testing & Quality
- **Test Framework:** xUnit, NUnit, or MSTest
- **Linting/Formatting:** EditorConfig, .NET analyzers
- **Code Analysis:** Roslyn analyzers

### Deployment & Infrastructure
- **Hosting:** [e.g., Azure, AWS, on-premises]
- **CI/CD:** [e.g., GitHub Actions, Azure DevOps, Jenkins]

### Third-Party Services
- **Authentication:** [e.g., ASP.NET Core Identity, Azure AD, Auth0]
- **Email:** [e.g., SendGrid, Azure Communication Services]
- **Monitoring:** [e.g., Application Insights, Sentry, Datadog]
