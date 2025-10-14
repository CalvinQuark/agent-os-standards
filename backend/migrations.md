## Database Schema Management

### SSDT/DACPAC Deployment
- **Declarative Model**: Define desired end-state in database project; deployment tools calculate necessary changes
- **Build Output**: Build produces DACPAC (Data-tier Application Package) file
- **Deployment Safety**: Review deployment script before applying to production
- **Backup First**: Always backup production database before schema deployment

### Schema Change Workflow
- **Modify Objects**: Edit SQL files in SSDT project to reflect desired schema
- **Build Project**: Run `dotnet build` to validate syntax and produce DACPAC
- **Generate Script**: Generate deployment script and review for safety
- **Test Deployment**: Deploy to test/staging environment first
- **Production Deployment**: Apply to production after validation

### Pre/Post Deployment Scripts
- **Pre-Deployment**: Use for setup tasks (e.g., disabling constraints temporarily)
- **Post-Deployment**: Use for data migrations, reference data updates, or cleanup
- **Script Location**: Store in project root or Scripts folder
- **Idempotency**: Ensure scripts can be run multiple times safely

### Deployment Best Practices
- **Review Generated SQL**: Always review generated deployment script before execution
- **Data Loss Prevention**: Check for operations that may cause data loss (column drops, type changes)
- **Backup Strategy**: Maintain current backups before any schema changes
- **Rollback Plan**: Have rollback DACPAC or script ready
- **Publish Profiles**: Use publish profiles for environment-specific settings
- **Version Control**: Commit all schema changes to source control

### High-Availability Considerations
- **Large Table Changes**: Test impact on large tables in non-production first
- **Index Creation**: Use ONLINE index creation when possible to minimize blocking
- **Minimize Downtime**: Consider multi-phase deployments for breaking changes
- **Communication**: Notify stakeholders of deployment windows and potential impact
