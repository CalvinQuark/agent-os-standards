## Test coverage best practices

- **Write Minimal Tests During Development**: Do NOT write tests for every change or intermediate step. Focus on completing the feature implementation first, then add strategic tests only at logical completion points.
- **Test Only Core User Flows**: Write tests exclusively for critical paths and primary user workflows. Skip writing tests for non-critical utilities and secondary workflows until if/when you're instructed to do so.
- **Defer Edge Case Testing**: Do NOT test edge cases, error states, or validation logic unless they are business-critical. These can be addressed in dedicated testing phases, not during feature development.
- **Test Behavior, Not Implementation**: Focus tests on what the code does, not how it does it, to reduce brittleness
- **Clear Test Names**: Use descriptive names that explain what's being tested and the expected outcome
- **Mock External Dependencies**: Isolate units by mocking databases, APIs, file systems, and other external services
- **Fast Execution**: Keep unit tests fast (milliseconds) so developers run them frequently during development

### End-to-End Testing with Playwright for .NET

- **Write Tests in C#**: Use Playwright for .NET and write all tests in C# rather than TypeScript
- **Cross-Browser Testing**: Test across Chromium, Firefox, and WebKit to ensure cross-browser compatibility
- **Page Object Model**: Organize E2E tests using Page Object Model pattern for maintainability
- **Async/Await Pattern**: Use async/await for all Playwright operations (e.g., `await page.GotoAsync()`, `await page.ClickAsync()`)
- **Wait for Elements**: Use Playwright's built-in waiting mechanisms (e.g., `WaitForSelectorAsync`) instead of manual delays
- **Explicit Locators**: Use explicit, stable locators (data-testid attributes, semantic selectors) rather than brittle CSS selectors
- **Test Isolation**: Each E2E test should be independent and not rely on state from previous tests
- **Setup and Teardown**: Use test fixtures for browser setup/teardown to avoid resource leaks
- **Screenshot on Failure**: Capture screenshots automatically on test failures for debugging
- **Headless Mode**: Run tests in headless mode in CI/CD pipelines for faster execution

### Database Testing with tSQLt
- **Test Database Separation**: All unit tests run in separate `*Tests` database (e.g., `NorthwindTests`)
- **Test Independence**: Each tSQLt test must clean up after itself or use FakeTable for isolation
- **Focus on Business Logic**: Test stored procedures and functions that contain business logic
- **Minimal Test Data**: Use smallest possible dataset that proves the test case
- **Realistic Scenarios**: Test data should reflect realistic production scenarios even if minimal
- **Fast Execution**: Database tests should complete in seconds, not minutes
- **Mock External Calls**: Use tSQLt.SpyProcedure for procedures that call other procedures or external systems
