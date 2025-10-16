## Database Schema Design Best Practices

- **Clear Naming**: Use singular names for columns and plural names for tables following your framework's conventions
- **Timestamps**: Include created and updated timestamps on all tables for auditing and debugging
- **Data Integrity**: Use database constraints (NOT NULL, UNIQUE, foreign keys) to enforce data rules at the database level
- **Appropriate Data Types**: Choose data types that match the data's purpose and size requirements
- **Indexes on Foreign Keys**: Index foreign key columns and other frequently queried fields for performance
- **Validation at Multiple Layers**: Implement validation at both model and database levels for defense in depth
- **Relationship Clarity**: Define relationships clearly with appropriate cascade behaviors and naming conventions
- **Avoid Over-Normalization**: Balance normalization with practical query performance needs

### SQL Server Table Design Standards

#### Primary Keys
- **Standard primary key**: All tables including join tables should use `Id INT IDENTITY(1,1) PRIMARY KEY` as their primary key
- **Business key constraints**: If there is another ID field (e.g., `OrderId`, `CustomerId`), it should get a uniqueness constraint with `UNIQUE`
- **Primary key naming**: Name primary key constraints using pattern `PK_TableName` (e.g., `CONSTRAINT PK_Orders PRIMARY KEY`)

#### Column Definitions
- **Data type alignment**: Align data types vertically for readability in CREATE TABLE statements
- **Text columns**: All text columns must be declared as NVARCHAR unless explicitly instructed otherwise for a particular field
- **Constraint placement**: Place constraints on the same line as the column definition for better organization
- **Null handling**: Explicitly specify NOT NULL or NULL for each column to make nullability clear
- **Default values**: Use DEFAULT constraint for columns that should have default values (e.g., `OrderDate DATETIME DEFAULT GETDATE()`)

#### Constraints
- **Named constraints**: Always name constraints explicitly for easier management and debugging
- **Constraint naming conventions**:
  - Primary keys: `PK_TableName`
  - Unique constraints: `UQ_TableName_ColumnName`
  - Foreign keys: `FK_TableName_ReferencedTable`
  - Check constraints: `CHK_TableName_ColumnName_Description`
  - Default constraints: `DF_TableName_ColumnName`
- **Constraint columns**: Place constraint column references on same line if short, or new line if longer or multiple columns
- **Foreign key references**: Fully specify foreign key references including the referenced table and column
- **Check constraints**: Use check constraints to enforce business rules at the database level (e.g., positive amounts, valid status values)

#### Table Structure
- **Schema specification**: Always specify schema (e.g., `dbo.TableName`, `[SchemaName].[TableName]`)
- **Bracket usage**: Use brackets for object names when they contain spaces or special characters, or for consistency
- **Column ordering**: Order columns logically - typically: Id, business keys, required fields, optional fields, timestamps
- **Audit columns**: Consider including standard audit columns (e.g., `CreatedDate`, `CreatedBy`, `ModifiedDate`, `ModifiedBy`)

#### Indexes
- **Index naming**: Use descriptive names like `IX_TableName_ColumnName` or `IX_TableName_Column1_Column2`
- **Clustered indexes**: Primary key is typically the clustered index; choose carefully if using a different clustered index
- **Non-clustered indexes**: Create non-clustered indexes on foreign keys and frequently queried columns
- **Covering indexes**: Consider covering indexes with INCLUDE clause for frequently accessed columns in queries

#### Schema Organization
- **Logical schemas**: Use schemas to organize related tables (e.g., `Sales`, `HR`, `Inventory`)
- **Default schema**: Use `dbo` schema when no specific schema is needed
- **Schema permissions**: Consider security implications when designing schema structure

### SSDT Project-Specific Guidelines

#### Temporal Tables
- **System-Versioning**: Use SQL Server temporal tables for tables requiring audit history
- **Column Requirements**: Include `ValidFrom DATETIME2 GENERATED ALWAYS AS ROW START` and `ValidTo DATETIME2 GENERATED ALWAYS AS ROW END`
- **Period Definition**: Add `PERIOD FOR SYSTEM_TIME (ValidFrom, ValidTo)`
- **History Table**: Specify history table with `SYSTEM_VERSIONING = ON (HISTORY_TABLE = [schema].[TableName_History])`

#### Table-Valued Types
- **Bulk Operations**: Define table-valued types for bulk insert/update operations
- **Type Naming**: Use `*TableType` suffix (e.g., `AccountTransactionsTableType`)
- **Column Matching**: Type structure should match target table structure for relevant columns
- **Performance**: Prefer table-valued parameters over XML or JSON for bulk operations

#### Transaction Patterns
- **Deduplication**: Use EXCEPT operator for deduplication in bulk insert procedures
- **Error Handling**: Include TRY/CATCH blocks in stored procedures with appropriate error handling
- **Transaction Scope**: Explicitly define transaction boundaries in stored procedures
