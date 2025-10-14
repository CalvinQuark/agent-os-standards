## SQL Server Database Tools (SSDT) Project Standards

### Project Structure
- **Project Type**: SDK-style SQL Server Database Projects
- **Development Environment**: Visual Studio Code with SQL Database Projects and SQL Server (mssql) extensions
- **Development Approach**: Database-first development
- **Target Platform**: SQL Server 2022 (compatibility level 160)
- **Deployment Target**: localhost with Integrated Security

### Object Organization
- **Folder structure**: Organize by schema, then object type
  ```
  dbo/
  ├── Tables/
  ├── StoredProcedures/
  ├── Functions/
  ├── Views/
  └── UserDefinedTypes/
  ```

### Naming Conventions
- **Stored Procedures**: `p_` prefix (e.g., `p_InsertAccountTransactions`)
- **Table-Valued Functions**: `tvf_` prefix (e.g., `tvf_AccountTransaction`)
- **Scalar Functions**: `f_` prefix (e.g., `f_IsActiveAccount`)
- **Table Types**: `*TableType` suffix (e.g., `AccountTransactionsTableType`)
- **Primary Keys**: `PK_TableName`
- **Foreign Keys**: `FK_TableName_ReferencedTable`
- **Unique Constraints**: `UQ_TableName_ColumnName`
- **Check Constraints**: `CHK_TableName_ColumnName_Description`
- **Default Constraints**: `DF_TableName_ColumnName`

### Build and Deployment
- **Build Command**: `dotnet build` produces DACPAC in `bin/Debug/`
- **Publish Profile**: Use `localhost.publish.xml` for local deployment
- **Database Creation**: Create test database before first deployment

### Code Documentation
- **Stored Procedures**: Include usage examples in comments
- **Complex Functions**: Document parameters and return values
- **Business Logic**: Comment non-obvious business rules

### SQL Server Features
- **Temporal Tables**: Use SQL Server temporal tables for audit history where appropriate
- **Table-Valued Parameters**: Use for bulk operations instead of multiple single-row operations
- **System-Versioning**: Leverage SYSTEM_TIME for historical data tracking
