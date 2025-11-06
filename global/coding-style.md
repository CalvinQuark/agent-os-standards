## Coding style best practices

- **Consistent Naming Conventions**: Establish and follow naming conventions for variables, functions, classes, and files across the codebase
- **Automated Formatting**: Maintain consistent code style (indenting, line breaks, etc.)
- **Meaningful Names**: Choose descriptive names that reveal intent; avoid abbreviations and single-letter variables except in narrow contexts
- **Small, Focused Functions**: Keep functions small and focused on a single task for better readability and testability
- **Consistent Indentation**: Use consistent indentation (spaces; not tabs) and configure your editor/linter to enforce it
- **Remove Dead Code**: Delete unused code, commented-out blocks, and imports rather than leaving them as clutter
- **Backward compatability only when required:** Unless specifically instructed otherwise, assume you do not need to write additional code logic to handle backward compatability.
- **DRY Principle**: Avoid duplication by extracting common logic into reusable functions or modules

### C# Specific Standards

#### Braces and Formatting
- **Opening braces on same line**: Place ALL opening braces `{` on the same line as the statement that precedes them (K&R style) - applies to classes, methods, properties, control flow statements, lambda expressions, and event handlers
- **All branches use braces**: Surround all `if` and `else` statement branches with braces, regardless of whether they are single-line statements

#### Type Declarations
- **Explicit types over var**: Use explicit type names instead of `var` for better code clarity and maintainability
- **Collection expressions**: Use C# 12's collection expression syntax `[]` for initializing collections (e.g., `List<string> items = [];`)
- **Object instantiation**: Use target-typed `new()` expressions to avoid redundant type specifications
  ```csharp
  // Correct - Target-typed new with parameters
  RootCommand rootCommand = new("description");
  StringBuilder stringBuilder = new(100);
  HttpClient httpClient = new();

  // Incorrect - Redundant type specification
  RootCommand rootCommand = new RootCommand("description");
  StringBuilder stringBuilder = new StringBuilder(100);
  HttpClient httpClient = new HttpClient();
  ```
- **Primary constructors**: Where feasible, use primary constructor syntax to declare constructor parameters directly on the class declaration (e.g., `public class OrderProcessor(ILogger logger, IOrderRepository repository)`)

#### Variable Naming
- **Class-level variables**: Use underscore-prefixed camelCase (e.g., `_customerName`, `_orderId`, `_connectionString`)
- **Local variables**: Use camelCase without prefix (e.g., `customerName`, `totalPrice`)
- **Type-suffixed variables**: For non-trivial types, suffix variable names with the type name (e.g., `spinePhraseAcrosticFont`, `primaryDatabaseConnection`)
- **Single type variables**: When only one instance of a type exists in scope, use just the type name in camelCase (e.g., `artboard`, `httpClient`)

#### Method and Class Naming
- **Methods**: PascalCase and descriptive (e.g., `CalculateTotalPrice`, `ProcessCustomerOrder`)
- **Classes**: PascalCase and descriptive (e.g., `OrderProcessor`, `CustomerDataValidator`)
- **Avoid capital sequences**: Use PascalCase with only the first letter of each word capitalized, even for acronyms (e.g., `HtmlUpdater` not `HTMLUpdater`, `JsonSerializer` not `JSONSerializer`, `XmlParser` not `XMLParser`)
- **Parameters**: camelCase and descriptive (e.g., `customerId`, `customerName`, `emailAddress`)
- **Properties**: PascalCase and descriptive (e.g., `CustomerName`, `OrderDate`, `TotalAmount`)

#### Nullable Reference Types
- **Nullable always enabled**: Assume `<Nullable>enable</Nullable>` is always set in project files
- **No unnecessary null checks**: Do not check non-nullable parameters for null; only check parameters explicitly declared as nullable (e.g., `Order?`)
- **Null checks for nullable types**: When a parameter is nullable, perform null checks and throw `ArgumentNullException` if appropriate

