## Database query best practices

- **Prevent SQL Injection**: Always use parameterized queries or ORM methods; never interpolate user input into SQL strings
- **Avoid N+1 Queries**: Use eager loading or joins to fetch related data in a single query instead of multiple queries
- **Select Only Needed Data**: Request only the columns you need rather than using SELECT * for better performance
- **Index Strategic Columns**: Index columns used in WHERE, JOIN, and ORDER BY clauses for query optimization
- **Use Transactions for Related Changes**: Wrap related database operations in transactions to maintain data consistency
- **Set Query Timeouts**: Implement timeouts to prevent runaway queries from impacting system performance
- **Cache Expensive Queries**: Cache results of complex or frequently-run queries when appropriate

### Entity Framework Core with Stored Procedures

- **Stored Procedure Access**: Use EF Core to interact with the database via Stored Procedures rather than accessing tables or views directly
- **Database-First Approach**: Follow Database-First development using SSDT (SDK-style) projects; define schema in SQL Server projects first
- **Procedure Mapping**: Use `FromSqlRaw` or `FromSqlInterpolated` with stored procedures for queries (e.g., `context.Customers.FromSqlRaw("EXEC dbo.GetCustomers")`)
- **Output Parameters**: Use `SqlParameter` with `Direction = ParameterDirection.Output` for stored procedures that return output parameters
- **Multiple Result Sets**: Use `DbDataReader` when stored procedures return multiple result sets
- **Parameterization**: Always pass parameters to stored procedures using `SqlParameter` objects to prevent SQL injection
- **Transaction Support**: Use `context.Database.BeginTransaction()` when calling multiple stored procedures that must execute as a unit
- **Return Values**: Capture stored procedure return values using `SqlParameter` with `Direction = ParameterDirection.ReturnValue`
- **Table-Valued Parameters**: Use table-valued parameters for bulk operations through stored procedures
- **Exception Handling**: Wrap stored procedure calls in try-catch blocks and handle SQL exceptions appropriately

### SQL Server T-SQL Standards

#### Casing Conventions
- **Reserved keywords**: UPPERCASE (e.g., SELECT, FROM, WHERE, JOIN, ORDER BY, CASE, WHEN, THEN, ELSE, END)
- **Built-in functions**: UPPERCASE (e.g., GETDATE, DATEDIFF, COUNT, SUM, AVG, MAX, MIN, NEWID)
- **Built-in data types**: UPPERCASE (e.g., INT, NVARCHAR, DATETIME, DECIMAL, BIT)
- **Text columns default**: All text columns must be declared as NVARCHAR unless explicitly instructed otherwise for a particular field
- **JOIN preference**: Use `JOIN` rather than `INNER JOIN` for inner joins
- **Object definitions**: Preserve original casing for user-defined objects (tables, columns, stored procedures, functions)

#### Common Table Expressions (CTEs)
- **CTE naming**: Name successive CTEs using lowercase letters in alphabetical order with `cte_` prefix (e.g., `cte_a`, `cte_b`, `cte_c`)
- **CTE structure**: Each CTE should be properly aligned and indented with clear formatting
- **CTE aliases**: Use single-letter aliases corresponding to the CTE name (e.g., `cte_a AS a`, `cte_b AS b`)
- **Sequential processing**: Whenever feasible, each subsequent CTE should reference the previous one when building upon results for clarity

#### Formatting and Style
- **Opening parentheses**: Place opening parenthesis on the same line, preceded by a space (e.g., `CREATE FUNCTION [dbo].[FunctionName] (`)
- **Parenthesis style**: Expanded to statement with indented contents for readability
- **Short statements**: Collapse statements shorter than 75 characters to a single line
- **Short subqueries**: Collapse subqueries shorter than 75 characters to a single line
- **Maximum line length**: 300 characters before wrapping

#### JOIN Statements
- **JOIN keyword placement**: Place JOIN keyword on new line
- **JOIN keyword alignment**: Align JOIN to FROM keyword
- **ON keyword**: Place on same line as JOIN table, indented
- **ON condition**: Place on same line as ON keyword, aligned to ON keyword

#### INSERT Statements
- **Column lists**: For shorter-width lists, place on same line; for wider lists with more columns, place on separate lines
- **VALUES clause**: Use compact indented parenthesis style with indented contents
- **Multiple value sets**: Each value set on separate lines with consistent indentation

#### CASE Expressions
- **First WHEN placement**: Always place on new line
- **WHEN alignment**: Indented from CASE
- **THEN placement**: Place THEN on new line
- **Expression alignment**: Indented from WHEN
- **ELSE placement**: Place ELSE on new line, aligned to WHEN
- **END placement**: Place END on new line, aligned to CASE
- **Short CASE expressions**: Collapse expressions shorter than 75 characters to single line

#### Operators and Conditions
- **Comparison operators**: Do not align them
- **AND/OR operators**: Right-aligned for visual hierarchy
- **BETWEEN**: Do not place on new line
- **IN clause**: Keep values on same line unless very long

#### Variables and Control Flow
- **Variable declaration**: Place equals sign on same line as variable declarations (e.g., `DECLARE @CustomerId INT = 123;`)
- **Short control flow**: Collapse IF statements shorter than 78 characters to single line
- **BEGIN/END blocks**: Use for multi-line IF/ELSE blocks with proper indentation

#### Comments
- **Comment alignment**: Align comments with related code elements for better readability
- **Inline comments**: Use `--` for single-line comments
- **Block comments**: Use `/* */` for multi-line comments
