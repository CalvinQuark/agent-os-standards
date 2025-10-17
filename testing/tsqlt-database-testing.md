## tSQLt Database Testing Standards

### Test Database Organization
- **Test Database Naming**: Suffix production database name with `Tests` (e.g., `Northwind` → `NorthwindTests`)
- **Test Database Location**: localhost
- **Framework**: tSQLt framework for SQL Server unit testing
- **Isolation**: Each test should be independent and not affect other tests

### Test Structure
- **Test Classes**: Organize tests into test classes matching schema or functional areas
- **Test Naming**: Use descriptive names starting with propercase `Test` prefix, utilizing spaces for readability
- **Artifact Delimiters**: Use backticks to delimit artifact names (procedures, functions, variables, tables, etc.)
- **Setup/Teardown**: Use tSQLt.FakeTable and tSQLt.SpyProcedure for test isolation
- **Assertions**: Use tSQLt assertion procedures (AssertEquals, AssertNotEquals, AssertEmptyTable, etc.)

### Test Organization
- **Schema-based**: Create test classes per schema (e.g., `[TestsDbo]`, `[TestsSales]`)
- **Feature-based**: Or organize by feature/functionality when it makes more sense
- **Test Independence**: Each test must be self-contained with its own setup and cleanup

### Code Style and Formatting
- **SQL Keywords**: Use UPPERCASE for all SQL keywords (SELECT, FROM, WHERE, etc.)
- **Built-in Functions**: Use UPPERCASE (GETDATE, COUNT, SUM, etc.)
- **Data Types**: Use UPPERCASE for built-in data types (INT, NVARCHAR, DATETIME)
- **Text Columns**: Use NVARCHAR for all text columns unless explicitly specified otherwise
- **Variable Naming**: Use PascalCase with @ prefix (e.g., `@CustomerId`, `@ExpectedResult`)
- **Opening Braces**: Place opening braces on same line with preceding space
- **Line Length**: Maximum 300 characters before wrapping
- **Short Statements**: Collapse statements shorter than 75 characters to single line
**Authentication:**
### Test Naming Conventions
- **Pattern**: `Test that [description with backtick-delimited artifacts]`
- **Examples**:
  - “Test that `CalculateDiscount` returns 15 percent for premium customers”
  - “Test that `ValidateOrder` throws exception when `@CustomerId` is NULL”
  - “Test that `ProcessPayment` raises error when funds are insufficient”
  - “Test that `SalesReport` calls `HistoricalReport` when `@showHistory = 1`”

### What to Test
- **Stored Procedures**: Test business logic, data transformation, and edge cases
- **Functions**: Test calculations, data formatting, and return values
- **Triggers**: Test trigger firing conditions and resulting data changes
- **Constraints**: Verify that constraints properly enforce business rules
- **Views**: Test complex views return expected result sets

### Testing Patterns
- **Arrange-Act-Assert**: Follow AAA pattern in all tests with clear comments
- **Variable Declaration**: Declare variables with explicit values using equals sign on same line
- **Error Testing**: Use tSQLt.ExpectException for testing error conditions
- **Assertion Messages**: Provide meaningful custom messages for assertions

```sql
CREATE PROCEDURE [TestsDbo].[Test that `CalculateOrderTotal` returns correct sum for valid items]
AS
BEGIN
    -- Arrange
    DECLARE @CustomerId INT = 123;
    DECLARE @ExpectedTotal DECIMAL(18, 2) = 150.00;
    
    EXEC tSQLt.FakeTable 'dbo', 'Orders';
    EXEC tSQLt.FakeTable 'dbo', 'OrderItems';
    
    INSERT INTO dbo.Orders (Id, CustomerId, OrderDate, Status)
    VALUES (1, @CustomerId, GETDATE(), N'Pending');
    
    INSERT INTO dbo.OrderItems (OrderId, ProductId, Quantity, UnitPrice)
    VALUES (1, 101, 2, 50.00),
           (1, 102, 1, 50.00);

    -- Act
    DECLARE @ActualTotal DECIMAL(18, 2);
    EXEC @ActualTotal = dbo.f_CalculateOrderTotal @OrderId = 1;

    -- Assert
    EXEC tSQLt.AssertEquals 
        @Expected = @ExpectedTotal,
        @Actual = @ActualTotal,
        @Message = N'Order total calculation should sum all item quantities * unit prices';
END;
```

### Exception Testing Pattern
```sql
CREATE PROCEDURE [TestsDbo].[Test that `ProcessPayment` throws ArgumentException when `@CustomerId` is NULL]
AS
BEGIN
    -- Arrange
    DECLARE @CustomerId INT = NULL;
    DECLARE @Amount DECIMAL(18, 2) = 100.00;
    
    EXEC tSQLt.ExpectException 
        @ExpectedMessagePattern = N'%Customer ID cannot be NULL%',
        @ExpectedSeverity = 16;

    -- Act
    EXEC dbo.p_ProcessPayment @CustomerId = @CustomerId, @Amount = @Amount;

    -- Assert handled by ExpectException
END;
```

### Data Setup Patterns
- **Fake Tables**: Create fake tables for all dependencies using consistent patterns
- **Minimal Data**: Use only the minimum data required to test the specific scenario
- **Realistic Values**: Use realistic but clearly identifiable test values
- **Constraint Application**: Apply necessary constraints using tSQLt.ApplyConstraint when testing constraint behavior

```sql
-- Standard fake table setup pattern
EXEC tSQLt.FakeTable 'dbo', 'Customers';
EXEC tSQLt.FakeTable 'dbo', 'Orders';
EXEC tSQLt.FakeTable 'dbo', 'OrderItems';

-- Apply constraints when testing constraint behavior
EXEC tSQLt.ApplyConstraint 'dbo.Orders', 'FK_Orders_Customers';
EXEC tSQLt.ApplyConstraint 'dbo.Orders', 'CHK_Orders_TotalAmount_Positive';
```

### Test Execution
- **Run All Tests**: `EXEC tSQLt.RunAll` to execute all tests in database
- **Run Test Class**: `EXEC tSQLt.Run 'TestClassName'` for specific test class
- **CI/CD Integration**: Include test execution in build pipelines
- **Test Output**: Review test results for failures and investigate root causes

### Best Practices
- **Mock External Dependencies**: Use tSQLt.FakeTable and tSQLt.ApplyConstraint for isolation
- **Fast Tests**: Keep tests fast by using minimal test data
- **Clear Assertions**: Use specific assertions with meaningful custom messages
- **Test Data**: Use realistic but minimal test data that clearly demonstrates the test scenario
- **Single Assertion**: Each test should verify one specific behavior
- **Descriptive Variables**: Use descriptive variable names that clearly indicate their purpose
- **Consistent Formatting**: Follow the same T-SQL formatting standards used in production code
- **Readable Test Names**: Use natural language with spaces and backtick-delimited artifact names for maximum readability
