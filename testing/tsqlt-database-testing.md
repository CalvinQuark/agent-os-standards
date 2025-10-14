## tSQLt Database Testing Standards

### Test Database Organization
- **Test Database Naming**: Suffix production database name with `Tests` (e.g., `Northwind` → `NorthwindTests`)
- **Test Database Location**: localhost
- **Framework**: tSQLt framework for SQL Server unit testing
- **Isolation**: Each test should be independent and not affect other tests

### Test Structure
- **Test Classes**: Organize tests into test classes matching schema or functional areas
- **Test Naming**: Use descriptive names starting with `test_` prefix
- **Setup/Teardown**: Use tSQLt.FakeTable and tSQLt.SpyProcedure for test isolation
- **Assertions**: Use tSQLt assertion procedures (AssertEquals, AssertNotEquals, AssertEmptyTable, etc.)

### Test Organization
- **Schema-based**: Create test classes per schema (e.g., `[dbo_tests]`, `[sales_tests]`)
- **Feature-based**: Or organize by feature/functionality when it makes more sense
- **Test Independence**: Each test must be self-contained with its own setup and cleanup

### What to Test
- **Stored Procedures**: Test business logic, data transformation, and edge cases
- **Functions**: Test calculations, data formatting, and return values
- **Triggers**: Test trigger firing conditions and resulting data changes
- **Constraints**: Verify that constraints properly enforce business rules
- **Views**: Test complex views return expected result sets

### Testing Patterns
- **Arrange-Act-Assert**: Follow AAA pattern in all tests
  ```sql
  CREATE PROCEDURE [TestClass].[test_ProcedureName_Behavior]
  AS
  BEGIN
      -- Arrange
      EXEC tSQLt.FakeTable 'dbo', 'TableName';
      INSERT INTO dbo.TableName VALUES (...);

      -- Act
      EXEC dbo.p_ProcedureName @param1, @param2;

      -- Assert
      EXEC tSQLt.AssertEquals @Expected = 1, @Actual = (SELECT COUNT(*) FROM dbo.ResultTable);
  END;
  ```

### Test Execution
- **Run All Tests**: `EXEC tSQLt.RunAll` to execute all tests in database
- **Run Test Class**: `EXEC tSQLt.Run 'TestClassName'` for specific test class
- **CI/CD Integration**: Include test execution in build pipelines
- **Test Output**: Review test results for failures and investigate root causes

### Best Practices
- **Mock External Dependencies**: Use tSQLt.FakeTable and tSQLt.ApplyConstraint for isolation
- **Fast Tests**: Keep tests fast by using minimal test data
- **Clear Assertions**: Use specific assertions with meaningful messages
- **Test Data**: Use realistic but minimal test data that clearly demonstrates the test scenario