#### Data Structures and Type Safety
- **Enums over dictionaries**: Prefer defining enums with extension methods over using dictionaries for fixed mappings
  ```csharp
  // Preferred - Enum with extension method
  public enum BankAccount {
      PersonalChecking,
      SharedPersonalVisa,
      LourdesVisa
  }

  public static class BankAccountExtensions {
      public static string GetAccountNumber(this BankAccount account) => account switch {
          BankAccount.PersonalChecking => "6686",
          BankAccount.SharedPersonalVisa => "7230",
          BankAccount.LourdesVisa => "2117",
          _ => throw new ArgumentOutOfRangeException(nameof(account))
      };

      public static int GetAccountId(this BankAccount account) => account switch {
          BankAccount.PersonalChecking => 3,
          BankAccount.SharedPersonalVisa => 4,
          BankAccount.LourdesVisa => 5,
          _ => throw new ArgumentOutOfRangeException(nameof(account))
      };
  }

  // Avoid - Dictionary for fixed mappings
  private static readonly Dictionary<string, int> AccountIdMap = new() {
      { "6686", 3 },
      { "7230", 4 },
      { "2117", 5 }
  };
  ```
- **Strongly-typed data structures**: Prefer strongly-typed classes/records over manually constructed DataTables; only convert to DataTable at the SQL Server boundary when needed
  ```csharp
  // Correct - Strongly-typed approach
  public record TransactionData(
      int AccountId,
      DateTime Date,
      string Trans,
      string Name,
      string Memo,
      decimal Amount,
      string Comment
  );

  List<TransactionData> transactions = [
      new(3, DateTime.Now, "TRX001", "John Doe", "Payment", 100.00m, "Monthly"),
      new(4, DateTime.Now, "TRX002", "Jane Smith", "Purchase", 50.00m, "One-time")
  ];

  // If needed for SQL Server TVPs, use a helper method
  DataTable ConvertToDataTable(List<TransactionData> transactions) {
      DataTable dataTable = new();
      dataTable.Columns.Add("AccountId", typeof(int));
      dataTable.Columns.Add("Date", typeof(DateTime));
      dataTable.Columns.Add("Trans", typeof(string));
      dataTable.Columns.Add("Name", typeof(string));
      dataTable.Columns.Add("Memo", typeof(string));
      dataTable.Columns.Add("Amount", typeof(decimal));
      dataTable.Columns.Add("Comment", typeof(string));

      foreach (TransactionData txn in transactions) {
          dataTable.Rows.Add(txn.AccountId, txn.Date, txn.Trans, txn.Name, txn.Memo, txn.Amount, txn.Comment);
      }

      return dataTable;
  }

  // Incorrect - Manual DataTable construction
  DataTable tvp = new();
  tvp.Columns.Add("AccountId", typeof(int));
  tvp.Columns.Add("Date", typeof(DateTime));
  tvp.Columns.Add("Trans", typeof(string));
  tvp.Columns.Add("Name", typeof(string));
  tvp.Columns.Add("Memo", typeof(string));
  tvp.Columns.Add("Amount", typeof(decimal));
  tvp.Columns.Add("Comment", typeof(string));

  foreach (var txn in transactions) {
      tvp.Rows.Add(txn.AccountId, txn.Date, txn.Trans, txn.Name, txn.Memo, txn.Amount, txn.Comment);
  }
  ```

#### String Literals and Symbol References
- **Use nameof operator**: Use the `nameof` operator instead of hard-coded string literals when referring to parameter names, method names, property names, or other code symbols
  ```csharp
  // Correct - Using nameof
  public void ProcessOrder(Order order) {
      if (order == null) {
          throw new ArgumentNullException(nameof(order));
      }
      _logger.LogInformation($"Starting {nameof(ProcessOrder)} for order {order.Id}");
  }

  // Incorrect - Hard-coded strings
  public void ProcessOrder(Order order) {
      if (order == null) {
          throw new ArgumentNullException("order");
      }
      _logger.LogInformation($"Starting ProcessOrder for order {order.Id}");
  }
  ```
- **Property change notifications**: Use `nameof` for property names in `INotifyPropertyChanged` implementations and validation scenarios
- **Configuration keys**: Consider using `nameof` for configuration keys that correspond to class properties to maintain refactoring safety

#### Method Modifiers (CA1822)
- **Static methods when possible**: Mark methods as `static` when they do not access instance data (fields, properties, or other instance methods)
- **Performance and clarity**: Static methods improve performance by avoiding unnecessary instance references and clearly signal that the method is stateless
- **CA1822 compliance**: Address CA1822 code analysis warnings by making methods static when they don't use instance members
  ```csharp
  // Correct - Static method that doesn't access instance data
  public static decimal ParseBalanceText(string balanceText) {
      // Implementation that only uses parameters
  }

  // Incorrect - Instance method that doesn't need instance access
  public decimal ParseBalanceText(string balanceText) {
      // Implementation that only uses parameters but is not marked static
  }
  ```
